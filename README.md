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

```yaml
- name: Generate a haiku
  run: replicate run meta/llama-2-70b-chat prompt="Write a haiku about llamas"
```

### Inputs

This following inputs can be specified using the `with` keyword:

- `replicate-version`: The version of the Replicate CLI to install in the form `vX.Y.Z`. See [CLI releases](https://github.com/replicate/cli/releases) for a list of available versions. Defaults to latest.
- `token`: Your Replicate API token. If set, the Action will automatically authenticate to Replicate using `replicate auth login`. To use this feature, get a token from [replicate.com/account](https://replicate.com/account), then create a repository secret named `REPLICATE_API_TOKEN` in your GitHub repo's settings.

