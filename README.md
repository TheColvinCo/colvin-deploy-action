# Colvin Deploy

Global Github Action for Colvin applications deployment.

The installation of dependencies and tools is done individually in each project, outside of this action.

## Setup

Add this Action ction as an additional step to each project.

```sh
    - name: "Deploy"
      uses: TheColvinCo/colvin-deploy-action@{VERSION}
```

**Note**: Review last available version: https://github.com/TheColvinCo/colvin-deploy-action/releases

## Expected variables

In the main action of each project, we will specify the variables block, like this example.

```sh
env:
  PROJECT_ID: "gcp-project"
  LIMIT_STG: "2"
  MAJOR_VERSION: "1"
  APP_NAME: "colvin"
  SA_GCP: ${{ secrets.SA_GCP }}
  GIT_CRYPT_KEY: ${{ secrets.GIT_CRYPT_KEY }}
  REGISTRY: "europe-docker.pkg.dev/gcp-project/colvin/"
  GCP_REGION: "europe-west9"
  GCP_ZONE: "europe-west9-a"
  K8S_PROD: "colvin"
  K8S_STG: "stage"
  EXEC_TERRAFORM: "true"
  EXEC_DOCKER: "true"
  EXEC_HELM: "true"
  HELM_TIMEOUT: "5m"
  HELM_PATH: "./helm"
  TERRAFORM_PATH: "./terraform"
  CONTAINER_LIST: "web"
  BUILD_ARG_PROD: "--build-arg environment=production"
  BUILD_ARG_STG: "--build-arg environment=stage"
  BUILD_USE_WORKSPACE: "false"
```


- `PROJECT_ID` - Unique identifier of the project in GCP

- `LIMIT_STG` - We can determine the maximum number of stage environments allowed by the application.

- `MAJOR_VERSION` - Used for construction of the version tag, MAJOR_VERSION.X

- `APP_NAME` - Helm chart main name.

- `SA_GCP` - Secret with the GCP Service Account with the necessary permissions.

- `GIT_CRYPT_KEY` - Secret with git-crypt key to decrypt files.

- `REGISTRY` - Google Cloud Artifact image repository name.

- `GCP_REGION` - GCP main project region.

- `GCP_ZONE` - GCP main project zone, for a zonal resouces.

- `K8S_PROD` - Kubernetes cluster name for production.

- `K8S_STG:` - Kubernetes cluster name for stage.

- `EXEC_TERRAFORM:` - If our application has terraform and we want to execute the terraform steps in the deploy process (init, apply).

- `EXEC_DOCKER:` - If our application needs to run the docker image build process (build, push).

- `EXEC_HELM:` - If our application has to update or install a Helm chart.

- `HELM_TIMEOUT` - Maximum time for the execution of the helm upgrade command.

- `HELM_PATH` - Root directory with the Helm chart.

- `TERRAFORM_PATH` - Root directory with erraform definitions.

- `CONTAINER_LIST` - List of containers to do the image build, list separated by space.

- `BUILD_ARG_PROD` - Additional parameters during the build process in production, e.g. --build-args.

- `BUILD_ARG_STG` - Additional parameters during the build process in stage, e.g. --build-args.

- `BUILD_USE_WORKSPACE` - If we want to add the stage workspace at the end of the build-args to make the build dynamic according to the environment.

