## Advanced Elastic Beanstalk

### Customizing your Elastic Beanstalk
Pre-Amazon Linux 2 environments (Amazon Linux 1): use a configuration file 
- format must be in (YAML or JSON)
- file must end with `.config` and be inside a folder called `.ebextensions` in the top-level directory of your application source
- config files can defined packages to install, create Linux uses, run shell commands, enable services, and configure load balancers 

Amazon Linux 2: use either Buildfile, Procfile and Platform hooks
- Buildfile: use for commands that run for short periods and then exit after task completion (shell commands)
  - Buildfile goes in root directory
  - format is usually key/value pairs: `<process_name>:<command>`
- Procfile: use for long-running application processes (commands to start your application)
  - create a file called Procfile in root directory 
  - format is the same as Buildfile (key/value pairs)
  - "command" in this case can be a script, however that script needs to also be part of your bundle
  - Elastic Beanstalk expects processes defined in the Procfile to run continuously, and will restart any failed processes
- Platform Hooks: is good for custom scripts or executable files that you want Beanstalk to run at a chosen stage of the EC2 provisioning process 
  - scripts are stored in dedicated directories in your app source code
  - `.platform/hooks/prebuild`: files you want Beanstalk to run before it builds, sets up, and configures the app and web servers 
  - `.platform/hooks/predeploy`: files you want to run after it sets up and configures the application and web server but BEFORE it deploys them to the final runtime location 
  - `.platform/hooks/postdeploy`: files that run AFTER Beanstalk deploys the application

---
## Exam Tips: Advanced Elastic Beanstalk
We have many options for customizing your Elastic Beanstalk environment
- The `.ebextensions` folder: strictly for Amazon Linux 1
  - this directory needs to be in root 
  - files must end with `.config`
- Buildfile: use for short commands that terminate upon completion (shell scripts)
  - Buildfile needs to go in root directory
- Procfile: use for long running processes (i.e. commands to start application)
  - Procfile needs to be in root directory
- Platform Hooks: use for custom scripts or executables that run at various stages when EC2 is provisioned
  - we have `.platform/hooks/prebuild | predeploy | postdeploy`

---
## Migrating Applications to Elastic Beanstalk
- if you want to migrate an existing application with minimal to no changes to the application: use the Migration Assistance Tool
- specifically for .NET users in a Windows Server environment use the `.NET Migration Assistant`
  - an interactive PowerShell Utility that enables your to migrate your entire .NET app into Elastic Beanstalk
- This tool is opensource and is available online

---
### Exam Tips: Migrating Apps to Elastic Beanstalk
- for .NET applications, use the .NET Migration Assistant
  - an open-source, interactive PowerShell utility 