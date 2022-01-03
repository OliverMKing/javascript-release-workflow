# javascript-release-workflow

Github workflow to simplify creating a release for a Node.js action. This will automatically increment the version of a tag (ex: v1.1 -> v1.2, v2 -> v2.1, v3.1.1 -> v3.1.2)

Previously, to create a release for a Node.js project, developers had to:

- Create a new branch (if a new major version)
- Remove node_modules and remove them from .gitignore
- Run `npm install --no-bin-links`
- Push to the new branch
- Create a tag
- Create the release

These workflows automate the process.

## Usage

Copy the yaml files ([release-branch-pr.yml](./release-branch-pr.yml) and [tag-and-release.yml](./tag-and-release.yml)) in this repository to your `.github` folder.

When you want to create a workflow follow these steps:

- Go to the `Actions` tab of your Github repository
- Select `Create release branch` on the left side
- Select `Run workflow` then enter your release version
- Find the created pull request and approve it (it may take a minute for the workflow to create the new release)
- Go to `Releases` then edit the created release (edit title, add release notes) and publish release

You can easily modify these workflows to fit other types of projects. Simply modify the `Install packages` and `Remove node_modules from gitignore` steps in [release-branch-pr.yml](./release-branch-pr.yml) to match how your project's release code needs to be built.
