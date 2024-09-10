# DIG CLI Store Management Action

This GitHub Action allows you to interact with a DIG (Decentralized Internet Gateway) store by cloning, committing, and pushing changes. The action installs the `@dignetwork/dig-chia-cli` package, clones a specified store using a `store_id`, and commits and pushes any changes.

## Inputs

| Name              | Description                                   | Required | Default |
|-------------------|-----------------------------------------------|----------|---------|
| `store_id`        | The Store ID for the DIG store                | Yes      | N/A     |
| `remote_password` | The password for the remote peer              | Yes      | N/A     |
| `remote_username` | The username for the remote peer              | Yes      | N/A     |
| `remote_ip`       | The IP address of the remote peer             | Yes      | N/A     |

### Input Details

- **`store_id`**: The ID of the DIG store you want to interact with.
- **`remote_password`**: The password to authenticate with the remote peer (stored securely in GitHub Secrets).
- **`remote_username`**: The username to authenticate with the remote peer.
- **`remote_ip`**: The IP address of the remote peer where the DIG store resides.

## Example Usage

Below is an example of how to use this action in your GitHub workflows:

```yaml
name: Manage DIG Store

on:
  push:
    branches:
      - main

jobs:
  dig-store-management:
    runs-on: ubuntu-latest
    steps:
      - name: Use DIG Store Management Action
        uses: ./path-to-action/action.yaml
        with:
          store_id: ${{ var.STORE_ID }}
          remote_password: ${{ secrets.DIG_REMOTE_PASSWORD }}
          remote_username: ${{ secrets.DIG_REMOTE_USERNAME }}
          remote_ip: ${{ var.DIG_REMOTE_IP }}
```

### Steps in the Example:

1. **Trigger**: This workflow is triggered when there is a push to the `main` branch.
2. **Use DIG Store Management Action**: The action is called to interact with a DIG store:
   - The `store_id`, `remote_password`, `remote_username`, and `remote_ip` are provided as inputs.

### Secrets

You need to store sensitive data, such as the `remote_password`, in your repository’s GitHub Secrets. You can add the secret under `Settings > Secrets` in your repository.

Example:

```bash
REMOTE_PASSWORD=your-secure-password
```

## Steps in the Action

1. **Checkout Code**: The action checks out the code from your repository.
2. **Install DIG CLI**: It installs the `@dignetwork/dig-chia-cli` package globally.
3. **Set up Remote**: Adds the remote credentials for the DIG CLI using the provided username, password, and IP.
4. **Clone DIG Store**: Clones the DIG store using the provided `store_id`.
5. **Commit to DIG Store**: Commits any changes to the cloned DIG store.
6. **Push to DIG Store**: Pushes the committed changes to the remote DIG store.

## How to Use

1. **Create the `action.yaml` file**:
   Save the reusable action code in your repository as `action.yaml`.

2. **Add a Workflow**:
   Create a GitHub Actions workflow that uses the reusable action. Ensure you provide the necessary inputs and secrets.

3. **Configure GitHub Secrets**:
   Ensure the sensitive data, such as `remote_password`, is stored securely in GitHub Secrets.

4. **Run the Workflow**:
   Once the workflow is triggered (e.g., on a `push` event), the action will install the DIG CLI, clone the store, commit changes, and push them back to the remote.
