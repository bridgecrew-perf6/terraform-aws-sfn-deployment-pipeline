# terraform-aws-sfn-deployment-pipeline
This Terraform module creates a Continuous Deployment (CD) pipeline using AWS Step Functions.

The pipeline deploys to the `test`, `stage` and `service` accounts in parallel, and deploys to `prod` only if all previous states have passed. The module allows you to create pipelines consisting of different combinations of accounts, with the only requirement being that at least one account is being deployed to. See examples below.

The module additionally allows you to add an arbitrary number of _post-deployment_ states to the pipeline -- that is, states that will be run after a successful deployment to `test`, `stage` or `prod`. These states will spin up a containers with a user-defined image, command and S3 content. Examples of such states are:
- An `Integration Tests` state after a successful deployment to stage.
- A `Smoke Tests` state after a successful deployment to prod.
- ...


## Testing
The Terraform files are separated into different files to make it easy to test the generation of the JSON state machine definition without actually provisioning any AWS resources.

The tests are run in parallel across different Terraform versions.


## Pipeline Examples
Single Account | Test, Stage & Prod Accounts | All Accounts | All Accounts w/Post-Deployment States
:-------------------------:|:-------------------------:|:------------------------:|:-------------------------:
![](docs/single_account_pipeline.png)  |   ![](docs/non_service_pipeline.png)  |  ![](docs/pipeline.png)  | ![](docs/pipeline_custom_states.png)
