## Step Functions
- visual interface for serverless applications, which enables you to build, and run serverless applications as a series of steps
- each step in your app executes in order, as defined by business logic
- output of one step can act as input of other step
- step functions: orchestration for serverless applications

### Orchestration for Serverless Apps
- manage the logic of your app
- including sequencing, error handling, retry logic, execution order, etc.
- step functions consist of state machines and tasks
  - tasks = single unit of work, what to do; usually executed in a Lambda
  - state machine = workflow, consisting of multiple tasks

---
## Exam Tips: Step Functions
- great way to visualize serverless applications
- step functions automatically trigger and track each step in sequence flow; output of one can be input of next
- step functions log state of each step, so if something goes wrong you can track what went wrong and where

---
## Comparing Step Function Workflows
- step functions provide various types of state machines that feature different workflows
- kind of tasks you want to orchestrate will determine what workflow you should use

### Standard Workflows
- good for long-running, durable, and auditable workflows that may run for up to a year
- full execution history available for 90 days
- at-most-once work model: tasks are never executed more than once unless you explicitly specify retry actions
- designed for non-idempotent actions (ex. processing payments should only process once)
  - request is non-idempotent if it always causes a change in state 
  - (ex. sending an email multiple times causes a change in state because you end up with multiple emails in your inbox)

### Express Workflows
- good for short-lived, high-volume, event-processing-type workloads
  - up to 5 minutes 
- at-least-once model: ideal if there is a possibility that an execution might run more than once or require multiple concurrent executions
- good for idempotent actions (ex. transforming input data and storing the result in DynamoDB)
  - request is idempotent if an identical request can be made once or several times in a row with no additional side effects 
  - (ex. reading data from a database or S3 bucket)
- 2 different types of Express Workflows: synchronous and asynchronous

### Synchronous vs Asynchronous Express Workflow
- Synchronous
  - begin workflow
  - wait till workflow completes
  - returns result
  - great for operations that are performed one at a time (workflow must complete before next step begins
- Asynchronous
  - begins workflow
  - confirms workflow has started
  - result of workflow can be found in CloudWatch logs (not waiting for workflow to complete)
  - great for services or operations that don't depend on the completion and result of your workflow


---
## Exam Tips: Step Function Workflows
- understand the differences between workflows
- standard workflows:
  - long-running (up to 1 year)
  - at-most-once
  - non-idempotent (always cause a change in state, ex. payment processing)
- express workflows: 
  - short-lives (up to 5 minutes)
  - at-least-once
  - idempotent (multiple identical requests will not yield additional side effects, ex. reading a database)
- synchronous express workflows:
  - workflow must complete before next step can begin (ex. confirm payment before sending order)
- asynchronous express workflows:
  - other tasks are not dependent on the completion of the workflow (ex. messaging system)

