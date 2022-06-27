- [Webhook Triggers](https://douglas-j-bothwell.github.io/triggers-doc-test)
  - [Define a Webhook Trigger](https://douglas-j-bothwell.github.io/triggers-doc-test/define-a-webhook-trigger)
  - Webhook Trigger Configuration
  - [Webhook Trigger Conditions](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-conditions)
  - [Webhook Trigger Expressions and Operators](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-expressions)
  - [Webhook Trigger Inputs](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-inputs)


# Webhook Trigger Configuration

This topic describes the Configuration Tab of the Webhook Trigger setup wizard. 

For steps on setting up different types of Triggers, see [Triggers Howtos](/category/oya6qhmmaw-trigger-category).


* **Name** The unique name for the Trigger.

* **ID

See [Entity Identifier Reference](/article/li0my8tcz3-entity-identifier-reference).

* **Description** Text string.

* **Tags** See [Tags Reference](/article/i8t053o0sq-tags-reference).

* **Payload Type** Git providers, such as GitHub, Bitbucket, and GitLab.

* **Custom Payload type** To use a custom payload type, copy the secure token and add it to your custom Git provider. Whenever you regenerate a secure token, any preceding tokens become invalid. Update your Git provider with the new token.

* **Connector** Select the Code Repo Connector that connects to your Git provider account. See [Code Repo Connectors Tech Ref](/category/xyexvcc206-ref-source-repo-provider).

* **Repository Name** Enter the name of the repo in the account.

* **Event and Actions** Select the Git events and actions that will initiate the Trigger.

## Git Events and Actions 

Harness uses your Harness account Id to map incoming events. Harness takes the incoming event and compares it to ALL triggers in the account.

You can see the event Id that Harness mapped to a Trigger in the Webhook's event response body `data`:

`{"status":"SUCCESS","data":"60da52882dc492490c30649e","metaData":null,...`

Harness maps the success status, execution Id, and other information to this event Id.

||||
|--- |--- |--- |
|Payload Type|Event|Action|
|Github|Pull Request|Closed|
|||Edited|
|||Labeled|
|||Opened|
|||Reopened|
|||Synchronized|
|||Unassigned|
|||UnLabeled|
||Push|n/a|
||Issue Comment Only comments on a pull request are supported.|Created|
|||Deleted|
|||Edited|
|GitLab|Push|N/A|
||Merge Request|Sync|
|||Open|
|||Close|
|||Reopen|
|||Merge|
|||Update|
|Bitbucket|On Pull Request|Pull Request Created|
|||Pull Request Merged|
|||Pull Request Declined|
||Push||

