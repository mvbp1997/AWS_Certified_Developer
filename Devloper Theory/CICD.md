## CICD
- Software Development best practice
- Continuous Integration, Continuous Delivery / Deployment
- make small changes and automate everything!
- automation: fast, repeatable, scalable, enabling rapid deployment

### AWS Developer Tools
- CodeCommit: source control service 
  - enabling teams to collaborate on code, html pages, scripts, images, binaries, etc (fully managed Git repository)
- CodeBuild: fully automated build service
  - compiles source code, runs tests and produces packages that are ready to deploy
- CodeDeploy: automated deployments 
  - to any instance including EC2, Lambda, and on-prem
- CodePipeline: workflow management
  - end-to-end solution, build, test and deploy your application every time there is a change

---
## Exam Tips
- Continuous Integration: merging new code changes frequently (think CodeCommit)
- Continuous Delivery: automating the build, test and deployment functions (CodeBuild and CodeDeploy)
- Continuous Deployment: fully managed release process to production (CodePipeline)
- AWS Whitepaper: practicing CICD on AWS
  - explains the features and benefits of using CICD and AWS tooling in your software development environment

