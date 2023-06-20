# promote-docker-image-action

To make this action available to other repos, it needs to be `internal` visibility, and "Accessible from repositories in the 'vivantehealth' organization" set in [Settings->Actions](https://github.com/vivantehealth/terraform-plan-action/settings/actions)

This action retags an image with an environment tag, effectively promoting it to a new environment. It looks up the PR that was introduced the current commit, and uses the sha from the head commit of that PR as the source tag to pull. Therefore, this action is meant to be used in CI/CD workflows where the docker image is built on a branch and tagged with a commit at that time. It allows an image to be built once and used in any environment.

Suggested use:

```yaml
permissions:
  contents: read
  pull-requests: read
jobs:
  run:
    name: Run
    runs-on: ubuntu-latest
    steps:
      - name: Run action
        uses: vivantehealth/promote-docker-image-action@v1
        with:
          environment: int
          image_name: image #default
          workload_identity_provider: vars.WORKLOAD_IDENTITY_PROVIDER
          gcp_service_account: vars.GCP_SERVICE_ACCOUNT
          docker_registry: vars.DOCKER_REGISTRY
```
