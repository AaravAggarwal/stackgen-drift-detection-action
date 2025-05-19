# StackGen Drift Detection Action

This GitHub Action triggers StackGen's infrastructure drift detection using the StackGen CLI. It mirrors the structure of the [Generate IaC Action](https://github.com/appcd-dev/action).

## ✅ Setup

1. Sign up at [StackGen](https://cloud.stackgen.com/)
2. Generate a **Personal Access Token (PAT)** from your [Account Settings](https://cloud.stackgen.com/account-settings/pat/)
3. Add that token as a secret in your repo, using the name: `STACKGEN_API_KEY`

## 🔧 Inputs

| Name           | Description                              | Required |
|----------------|------------------------------------------|----------|
| `appstack_id`  | The ID of the appStack to check          | ✅ Yes    |
| `region`       | Region for the appStack (e.g. us-east-1) | ✅ Yes    |

## 🚀 Usage

```yaml
- name: Detect Infrastructure Drift
  uses: your-org/stackgen-drift-action@v0
  env:
    STACKGEN_API_KEY: ${{ secrets.STACKGEN_API_KEY }}
  with:
    appstack_id: 'abc123'
    region: 'us-east-1'