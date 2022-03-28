## CodeArtifact
- artifact repository for developers to find the software packages (and versions) they need
- securely store, publish and share artifacts related to your app
- a package = bundle of software
- software can be in-house or open-sourced 
- integrates well with public repositories as well
  - ex. NPM registry, Python Package index, Maven Central
- integrates well with CI/CD systems as well (ex. CodeBuild)

### Artifacts?
More than just Software
- documentation
- compiled applications
- deployable package 
- libraries

### CodeArtifact Integration with Public Repositories
Makes third-party software available to use from one location
- IT leaders within your org can manage public repositories packages and can approve changes
- manage which packages and versions our org is willing to support 
- increases efficiency: 
  - find all approved packages in one location
  - can also publish and share their own

### Integrating CodeArtifact with Public Repositories
- Step 1: create a CodeArtifact Domain
  - a domain is where you will group code artifacts in order to manage them
- Step 2: create a repository within the Domain
- Step 3: create an upstream repository 
- Step 4: add external connection to a public repository pointing to upstream repository 
  - allows CodeArtifact to pull packages
  - packages are encrypted in transit
- Step 5: associate the repo with the upstream repo
  - this will allow developers to pull from that repo

---
## Exam Tips: CodeArtifact
- CodeArtifact is an artifact repo that makes it easy for developers to find the software packages they need 
  - package = bundle of software used in your app
- enables developers to find approved packages and can also publish their own
- enables developers to create an upstream repository with an external connection to pull packages from an external public repository (making them available in the orgs private repo)
