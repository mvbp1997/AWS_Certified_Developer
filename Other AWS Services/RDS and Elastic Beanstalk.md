## Integrate RDS with Elastic Beanstalk
- Method 1: deploy RDS inside your Elastic Beanstalk environment
- Method 2: deploy RDS outside your Beanstalk environment 

### Launch RDS within Beanstalk
- launch RDS within Beanstalk console
- downside is, when you terminate the environment, your database is also terminated
- good for development and testing environments
- not good for production; lacks flexibility and rigidity

### Launch RDS outside Beanstalk
- don't use Beanstalk to create RDS
- use RDS console or CLI instead to create RDS independent of Beanstalk
- benefit of being able to tear down Beanstalk environment without terminating RDS instance
- preferred approach for production systems

### Connecting to an Outside Database
- need to add an additional security group to your environments Auto Scaling Group 
  - this will allow EC2 instances to communicate with RDS database on relevant port
- you will also need to provide connection string information to your application servers
  - you can use Beanstalk environment properties

---
## Exam Tips: RDS and Elastic Beanstalk
- two main options to connect an RDS: within your Beanstalk app and outside
- inside beanstalk is good cause its quick and easy to add your database and get started
  - downside is when Beanstalk environment is terminated then so is your RDS
  - suitable for Dev or Testing environments
- outside beanstalk is good because your RDS is independent of your Beanstalk environment
  - will need additional configuration: add security group to open RDS ports and provide connection info to your Beanstalk environment (usually RDS resource name and a reference to the database password)
  - preferred approach for Production environments