# GithubActionTest
test Github Action

Intend to follow this [link](https://docs.github.com/en/actions/quickstart).

Starter Code: https://github.com/actions/starter-workflows


### Core concepts
- Main components: workflows, events, jobs, actions, runners
- Configure a GitHub Actions workflow to be triggered when an event occurs in your repository,
- A workflow is a configurable automated process that will run one or more jobs. Workflows are defined by a YAML file checked in to your repository and will run when triggered by an event in your repository, or they can be triggered manually, or at a defined schedule.
    - Reuse the workflow
        - One caller workflow can use multiple called workflows. Each called workflow is referenced in a single line.
        - The github context is always associated with the caller workflow. The called workflow is automatically granted access to `github.token` and `secrets.GITHUB_TOKEN`.
        - If you use a commit SHA when referencing the reusable workflow, you can ensure that everyone who reuses that workflow will always be using the same YAML code. However, if you reference a reusable workflow by a tag or branch, be sure that you can trust that version of the workflow.
        - Any environment variables set in an env context defined at the workflow level in the caller workflow are not propagated to the called workflow. To reuse variables in multiple workflows, set them at the organization, repository, or environment levels and reference them using the vars context.
    - Variables:
        - Variables provide a way to store and reuse non-sensitive configuration information. You can store any configuration data such as compiler flags, usernames, or server names as variables.
    - Actions:
        - Customize actions: https://docs.github.com/en/actions/creating-actions/about-custom-actions
        - Adding an action from a different repository: reference the action with the `{owner}/{repo}@{ref}` syntax
        - Referencing a container on Docker Hub: reference the action with the `docker://{image}:{tag}` syntax
            - Use the docker: https://docs.github.com/en/actions/creating-actions/creating-a-docker-container-action
- Workflow Syntax:
    - Link: https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idsteps
    - push: branch, tag, path
        - Example: Only cancel in-progress jobs or runs for the current workflow
            ```bash
            concurrency:
                group: ${{ github.workflow }}-${{ github.ref }}
                cancel-in-progress: true
            ```
    - schedule (crontab)
        ```bash
        on:
            schedule:
                - cron: '30 5 * * 1,3'
                - cron: '30 5 * * 2,4'
        ```
    - Job Dependency:
        - https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#example-requiring-successful-dependent-jobs
    - 
    
    

### Some Sample Codes
- actions/checkout@v3:
    - https://github.com/actions/checkout