# setup-replicate

## Usage

Add a step to your workflow that uses this action:

```yaml
- name: Setup Replicate
  uses: replicate/setup-replicate@main
  with:
    token: ${{ secrets.REPLICATE_API_TOKEN }}
```

Now you can run the `replicate` CLI in subsequent steps.


## Example: Model CI/CD

Here's an example that pushes a Cog model to Replicate whenever your repo's `main` branch is updated:

```yml
name: CI

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Check out code
        uses: actions/checkout@v3

      - name: Setup Cog
        uses: replicate/setup-cog@v1
        with:
          token: ${{ secrets.REPLICATE_API_TOKEN }}

      - name: Setup Replicate
        uses: replicate/setup-replicate@main
        with:
          token: ${{ secrets.REPLICATE_API_TOKEN }}

      - name: Push the model
        run: |
          cog push r8.im/zeke/hello-world

      - name: Run the model
        run: |
          cog run zeke/hello-world
```

### Inputs

This following inputs can be specified using the `with` keyword:

- `replicate-version`: The version of the Replicate CLI to install in the form `vX.Y.Z`. See [CLI releases](https://github.com/replicate/cli/releases) for a list of available versions. Defaults to latest.
- `token`: Your Replicate API token. If set, the Action will automatically authenticate to Replicate using `replicate auth login`. To use this feature, get a token from [replicate.com/account](https://replicate.com/account), then create a repository secret named `REPLICATE_API_TOKEN` in your GitHub repo's settings.

