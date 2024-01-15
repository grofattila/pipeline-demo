# Feature detection on faces and suspect identification

## Plan
We need to create a general roadmap of ideas and solutions to be explored and implemented.
Furthermore, we need to document resources and publication used in code to reference them later.


### Project/task management
Task/stories will be tracked as GitLab issues. Issues will be assigned to a milestone and a project board.
Milestones will be used to track progress and to plan the next iteration.
There will be 2 project boards:
    - Face features detection
    - Suspect identification
Labels can be used to distinguish between different types of issues, e.g. bug, feature, documentation, etc.

### Milestones and time/effort tracking
Time/effort will be tracked using GitLab issues and milestones.

## Design

Create architecture diagram and logical flow diagram for the data transformation, training and inference pipeline.
Tool: [draw.io](https://www.draw.io/) and embed the diagram in the README.md file.


## Implementation

### Branching strategy
We will use traditional branching strategy with a main branch and feature branches as mentioned for [git flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

<img src="https://wac-cdn.atlassian.com/dam/jcr:cc0b526e-adb7-4d45-874e-9bcea9898b4a/04%20Hotfix%20branches.svg?cdnVersion=1393" width="600" alt="gitflow">

### Code documentation
This will be enforced by the code style checker, an example is:
[](https://docs.astral.sh/ruff/rules/#pydocstyle-d)
```python
class FasterThanLightError(ZeroDivisionError):
    ...


def calculate_speed(distance: float, time: float) -> float:
    ...
```
Use instead:

```python
"""Utility functions and classes for calculating speed.

This module provides:
- FasterThanLightError: exception when FTL speed is calculated;
- calculate_speed: calculate speed given distance and time.
"""


class FasterThanLightError(ZeroDivisionError):
    ...


def calculate_speed(distance: float, time: float) -> float:
    ...


```

All commits need to belong to an issue and have a meaningful commit message. Issue number will be forced by git hooks.

### Code review
main branch is protected and requires a code review before merging.

### Code quality
Gitlab CI will run code quality checks using [Gitlab code quality tool](https://docs.gitlab.com/ee/ci/testing/code_quality.html)

### Code coverage
Gitlab CI will run code coverage checks using [Gitlab code coverage tool](https://docs.gitlab.com/ee/ci/testing/code_coverage.html)

### Code style

Code style is enforced using [black](https://black.readthedocs.io/en/stable/guides/using_black_with_other_tools.html) or 
[wemake-python-styleguide with flak8](https://gitlab.com/wemake-services/wemake-python-styleguide) or 
[ruff](https://gitlab.com/astral-sh/ruff?tab=readme-ov-file).

Code style is forced with githooks.

### Code security
We will run automated vulnerability checks GitLab CI.

### Code performance
We can measure the integration test execution time and interpolate that.

### Automation
We will use gitlab hooks to automate formatting, documentation, code quality, code coverage, code security and code performance checks.
Test dataset will be uploaded to gitlab using git lfs.
Locally code will run in docker container code, data and dependencies will be mounted as volumes.

Will have separate docker containers for training and inference.

## Test

### Unit tests
Optional but I encourage you to write unit tests for your code.

### Integration tests
We will need a small anonymised dataset to test the integration of the different components of the pipeline.

### Recording experiments
We will use wandb to record experiments. -> Tested local setup, works fine.

### Automation
We will use GitLab CI to automate the testing and running integration tests before merging to main branch.
We will also need 1 approved code review before merging to main branch.

## Deploy
We will need to have docker builds out of the box for the different components of the pipeline to be able to run them everywhere and ship it to customer.


## Maintain
TODO: add a section about how to maintain the project after delivery.
