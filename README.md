# gcr-build-push
Composite Github Action to build and push your repo/container to Google's Container Registry (GCR - gcr.io)

## Usage
| Option | Default Value | Notes |
| ------------ | ------------ | ------------ |
| tags           | `latest`          | CSV of tags: `latest,v1,v1.0.1`  |
| project-id     | *required*        | GCP project-id e.x.`my-project-123456`  |
| container-name | implied from repo | name of the container or the repo name if not set  |
| GCR-key        | *required*        | JSON key with the required permissions for GCR  |

Outputs: `image-name` a static tag from the sha of the commit which triggered the build e.x.`gcr.io/my-project-123456/container-name:139408532689841229c6ba254b0dcc8a1d8eef96`

### Example Workflow
```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Build and push repo
        uses: DanielBarnes/gcr-build-push@main
        with:
          tags: latest
          project-id: ${{ secrets.GCP_PROJECT_ID }}
          GCR-key: ${{ secrets.GCP_GCR_KEY }}
```

## Compontent Actions
- [actions/checkout@v2](https://github.com/actions/checkout/tree/v2)
- [actions/github-script@v5](https://github.com/actions/github-script/tree/v5)
- [docker/login-action@v1](https://github.com/docker/login-action/tree/v1)
- [docker/setup-buildx-action@v1](https://github.com/docker/setup-buildx-action/tree/v1)
- [docker/build-push-action@v2](https://github.com/docker/build-push-action/tree/v2)
