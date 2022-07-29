# How to Model Your Gitops Environments

This is a very simple web application that gets configuration from environment variables and prints them out. You might want to see the [deployment repository as well.](https://github.com/JavadZahrabi/gitops-environment-promotion_02)

This sample project is deliberately simplified to illustrate the core concepts, events and issues. It is a fictitious cloud-native microservice project that uses the Scrum approach model.

The cloud infrastructure in this scenario consists of a Kubernetes cluster. Three environments are deployed on the cluster for the microservice -- DEV, STAGING and PROD. The DEV environment is used to develop and test new features internally by the development team. The STAGING environment is used as the production environment for integrating new features into a release candidate within a sprint, and is also used for review by the product owner. PROD is the production environment for the end users. Only the Product Owner or the DevOps role with the approval of the Product Owner may access the PROD environment and make changes. For example, releasing a new version.


![Project Process](./documentation/Master_thesis_project_process.png?raw=true "Project Process")

The project uses Git to manage the source code of the microservice. The branching strategy is simplified here to keep the complexity of this example low. The main branch always contains a runnable state of the application and serves as the basis for release candidates. For each user story, a feature branch is created on which development takes place. The feature branch is merged with the main branch via a pull request as soon as the Definition of Done (DoD) is fulfilled and the user story is considered complete. An internal review in the development team is part of the DoD and is triggered when the pull request is created.

Git events include the push to the main branch, which occurs via the merge of the feature branch pull request, as well as the merges of the "Deploy to STAGING" and "Deploy to PROD" pull requests. When a feature-Branch pull request is merged, the CI pipeline creates a release candidate artifact that is then automatically deployed to the DEV environment by the CD. The artifact is a Docker image containing the compiled application. Als Docker Image Tag wird die Release Version verwendet. Releases are uniquely versioned using the scheme YYY-MM-DD-Short Commit Hash, e.g. "2022-06-12-858cc39".

The deployment to STAGING and PROD is done by a manual trigger. The "Deploy to STAGING" and "Deploy to PROD" pull request merge events are used for this purpose. Only the PO or the DevOps role is allowed to merge these two pull requests.

test changed repo name
