🔹 1. Repository Variables (vars)

Defined in Repo → Settings → Secrets and variables → Actions → Variables.

Accessible everywhere in the workflow with the vars context.

Example:
```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: echo "My repo variable is ${{ vars.MY_VARIABLE }}"
```

✅ Available at workflow, job, and step — no need to redefine them with env:.
❌ But you must always access them using ${{ vars.MY_VARIABLE }} (they don’t automatically become environment variables unless you put them in env:).

🔹 2. Repository Secrets (secrets)

Defined in Repo → Settings → Secrets and variables → Actions → Secrets.

Work the same way as vars, but encrypted.

Example:
```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - run: echo "My secret is ${{ secrets.MY_SECRET }}"
```

✅ Also available anywhere in the workflow.
⚠️ GitHub masks them in logs automatically.

🔹 3. Making repo variables available as normal env vars

If you want repo-level variables/secrets to behave like your env: variables, you can pass them down explicitly:
```yaml
env:
  FROM_REPO_VAR: ${{ vars.MY_VARIABLE }}
  FROM_REPO_SECRET: ${{ secrets.MY_SECRET }}

jobs:
  demo:
    runs-on: ubuntu-latest
    steps:
      - run: |
          echo "Var: $FROM_REPO_VAR"
          echo "Secret: $FROM_REPO_SECRET"
```
Now you can just use $FROM_REPO_VAR inside scripts without ${{ ... }}.

✅ So yes:
Repo-level variables/secrets are available everywhere (workflow, job, step), but how you access them differs:

Direct with ${{ vars.NAME }} or ${{ secrets.NAME }}.

Or map them into env: if you want them to look like environment variables ($NAME).
