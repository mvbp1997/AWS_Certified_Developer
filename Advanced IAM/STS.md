## STS with AssumeRoleWithWebIdentity
- STS: security token service
- STS API: assume-role-with-web-identity is an API provided by STS
  - returns temporary credentials for users authenticated by a mobile or web app or using a web ID provider
- Web Apps can use STS API
- Mobile apps recommended to use Cognito

### STS Workflow
- user authenticates with webID provider (Facebook, Google, Amazon, etc.)
- webId provider returns JWT token
- app makes an `assume-role-with-web-identity` call to STS and provides the JWT token
- STS returns temporary AWS credentials (access and secret access keys)
- app can use creds to access AWS resources

### STS Response
- `AssumedRoleUser`: ARN identifiers that can be used to refer to the credentials programmatically
  - `AssumedRoleId`: is the actual ID
- `Credentials`: contains the access and secret access key

## Exam Tips
- STS: part of the security token service
- authentication: allows users who have authenticated with web identity providers to access AWS resources
- API call: after the user has authenticated, the app makes the `assume-role-with-web-identity` API call
- STS API returns temporary AWS credentials 
- `AssumedRoleUser`
  - the Arn and the AssumedRoleID are used to programmatically reference the temporary credentials
