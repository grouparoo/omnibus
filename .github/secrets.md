# Repository secrets

The following secrets are required to run the various GitHub Action workflows in this repository:

- `BOT_NPM_TOKEN`: NPM token that has access to the `@grouparoo/ui-enterprise` package.
- `DOCKERHUB_USERNAME`: Username for the Docker Hub account that will publish the docker image.
- `DOCKERHUB_PASSWORD`: Password for the Docker Hub account that will publish the docker image.
- `TERRAFORM_NOTIFIER_APP_ID`: GitHub App ID for authenticating to the GitHub API when notifying infra-apps that there's a new image available.
- `TERRAFORM_NOTIFIER_APP_PRIVATE_KEY`: GitHub App Private Key for authenticating to the GitHub API when notifying infra-apps that there's a new image available.
- `OMNIBUS_APP_ID`: GitHub App ID for creating PRs to this repo.
- `OMNIBUS_APP_PRIVATE_KEY`: GitHub App Private Key for creating PRs in this repo.
- `BOT_PR_REVIEWER_USERS`: Comma-separated list of users whose review will be requested on action-generated PRs.

### Required GitHub Apps

Two distinct GitHub Apps are required to run actions in this repo. A new GitHub App can be created [here](https://github.com/organizations/grouparoo/settings/apps/new).

To sign requests, the app's private key is required. Instructions for generating a private key can be found [here](https://docs.github.com/en/developers/apps/building-github-apps/authenticating-with-github-apps). The contents of the key will need to be copied into the `XYZ_APP_PRIVATE_KEY` GitHub secret.

**Omnibus GitHub App**

This app is used when creating PRs to this repo via actions, such as when automatically updating the Grouparoo version.

It needs to be installed on this repo (`grouparoo/omnibus`) and be given the following permissions:
- `Contents`: Read & write.
- `Pull requests`: Read & write.

**Notifier GitHub App**

This app is used when notifying another repository that there's a new image available.

It needs to be installed on the repo that will be notified (infra-apps) and be given the following permissions:
- `Actions`: Read & write.
