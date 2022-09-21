# Colvin Deploy

Global Github Action for Colvin applications deployment.

The installation of dependencies and tools is done individually in each project, outside of this action.

## Setup

Add this Action as an additional step to each project.

```sh
    - name: "Deploy"
      uses: TheColvinCo/colvin-deploy-action@{VERSION}
```

**Note**: Review last available version: https://github.com/TheColvinCo/colvin-deploy-action/releases

## Expected variables

In the main Action of each project, we will specify the variables block, like this example.

```sh
env:
  PROJECT_ID: "gcp-project"
  APP_NAME: "colvin"
  SA_GCP: ${{ secrets.SA_GCP }}
  GIT_CRYPT_KEY: ${{ secrets.GIT_CRYPT_KEY }}
  REGISTRY: "europe-docker.pkg.dev/gcp-project/colvin/"
  GCP_REGION: "europe-west9"
  GCP_ZONE: "europe-west9-a"
  GCS_DYNAMIC: 'clv-dynamic-envs'
  K8S_PROD: "colvin"
  K8S_STG: "stage"
  K8S_STG_LOCATION: 'region'
  EXEC_TERRAFORM: "true"
  EXEC_DOCKER: "true"
  EXEC_HELM: "true"
  DIFF_TERRAFORM: "true"
  HELM_TIMEOUT: "5m"
  HELM_PATH: "./helm"
  TERRAFORM_PATH: "./terraform"
  CONTAINER_LIST: "web"
  BUILD_ARG_PROD: "--build-arg environment=production"
  BUILD_ARG_STG: "--build-arg environment=stage"
  BUILD_USE_WORKSPACE: "false"
  DNS_ZONE: 'blommarket-com'
  DNS_DOMAIN: 'blommarket.com'
  GCS_DYNAMIC: 'clv-dynamic-envs'
  SLACK_EMOJI: ':basket:'
```


- `PROJECT_ID` - Unique identifier of the project in GCP

- `APP_NAME` - Helm chart main name.

- `SA_GCP` - Secret with the GCP Service Account with the necessary permissions.

- `GIT_CRYPT_KEY` - Secret with git-crypt key to decrypt files.

- `REGISTRY` - Google Cloud Artifact image repository name.

- `GCP_REGION` - GCP main project region.

- `GCP_ZONE` - GCP main project zone, for a zonal resouces.

- `GCS_DYNAMIC` -

- `K8S_PROD` - Kubernetes cluster name for production.

- `K8S_STG:` - Kubernetes cluster name for stage.

- `K8S_STG_LOCATION` - [region|zone] Indicate the location of the stage cluster

- `EXEC_TERRAFORM:` - If our application has terraform and we want to execute the terraform steps in the deploy process (init, apply).

- `EXEC_DOCKER:` - If our application needs to run the docker image build process (build, push).

- `EXEC_HELM:` - If our application has to update or install a Helm chart.

- `DIFF_TERRAFORM:` - If we want to do a check for the terraform folder and avoid deploy when there are breaking changes (modified files).

- `HELM_TIMEOUT` - Maximum time for the execution of the helm upgrade command.

- `HELM_PATH` - Root directory with the Helm chart.

- `TERRAFORM_PATH` - Root directory with erraform definitions.

- `CONTAINER_LIST` - List of containers to do the image build, list separated by space.

- `BUILD_ARG_PROD` - Additional parameters during the build process in production, e.g. --build-args.

- `BUILD_ARG_STG` - Additional parameters during the build process in stage, e.g. --build-args.

- `BUILD_USE_WORKSPACE` - If we want to add the stage workspace at the end of the build-args to make the build dynamic according to the environment.

- `DNS_ZONE` - DNS zone ID in Google Cloud DNS.

- `DNS_DOMAIN` - DNS zone root domain.

- `GCS_DYNAMIC` - Identifier of the bucket in GCS that saves the states of the dynamic environments.

- `SLACK_EMOJI` - Emoticon of notifications in Slack.
