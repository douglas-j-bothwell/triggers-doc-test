- [Webhook Triggers](https://douglas-j-bothwell.github.io/triggers-doc-test)
  - [Define a Webhook Trigger](https://douglas-j-bothwell.github.io/triggers-doc-test/define-a-webhook-trigger)
  - [Webhook Trigger Configuration](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-configuration)
  - [Webhook Trigger Conditions](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-conditions)
  - [Webhook Trigger Expressions and Operators](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-expressions)
	- [Webhook Trigger Inputs](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-inputs)


# Define a Webhook Trigger

A *webhook trigger* listens on a webhook and starts a Pipeline Build when a matching event arrives. You can set up Triggers based on header fields, body fields, pull requests, and so on. Triggers enable event-driven CI/CD and support the practice of every commit building and/or deploying to a target environment.

## Limitations

*   Currently, Harness supports Git-based Triggers for the most common Git providers. Harness includes a Custom Trigger for other repo providers.
*   The **IN** and **NOT IN** operators do not support Regex.
*   In Harness, you can select who is able to create and use Triggers within Harness, but you must use your repos' RBAC to control who can initiate the Git events that start the Harness Trigger.


## Before You Begin

To complete this workflow, you must have the following:

* A CI Pipeline with a Build Stage and a Codebase.

* A Build Infrastructure with a Harness Delegate installed (if you're using an on-prem build infrastructure).

* A Codebase Connector with API Access enabled.

* A Personal Access Token with the following permissions: 

   * **GitHub —** A Personal Access Token with the **repo**, **user**, and **admin:repo_hook** scope enabled. You should also be repo admin.
   
   * **Gitlab —** A Personal Access Token with the **api**, **read_repository**, **write_repository** permissions enabled. 
   
   * **AWS CodeCommit —** AWS access key. TBD Permissions? 

   * **Bitbucket —** ???
   

## Define the Trigger

1) In the Pipeline Studio, go to the CI Pipeline where you want to define the Trigger.

2) Choose **Triggers** > **+ New Trigger** and select ond one of the webhook triggers such as GitHub. The New Webhook setup wizard appears.

3) Set up the Trigger as described in:



## Test the Trigger

Make a change on the repo and see if it executes the Trigger. For example, change a file, commit it on a branch, and make a pull request.

In your Git provider repo, you can see that the request and response were successful.

![](https://files.helpdocs.io/i5nl071jo5/articles/hndnde8usz/1614104307757/image.png)

In Harness, view the Pipeline execution.

In Harness CI, click **Builds**.

You can see the source and target branches. You can also see the pull request comment and number.

![](https://files.helpdocs.io/i5nl071jo5/articles/hndnde8usz/1614104376860/image.png)

Click the pull request number and it opens the Git provider repo at the pull request.

If you open the Trigger in the Pipeline you will see a status in **Last Activation Details**.

![](https://files.helpdocs.io/i5nl071jo5/articles/hndnde8usz/1624922961169/clean-shot-2021-06-28-at-16-29-13.png)

Activation means the Trigger was able to request Pipeline execution. It does not mean that the Webhook didn't work.

  

