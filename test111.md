name: Deploy to AWS vfmp-ObjHydProgram

on:
  workflow_dispatch:
  workflow_call:

permissions:
    id-token: write
    contents: read
    actions: read
    security-events: write
    pull-requests: write
    checks: write

jobs:
  build:
    name: Build Image
    uses: department-of-veterans-affairs/ped-services-common/.github/workflows/build-template.yml@develop
    with:
      BRANCH: ${{ github.ref_name }}
      APP_DIR_ROOT: 'PayerEDI.TAS.CXM'
      APP_PROJ_NAME: 'PayerEDI.TAS.Remediation.Containers'
      APP_PROJ_FILE: 'PayerEDI.TAS.Remediation.Containers.csproj'
      ECR_REPOSITORY: 'vfmp-remediation'
      DOCKERFILE_TYPE: 'Dockerfile.app'
      ROLE: ${{ vars.AWS_GH_ROLE }}
      MONITOR_PATHS: >
        .github/workflows/test-build-pipeline.yml
        .github/workflows/build-vfmp-remediation.yml
        Dockerfile.app
        PayerEDI.TAS.CXM/PayerEDI.TAS.Remediation.Containers/
        PayerEDI.TAS.CXM/PayerEDI.TAS.RefNugetCommon/
    secrets:
      REGISTRY_USER: ${{ secrets.REGISTRY_USER }}
      REGISTRY_TOKEN: ${{ secrets.REGISTRY_TOKEN }}
      MSSQL_DOCKER_PASS: ${{ secrets.MSSQL_DOCKER_PASS }}
