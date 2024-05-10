# DATA472 Project Git Workflow

## Project Overview

Our project, part of the DATA472-data engineering, focuses on developing microservices for both frontend and backend in the realm of data engineering. It involves utilising PostgreSQL databases and running services on AWS EC2. GitHub will serve as our primary platform for project management and version control.

## Git Repository Organization

We will establish the following repositories under our organization:

* DataPipelineService: Repository for backend microservices code related to data pipeline services.
* WebFrontendService: Repository for the web frontend service for data visualization.

## Branch Management

We will implement the following branch management strategy:

* `main`: Main branch containing stable versions. Merged from `production` branch and tagged for versioning.
* `production`: The production environment branch merged from the `development` branch.
* `development`: Integration branch for all features and fixes. Developers should create feature branches from this branch. All code submissions and merges must go through Pull Requests for code review and testing.
* `feature`: Feature branches created by developers from the development branch for specific tasks/features. Named as `feature/<feature-name>`. After development and testing, a Pull Request should be created and assigned to a code reviewer for merging into the development branch.
* hotfix: Emergency fix branch for production environment issues. Created from production branch and merged back after resolution. Also merged into the `development` branch.

## Workflow Process

### Task and Issue Management

Utilize GitHub Issues to track tasks and issues. Each task should have a clear title, description, assignees, labels, and due date. Use Projects to organize and manage tasks for effective progress tracking.

###  Feature Development

Developers should create feature branches from the development branch. Each feature should be implemented and tested on its respective branch. Small feature changes should be encapsulated in a single commit with descriptive commit messages.

###  ]Code Review and Merge

Submit a Pull Request (PR) to merge the feature branch into the development branch. At least one team member should perform code review. Upon approval, the code should be merged into the development branch.

### Deployment to Production

Once the code in the development branch is ready for release, create a release Pull Request to merge into the production branch. After thorough testing and validation, deploy the production branch to the production environment.

###  Versioning

Merge from the production branch to the main branch and tag the version to maintain version consistency and stability.

###  Emergency Fixes

For issues in the production environment, create a fixed branch from the production branch. After resolution, merge it back into both the production and development branches.

## Additional Notes

* Use meaningful commit messages for clarity and transparency in code changes.
* Ensure thorough testing to prevent the introduction of new issues or disruption of existing functionality.
* Prioritize code cleanliness and maintainability to facilitate future development and collaboration.
* Regularly synchronize the development branch with the latest changes from the main branch to avoid conflicts and ensure code consistency.
* Maintain open communication among team members to stay informed and aligned with project progress.
* Leverage GitHub features such as Issues, Projects, and Pull Requests for efficient project management and collaboration.

This workflow is tailored to our team's requirements and will facilitate effective collaboration and project development.
