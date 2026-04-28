# yiisoft-demo-diary-poc

Replica of yiisoft/demo-diary's CI workflow.

Demonstrates fork checkout + composer install script injection:
- `pull_request_target` triggers on any fork PR (no gate, no approval)
- `cs-fix` job checks out the fork with `ref: github.head_ref` + `repository: github.event.pull_request.head.repo.full_name`
- Runs `composer install` via `ramsey/composer-install@v3` on attacker's code
- Attacker adds `post-install-cmd` script to `composer.json` with exfil payload
- `YIISOFT_GITHUB_TOKEN` custom PAT exposed in the same job
- `GITHUB_TOKEN` has `contents: write`

Used for authorized security research only.
