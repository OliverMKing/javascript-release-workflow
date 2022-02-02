# javascript-release-workflow

Github workflow to simplify creating a release for a Node.js action. This will automatically increment the version of a tag (ex: v1.1 -> v1.2, v2 -> v2.1).

New releases are cut from the main (or master) branch. When creating a release branch PR we install all `node_modules` and execute `npm run build`. A draft release will also be created if any branch with the prefix `releases/` is pushed to.

This was created for the specific workflow of two digit release names (first number for major / breaking improvements and 2nd number for smaller changes). Major releases are stored on a `releases/v1` branch with the number corresponding to the major version. Modifying this workflow to support other workflows would be trivial.

Previously, to create a release for a Node.js project, developers had to:

- Create a new branch (if a new major version)
- Remove node_modules and remove them from .gitignore
- Run `npm install --no-bin-links`
- Push to the new branch
- Check which tag should be used
- Create a tag
- Create the release

These workflows automate the process.

## Usage

Add the following to your workflow files for a [reusable workflow](https://docs.github.com/en/actions/using-workflows/reusing-workflows).

```yaml
release-pr:
  uses: OliverMKing/javascript-release-workflow/release-pr.yml@main
  with:
    release: {{ github.event.inputs.release }}
```

and

```yaml
tag-and-release:
  uses: OliverMKing/javascript-release-workflow/tag-and-release.yml@main
```

Alternatively, you can copy the yaml files ([release-pr.yml](./release-pr.yml) and [tag-and-release.yml](./tag-and-release.yml)) in this repository to your `.github` folder. Replace `main` with `master` in the `Reset promotion branch` step ([release-pr.yml](./release-pr.yml)) depending on your repo.

When you want to create a workflow follow these steps:

- Go to the `Actions` tab of your Github repository
- Select `Create release PR` on the left side
- Select `Run workflow` then enter your release version (ex: v1, v2, v3)
- Find the created pull request and approve it (it may take a minute for the workflow to create the new release)
- Go to `Releases` then edit the created release (edit title, add release notes) and publish release
