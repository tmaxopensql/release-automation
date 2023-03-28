# Release Automation
This repository contains github action for release automation.

## Overview
<p align="center">
<img
    src="/overview.png"
    alt="Release Automation Overview"
    style="display: inline-block; margin: 0 auto; width: 640px"
/>
</p>

The release automation goes through the following process:
- Pull request is created by a developer with one of the following branch name prefixes (if not, the pull request is blocked by the required check):
    - release/**
    - feature/**
    - hotfix/**
    - patch/**
    - gh-action/**
- After reviewing the pull request, the source code admin will accept and close the pull request
- Upon closing the pull request, release automation workflow is triggered
- The workflow will determine which version (major, minor, patch, or none) must be updated by examining the prefix of the branch name
- With the new version, a release tag is created with a release note generated from the pull request message

NOTE: The release automation workflow is provided as a starter workflow. You can easily add this workflow to your repository using the pre-made workflow template (starter workflow is not provided for private repositories)

<p align="center">
<img
    src="/starter_workflow.png"
    alt="Starter Workflow"
    style="display: inline-block; margin: 0 auto; width: 640px"
/>
</p>

## OpenSQL Branch Policy
<p align="center">
<img
    src="/branch_policy.png"
    alt="branch_policy"
    style="display: inline-block; margin: 0 auto; width: 640px"
/>
</p>

You must use specific branch name prefix for your pull request. Here are the prefixes and their rules.

- "release"
    - This branch name prefix is used for new release of the product
    - The naming format must be "release/\[new version\]"
    - Once this branch is merged to the main branch, the major version is updated and a stable branch is automatically created with the previous major version
- "feature"
    - This branch name prefix is used for new feature implementation
    - The naming format must be "feature/\[new feature name\]"
    - Once this branch is merged to the main branch, the minor version is updated
- "hotfix"
    - This branch name prefix is used for fixing critical security-related issues
    - The naming format must be "hotfix/\[the issue detail\]"
    - Once this branch is merged to the main branch, the minor version is updated
- "patch"
    - This branch name prefix is used for fixing bugs
    - The naming format must be "feature/\[the fix detail\]"
    - Once this branch is merged to the main branch, the patch version is updated
- The following are the exceptions that will be accepted for pull request but will not create a new release
    - "gh-action"
- Any other branch name prefix will be blocked by the required checks

## OpenSQL Version Policy
### Semantic Versioning
- We follow [semantic versioning](https://semver.org/) with a slight customization
```
    □    .    ■    .    ◆
  Major     Minor     Patch
```
- Minor becomes 0 when Major version has changed
- Patch becomes 0 when Minor version has changed
- Version must change incrementally (ex. 1.0.1 -> 1.0.2 -> 1.0.3 -> 1.1.0)

### Major Version
- At first, the major version is set to be 0, indicating that the project is at pre-released initial stage
- After the project is thought to be ready for public production stage, the major version is set to be 1
- Products with the same major version must be compatible with each other
- Major version must change when: 
  - the project reached public production stage level
  - a newly added feature is not compatible with the current major version
  - a significant changes in architecture cause incompatibility

### Minor Version
- Minor version must change when:
  - critical errors like undefined behavior or abnormal crash have been fixed
  - a supplementary fixes have been added following a newly added features
  - a new feature that is compatible with the current minor version has been added
  - a performance enhancement has been added

### Patch Version
- Patch version must change when: 
  - a fix to non-critical bugs has been added
  - a fix to dependency versions has been added
  - a fix to README.md has been added
  - a fix to tests or test framework has been added
  - a simple refactoring has been added
