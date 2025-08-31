# GitHub Actions vs Azure DevOps — Variable & Context Cheat Sheet

| **Purpose**                  | **GitHub Actions** (YAML)                         | **Azure DevOps** (YAML)                  |
|-------------------------------|--------------------------------------------------|------------------------------------------|
| **Custom variable**           | `env:` block → `${{ env.MY_VAR }}`<br>`echo $MY_VAR` | `variables:` block → `$(MY_VAR)`<br>`echo $(MY_VAR)` |
| **Repo / pipeline variable**  | `${{ vars.MY_VAR }}`                             | `$(MY_VAR)` (from pipeline or variable group) |
| **Secret variable**           | `${{ secrets.MY_SECRET }}`                       | `$(MY_SECRET)` (from pipeline / KeyVault / library) |
| **Branch / Ref**              | `${{ github.ref }}`                              | `$(Build.SourceBranch)` |
| **Commit SHA**                | `${{ github.sha }}`                              | `$(Build.SourceVersion)` |
| **Build / Run ID**            | `${{ github.run_id }}`                           | `$(Build.BuildId)` |
| **Workflow name**             | `${{ github.workflow }}`                         | `$(Build.DefinitionName)` |
| **Job name**                  | `${{ github.job }}`                              | `$(Agent.JobName)` |
| **Trigger event**             | `${{ github.event_name }}`                       | `$(Build.Reason)` |
| **Access environment var**    | `${{ env.VAR_NAME }}` or `$VAR_NAME` in script   | `$(VAR_NAME)` in tasks/scripts |
| **Dynamic variable (runtime)**| `echo "MYVAR=123" >> $GITHUB_ENV` → `$MYVAR`     | `echo "##vso[task.setvariable variable=MYVAR]123"` → `$(MYVAR)` |

---

### 🔎 Key Points
- **GitHub Actions** = context objects (`github`, `env`, `vars`, `secrets`) → always `${{ ... }}`.  
- **Azure DevOps** = macro syntax `$(VarName)` → no explicit contexts, system vars are prefixed (`Build.*`, `Agent.*`, etc.).  
- **Runtime variables**:  
  - GitHub → `$GITHUB_ENV` file  
  - Azure DevOps → `##vso[task.setvariable ...]` logging command  

---

✅ With this table, you can translate any GitHub Actions context to its Azure DevOps equivalent.
