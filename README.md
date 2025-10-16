# GithubActions
Testing Github Actions

[![Actions](https://github.com/CodingAero/GithubActions/actions/workflows/gh_actions.yml/badge.svg)](https://github.com/CodingAero/GithubActions/actions/workflows/gh_actions.yml)


## Overview
Learning to use Github Actions feels like a valueable skill to build. This repository automatically commits updates to a markdown file.

### Adding a Workflow
Within your repository, create a directory structure for `.github/workflows` and create a `.yml` file with a name describing the scripts purpose.
See my workflow for an example but lets quickly cover a few aspects of this file.

#### Triggering the Workflow

The workflow is triggered by a `schedule` using a `cron` expression.
The workflow contains a single job named commit, which executes on a standard ubuntu-latest runner.

#### Checkout the Repository

The first step uses the standard `actions/checkout@v2` action to prepare the runner environment. This essential process downloads a copy of the repository's code from GitHub onto the virtual machine running the job. By specifying `ref: main`, the workflow ensures it is working on the latest code from the `main` branch, allowing it to read existing files and make new changes. 

#### Creating and Updating a File

This step executes a Bash script to manage the `test_actions.md` file and push the updated count. The script first checks if the file exists; if it doesn't, it's created with an initial rolling count of 1. If the file is found, the script uses `grep` to extract the current rolling count, increments that number by one, and uses `sed` to update the file with the new count. Finally, it configures Git user credentials, stages the modified file, creates a new commit with the message "Incremental test of Github Actions", and pushes the change back to the repository using the secured `GITHUB_TOKEN` for authentication.

#### Permissions
Github Actions will need permission to commit to your repository. This can be configured in `Settings` > `Actions` > `General`. Under `Workflow permissions`, check the read and write permissions option.
