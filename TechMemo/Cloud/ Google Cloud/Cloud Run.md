## GitHub Actions経由でCloud Runにデプロイするワークフローのサンプル

1. service.ymlを作る
2. GitHub Actionsのワークフローを作る

参考: [GitHub Actions からのキーなしの認証の有効化](https://cloud.google.com/blog/ja/products/identity-security/enabling-keyless-authentication-from-github-actions)

[service.yml]
```yml
apiVersion: serving.knative.dev/v1
kind: Service
metadata:
  annotations:
    run.googleapis.com/ingress: internal-and-cloud-load-balancing
    run.googleapis.com/cpu-throttling: true
  name: rag-memo
spec:
  template:
    spec:
      containers:
        - image: rag-memo:xxxxx
          ports:
            - containerPort: 80
          env:
            - name: APP_KEY
              valueFrom:
                secretKeyRef:
                  key: "1"
                  name: APP_KEY
```

[.github/workflows/release-cloudrun.yml]
```yml
name: Build & Release Staging

on:
  push:
    branches:
      - "main"

permissions:
  id-token: write
  contents: read

env:
  PROJECT_ID: hoge_id
  REGION: asia-east1
  ENV_TYPE: stg
  WORKLOAD_IDENTITY_PROVIDER: projects/9299232/locations/global/workloadIdentityPools/github-actions/providers/hoaad
  SERVICE_ACCOUNT: hoge-github-actions@hoge_id.iam.gserviceaccount.com

jobs:
  build-stg:
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@b4ffde65f46336ab88eb53be808477a3936bae11 # v4.1.1

      - name: Authenticate Google Cloud
        id: auth
        uses: google-github-actions/auth@35b0e87d162680511bf346c299f71c9c5c379033 # v1.1.1
        with:
          token_format: access_token
          workload_identity_provider: ${{ env.WORKLOAD_IDENTITY_PROVIDER }}
          service_account: ${{ env.SERVICE_ACCOUNT }}

      - name: Login Artifact Registry
        uses: docker/login-action@343f7c4344506bcbf9b4de18042ae17996df046d # v3.0.0
        with:
          registry: ${{ env.REGION }}-docker.pkg.dev
          username: oauth2accesstoken
          password: ${{ steps.auth.outputs.access_token }}

      - name: Configure Docker
        run: |
          gcloud auth configure-docker ${{ env.REGION }}-docker.pkg.dev --project ${{ env.PROJECT_ID }}
        shell: bash

      - name: Setup Docker Buildx
        uses: docker/setup-buildx-action@f95db51fddba0c2d1ec667646a06c2ce06100226 # v3.0.0

      - name: Create .env
        run: cp ./deploy/env/.env.example .env

      - name: Build docker image
        uses: docker/build-push-action@0565240e2d4ab88bba5387d719585280857ece09 #v5.0.0
        with:
          context: .
          push: true
          build-args: ${{ inputs.build_args }}
          file: ./docker/Dockerfile
          tags: |
            ${{ inputs.image_uri }}:latest
            ${{ inputs.image_uri }}:${{ github.sha }}-${{ github.run_attempt }}
          cache-from: type=registry,ref=${{ inputs.image_uri }}:latest
          cache-to: type=inline

  release-stg:
    runs-on: ubuntu-22.04
    needs: build-stg
    steps:
      - uses: actions/checkout@b4ffde65f46336ab88eb53be808477a3936bae11 # v4.1.1

      - name: Authenticate Google Cloud
        uses: google-github-actions/auth@35b0e87d162680511bf346c299f71c9c5c379033 # v1.1.1
        with:
          token_format: access_token
          workload_identity_provider: ${{ env.WORKLOAD_IDENTITY_PROVIDER }}
          service_account: ${{ env.SERVICE_ACCOUNT }}     

      - name: Update Container Image
        run: |
          envsubst < deploy/cloudrun/service.yml > service.yml
        env:
          DEPLOY_IMAGE_TAG: ${{ needs.tagging-deploy-image.outputs.deploy-image-tag }}

      - name: Deploy Cloud Run Service
        run: |
          gcloud run services replace service.yml \
            --region=${{ env.REGION }} \
            --project=${{ env.PROJECT_ID }}
```

## hoge