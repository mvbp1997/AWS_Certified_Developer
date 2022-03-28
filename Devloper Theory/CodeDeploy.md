---
## CodeDeploy
- automated deployment that works with EC2 instances, on-prem and lambda
- deployment approaches:
  - In-Place: the application is stopped on each instance and the new release is installed (rolling update)
  - Blue/Green: new instances are provisioned and the new release is installed on them

- new versions in CodeDeploy are known as "Revisions"

### In-Place Deployment 
- application is stopped on each instance (one after another) while deployment is in progress
- similar to Rolling updates for Beanstalk, capacity is reduced
- you should configure your load balancer to stop sending requests to that instance (configurable on CodeDeploy)
- How to Rollback: you'll need to re-deploy the previous version which can be time consuming

### Blue/Green Deployment
- blue represents the active/current deployment 
- green represents the new release environment (completely independent from blue environment)
- Revision is deployed on Green, then registered on the load balancer
- traffic is routed away from the old environment
- once green has satisfied all the checks, we terminate the blue environment
- rollback strategy: just set the load balancer back to blue environment

### Exam Tips - CodeDeploy 101
- In-Place
  - capacity is reduced during deployment
  - Lambda is NOT supported
  - Rolling back involves re-deployment
  - Great when deploying for the first time
- Blue/Green
  - no capacity reduction (safest option for production environment)
  - green instances created independent of blue instances
  - easy to switch (rollback) between old and new 
  - drawback is you pay for the 2 environments until you terminate the old servers

---
## CodeDeploy AppSpec File
- AppSpec is the configuration file used to define the parameters to be used during deployment
- YAML format: for EC2 and on-prem systems only 
- YAML and JSON format: for Lambda and/or EC2 and on-prem
- keep the `appspec.yml` file in the root of the directory
  - `/scripts`, `/config`, `/source` directories can also go on root

### EC2 AppSpec File
- version (reserved for future use): currently only value is 0.0
- os: operating system you are deploying to
- files: cconfig files, application files, and packages and where they should be copied to
- hooks (lifecycle events): scripts that run at set points in the deployment; hooks run in a very specific order

### Scripts you can run during deployment
- uzip files: unzip app files prior to deployment
- test files: run functional tests on a newly deployed application
- load balancer config files: de-register and re-register instances with load balancer 

### Exam Tips - AppSpec File
- configuration file that defines parameters used by CodeDeploy (OS, files, hooks, etc.)
- the `appspec.yml` file should be found in the root of the directory
- hooks: lifecycle events have a very specific run order

---
## CodeDeploy LifeCycle Event Hooks
- event hooks run in a specific order (known as the Run Order)

### Phase 1 - De-register instances from a Load Balancer
- BeforeBlockTraffic: all tasks you want to run on instances before they are de-registered from LB
- BlockTraffic: actually de-register instance from a LB
- AfterBlockTraffic: any tasks you want to run on instances after they are de-registered

### Phase 2 - Application Deployment
- ApplicationStop: gracefully stop the application
- DownloadBundle: CodeDeploy agent copies the application revision files (from Git) to a temp location
- BeforeInstall: pre-installation scripts (i.e. backup, decrypt files, etc.)
- Install: scripts relating to copying application files to final location
- AfterInstall: post-installation script (i.e. updating config files and permissions)
- ApplicationStart: start any services that were stopped during ApplicationStop
- ValidateService: run any test scripts to validate the service is working as expected

### Phase 3 - Re-register instances with Load Balancer
- BeforeAllowTraffic: any tasks you want to run on instances before they are registered to LB
- AllowTraffic: register instances to LB
- AfterAllowTraffic: tasks you want to run after instances are registered with LB

### Exam Tips - Lifecycle Event Hooks for In-Place Deployments
- run order: event hooks are run in a specific order 
- in-place deployment has three phases: de-register from LB, app install, re-register to LB
- remember the order in which event hooks execute

---
### Code Deploy Demo
- service roll for CodeDeploy: to allow CodeDeploy to make API calls on our behalf and install the application
