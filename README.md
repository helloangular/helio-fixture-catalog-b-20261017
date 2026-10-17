# helio-fixture-catalog-b-20261017

Catalog lane B: a synthetic Helio Environment Catalog fixture on GitHub App B
(`helio-client-capacity-b`). It is used for the BlueMatrix Environment Catalog test cases on
https://cicd.dagly.io and is kept apart from the QA catalog lane and the 33 shared
capacity-b lanes. Nothing is deployed.

- Caller: `.github/workflows/cb-catalog-release.yml` (dispatched by Helio, `workflow_dispatch`).
- Template: `helloangular/helio-client-capacity-20260916/.github/workflows/cb-catalog-deploy.yml@cb-catalog-20261017`
  (stages `qa` then `production`, GitHub-hosted `ubuntu-latest` runners).
- Catalog environments: `cb-qa-east` (qa) and `cb-prod-east` (production), written by Helio.

Rules:

- Every commit to `main` needs the tag `helio/workflow/<sha>` in the same step, or every Helio
  release start blocks with `github_pinned_dispatch_ref_unavailable`.
- New versions: change `VERSION`, commit, push, tag.
- Failure switch: a commit that adds `.helio-cb/catalog-fail/<environment>` makes that
  environment's job fail. Remove the file in the next commit.
