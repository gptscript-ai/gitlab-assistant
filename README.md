# GitLab API Assistant

Initial work on a GitLab assistant. Only tested against GPT-4o and the public GitLab instance.

## Overview

This is a GitLab Assistant that can interact with the public GitLab instance. It currently provides agents to work with projects, repositories, and merge_requests. It leverages the openapi.yaml spec in this repository to build out the assistant with each Agent having a set of tools to interact with the resource in the GitLab API.

## Pre-requisites

You will need a PAT (Personal Access Token) from GitLab to interact with the API. You can create one by following the instructions [here](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html).

## Getting Started

To get started you can run the following command:

```bash
gptscript github.com/cloudnautique/gitlab-assistant
```

You will be prompted for an OpenAI API key and a GitLab Personal Access Token.

## Capabilities

The GitLab Assistant can interact with the following resources:

### GitLab Agent

- **Main entrypoint for GitLab Agent**: Understands all things GitLab, source control, CI/CD, and general DevOps best practices.

### Pipelines

- **Operations related to pipelines**: Creating, listing, updating, and deleting pipelines and jobs in GitLab.

### Projects

- **Operations related to projects**: Creating, listing, updating, and deleting projects in GitLab. Does not cover all things projects.

### Repositories

- **Operations related to repositories**: Creating, listing, updating, and deleting repositories in GitLab. This also provides access to branches etc.

### Merge Requests

- **Operations related to merge requests**: Creating, listing, updating, and deleting merge requests in GitLab. You can also comment, close, merge and check the status of the builds/pipelines.

## Adding a new Agent

When adding a new agent, you should leverage the existing `context.gpt` and create a new file.

Tools should be a subset and focus on a single resource because there are to many endpoints to cover in a single agent.

```
Name: New Agent
Description: Interact with XYZ in GitLab
Context: context.gpt
Tools: *resources* from openapi.yaml
Chat: true

Handle the users requests for XYZ in gitlab
```

## Private GitLab Instance

You will need to edit the `openapi.yaml` spec and adjust the host section to point to your private GitLab instance.

```yaml
...
schemes:
- https
host: gitlab.com
...
```
