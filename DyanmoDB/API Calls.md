## DynamoDB API Calls
- use API calls to programmatically interact with our DynamoDB table (ex. query, delete or add items)
- when using the AWS CLI to run the `get-item` command, we are interacting with the DynamoDB `GetItem` API
- users must have the correct IAM permissions to be able to execute these commands

### Commonly Used Commands
`create-table`: creates a new table
`put-item`: adds a new item or replaces an old item with a new one
`get-item`: returns a set of attributes for an item given a primary key
`update-item`: edit attributes of an existing item
`update-table`: used to modify a table
`list-tables`: list all tables in your account
`describe-table`: return information about the table
`scan`: reads every item and returns all items and attributes
`query`: query the table based on a partition key value
`delete-item`: delete an item based on its primary key
`delete-table`: delete a table including all its items

---
## Exam Tips: DynamoDB CLI Commands
- know how to use each of the common commands: CLI commands make calls to DynamoDB API
- the user making the calls must have the appropriate IAM permissions
- 