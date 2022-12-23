# Mirror repo to GitLab

This repo contains a reusable Github Actions workflow that mirrors the current repo to GitLab.

To use it for mirroring a new repo:
- Create a new corresponding project in GitLab under [ITMO-NSS-team](https://gitlab.actcognitive.org/itmo-nss-team)

- Either import the project from GitHub in the UI or create a blank project and manually clone the repo from GitHub:
```
git clone --mirror <github_repo_web_URL>
cd <repo_name>.git
git push --mirror <gitlab_repo_web_URL>
```

- Set secrets `GITLAB_USER` and `GITLAB_PASSWORD` in your GitHub repo (this is required only for private repos)

- In the GitHub repo create `.github/workflows/mirror_repo_to_gitlab.yml` with the following content:
```
name: Mirror repo to GitLab

on: [push, pull_request, delete]

jobs:
  call-nss-ops-mirror-workflow:
    uses: ITMO-NSS-team/NSS-Ops/.github/workflows/mirror-repo.yml@master
    with:
      GITLAB_URL: '<gitlab_repo_web_URL>'
    secrets:
      GITLAB_USER: ${{ secrets.GITLAB_USER }}
      GITLAB_PASSWORD: ${{ secrets.GITLAB_PASSWORD }}
```

- Make sure to set the `GITLAB_URL` var in the yaml file

 
Every push to the repo will trigger this action, it will automatically synchronize commits and branches.
PRs, issues and wikis will NOT be mirrored.

If you import the repo from GitHub through the UI, issues and PRs will get cloned as well, but all further changes will not be synchronized for them.