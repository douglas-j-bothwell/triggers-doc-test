- [Webhook Triggers](https://douglas-j-bothwell.github.io/triggers-doc-test)
  - [Define a Webhook Trigger](https://douglas-j-bothwell.github.io/triggers-doc-test/define-a-webhook-trigger)
  - [Webhook Trigger Configuration](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-configuration)
  - [Webhook Trigger Conditions](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-conditions)
  - [Webhook Trigger Expressions and Operators](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-expressions)
	- [Webhook Trigger Inputs](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-inputs)


# Webhook Trigger Inputs


Runtime Inputs for the Trigger to use, such as Harness Service and artifact.

You can use the [Built-in Git Payload Expressions](#built_in_git_trigger_and_payload_expressions) and JEXL expressions in this setting.

See [Run Pipelines using Input Sets and Overlays](/article/gfk52g74xt-run-pipelines-using-input-sets-and-overlays).

Topics discussed:
<!-- TOC depthFrom:3 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Webhook](#webhook)
- [Git Events Automatically Registered with Webhooks](#git-events-automatically-registered-with-webhooks)
		- [GitHub](#github)
- [GitLab](#gitlab)
- [Bitbucket Cloud](#bitbucket-cloud)
- [Bitbucket Server](#bitbucket-server)

<!-- /TOC -->

### Webhook

For all Git providers supported by Harness, the Webhook is created in the repo automatically. You don't need to copy it and add it to your repo webhooks.

### Git Events Automatically Registered with Webhooks

The following Git events are automatically added to the webhooks Harness registers.

##### GitHub

[GitHub events](https://docs.github.com/en/developers/webhooks-and-events/webhooks/webhook-events-and-payloads):

*   `create`
*   `push`
*   `delete`
*   `deployment`
*   `pull_request`
*   `pull_request_review`

### GitLab

[GitLab events](https://docs.gitlab.com/ee/user/project/integrations/webhooks.html):

*   Comment events
*   Issue events
*   Merge request events
*   Push events

### Bitbucket Cloud

[Bitbucket Cloud events](https://support.atlassian.com/bitbucket-cloud/docs/event-payloads/):

*   `issue`
*   `pull request`

### Bitbucket Server

[Bitbucket Server events](https://confluence.atlassian.com/bitbucketserver/event-payload-938025882.html):

*   Pull requests
*   Branch push tag