# StackGen Drift Detection Action

This GitHub Action triggers StackGen's drift detection through the StackGen CLI. It mirrors the structure of the [Generate IaC Action](https://github.com/appcd-dev/generate-action).

## ✅ Setup

Please follow the steps below to setup the action:

1. Signup for an account on [StackGen](https://cloud.stackgen.com/)
2. Setup a **Personal Access Token** on [StackGen](https://cloud.stackgen.com/account-settings/pat/)
3. Add that token as a secret in your repository with the name: `STACKGEN_TOKEN`


## 🔧 Inputs

| Name           | Description                              | Required |
|----------------|------------------------------------------|----------|
| `appstack_id`  | The ID of the appStack to check          | ✅ Yes   |
| `region`       | Region for the appStack (e.g. us-east-1) | ✅ Yes   |

## 🚀 Usage

```yaml
name: Drift Detection

on:
  # Manual trigger
  workflow_dispatch:

  # Scheduled run every day at 6 AM UTC
  schedule:
    - cron: '0 6 * * *'

jobs:
  drift:
    runs-on: ubuntu-latest
    steps:
      - name: Trigger StackGen Drift Detection
        uses: AaravAggarwal/stackgen-drift-detection-action@main
        env:
          STACKGEN_TOKEN: ${{ secrets.STACKGEN_TOKEN }}
        with:
          appstack_id: 'app-stack-12345'
          region: 'us-east-1'

