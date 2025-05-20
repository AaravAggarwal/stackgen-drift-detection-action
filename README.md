# StackGen Drift Detection Action

This GitHub Action triggers StackGen's drift detection through the StackGen CLI. It mirrors the structure of the [Generate IaC Action](https://github.com/appcd-dev/generate-action).

## ✅ Setup

Please follow the steps below to setup the action:

1. Signup for an account on [StackGen](https://cloud.stackgen.com/)
2. Make an appStack and note the appStack id (part of the URL after /appstacks/)
3. Setup a **Personal Access Token** on [StackGen](https://cloud.stackgen.com/account-settings/pat/)
4. Add the PAT as a GitHub secret: `STACKGEN_TOKEN`
5. Add any other necessary cloud provider credentials your appStack requires


## 🔧 Inputs

| Name           | Description                              | Required |
|----------------|------------------------------------------|----------|
| `appstack_id`  | The ID of the appStack to check          | ✅ Yes   |
| `region`       | Region for the appStack (e.g. us-east-1) | ✅ Yes   |

## 🚀 Usage

Create a new workflow under `.github/workflows/` in your project

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
    - name: Checkout repo
        uses: actions/checkout@v3

    - name: Create temporary directory
        run: mkdir -p tmp
jobs:
  drift:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout repo
      uses: actions/checkout@v3

    - name: Create temporary directory
      run: mkdir -p tmp

    - name: Trigger StackGen Drift Detection
      uses: AaravAggarwal/stackgen-drift-detection-action@main
      env:
        STACKGEN_TOKEN: ${{ secrets.STACKGEN_TOKEN }}
        TMPDIR: ${{ github.workspace }}/tmp
        # add any cloud provider creds your appStack needs (ex:
        #AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID}}
        #AWS_SECRET_ACCESS_KEY_ID: ${{ secrets.AWS_SECRETS_ACCESS_KEY_ID}}
      with:
        appstack_id: 'your-appstack-id-here' # this is found in the URL of your appStack after /appstacks/
        region: 'your-region-here'  # e.g. us-east-1