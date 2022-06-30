- Define a Webhook Trigger
  - [Webhook Trigger Configuration](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-configuration)
  - [Webhook Trigger Conditions](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-conditions)
  - [Webhook Trigger Expressions and Operators](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-expressions)
  - [Webhook Trigger Inputs](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-inputs)


# Define a Webhook Trigger

You can define a *webhook trigger* that listens on a webhook and starts a CI Pipeline Build when a matching Git event arrives. You can set up Trigger filters and expressions based on any elements in a Git header or payload: commits, branches, pull requests, tags, updates to specific files, and so on. 

All conditions in a Trigger are ANDed together into one filter, so an event must match all conditions for a Trigger to start a Build. You can define multiple Triggers for a Pipeline that address specific use cases. You can also use [JEXL expressions](https://commons.apache.org/proper/commons-jexl/reference/syntax.html) to define complex, targeted filters. All [JexlOperator](https://commons.apache.org/proper/commons-jexl/apidocs/org/apache/commons/jexl3/JexlOperator.html) constants, methods, and operators are supported.

Harness supports many different types of Triggers for both CI and CD workflows. Triggers support the practice of every commit automatically building and/or deploying to a target environment. See [Triggers](https://ngdocs.harness.io/category/oya6qhmmaw).

##### Watch a Video
<details>
  <summary>Click to expand</summary>
  
  This video shows how you can create and run a Trigger in response to Git events.
  <iframe  width="640"  height="480" src="https://www.youtube.com/embed/y8s351IJLXw"  frameborder="0" allow="autoplay; encrypted-media" allowfullscreen> </iframe>
  
</details>

##### Table of contents

  - [Important Notes](#important-notes)
  - [Before You Begin](#before-you-begin)
  - [Define the Trigger](#define-the-trigger)
    - [Webhook Trigger Configuration](#webhook-trigger-configuration)
      - [Webhook Trigger Configuration](#webhook-trigger-configuration)
      - [Git Events and Actions](#git-events-and-actions)
    - [Webhook Trigger Conditions](#webhook-trigger-conditions)
      - [Webhook Trigger Conditions](#webhook-trigger-conditions)
      - [Table of contents](#table-of-contents)
      - [Conditions are ANDs](#conditions-are-ands)
      - [Source and Target Branch](#source-and-target-branch)
      - [Header Conditions](#header-conditions)
      - [Payload Conditions](#payload-conditions)
      - [Referencing Payload Fields](#referencing-payload-fields)
    - [Webhook Trigger Expressions and Operators](#webhook-trigger-expressions-and-operators)
      - [Webhook Trigger Expressions and Operators](#webhook-trigger-expressions-and-operators)
      - [Table of contents](#table-of-contents)
      - [Built-in Git Trigger and Payload Expressions](#built-in-git-trigger-and-payload-expressions)
      - [Main Expressions](#main-expressions)
      - [PR and Issue Comment Expressions](#pr-and-issue-comment-expressions)
      - [Push Expressions](#push-expressions)
      - [JEXL Expressions](#jexl-expressions)
      - [Operators](#operators)
    - [Webhook Trigger Inputs](#webhook-trigger-inputs)
      - [Webhook Trigger Inputs](#webhook-trigger-inputs)
      - [Table of contents](#table-of-contents)
      - [Webhook](#webhook)
    - [Git Events Automatically Registered with Webhooks](#git-events-automatically-registered-with-webhooks)
      - [GitHub](#github)
      - [GitLab](#gitlab)
      - [Bitbucket Cloud](#bitbucket-cloud)
      - [Bitbucket Server](#bitbucket-server)
  - [Test the Trigger](#test-the-trigger)
  - [See Also](#see-also)


## Important Notes

*   Currently, Harness supports Git-based Triggers for the most common Git providers. Harness includes a Custom Trigger for other repo providers.
*   The **IN** and **NOT IN** operators do not support Regex.
*   In Harness, you can select who is able to create and use Triggers within Harness, but you must use your repos' RBAC to control who can initiate the Git events that start the Harness Trigger.


## Before You Begin

To complete this workflow, you must have the following:

* A [CI Pipeline](https://ngdocs.harness.io/article/x0d77ktjw8-ci-pipeline-quickstart) with a [Build Stage](https://ngdocs.harness.io/article/yn4x8vzw3q-ci-stage-settings) and a [Codebase](https://ngdocs.harness.io/article/mozd8b49td-create-and-configure-a-codebase).

* A [Build Infrastructure](https://ngdocs.harness.io/category/rg8mrhqm95-set-up-build-infrastructure) with a Harness Delegate installed (if you're using an on-prem build infrastructure).

* A Codebase Connector to your Git Saas provider.

   * The Connector needs to have API Access enabled. 
   
   * Your Connector also requires a token, password, or key with the following permissions: 

      - **[GitHub Connector](https://ngdocs.harness.io/article/v9sigwjlgo) —** A Personal Access Token with the **repo**, **user**, and **admin:repo_hook** scope enabled. You should also be repo admin.
   
      - **[Gitlab Connector](https://ngdocs.harness.io/article/5abnoghjgo) —** A Personal Access Token with the **api**, **read_repository**, **write_repository** permissions enabled. 
   
      - **[AWS CodeCommit Connector](https://ngdocs.harness.io/article/jed9he2i45) —** AWS Access Key and Secret Key. 

      - **[Bitbucket Connector](https://ngdocs.harness.io/article/iz5tucdwyu) —** An App Password with the following permissions: **Pull Requests: Write**, **Issues:Read**, and **Webhooks:Read and write**.
   

## Define the Trigger

  1) In the Pipeline Studio, go to the CI Pipeline where you want to define the Trigger.

  2) Choose **Triggers** > **+ New Trigger** and select ond one of the webhook triggers such as GitHub. The New Webhook setup wizard appears.

  3) The New Webhook setup wizard has three tabs: Configure, Conditions, and Pipeline Inputs. Set up the Trigger as described in in the following sections:

   - [Webhook Trigger Configuration](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-configuration)
   - [Webhook Trigger Conditions](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-conditions)
   - [Webhook Trigger Expressions and Operators](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-expressions-and-operators)
   - [Webhook Trigger Configuration](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-inputs)
     
  4) Save and test the filter as described below.
 
  
###  Webhook Trigger Configuration
<details>
    <summary>Click to expand</summary>
 

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


**Git Events and Actions** 

Harness uses your Harness account Id to map incoming events. Harness takes the incoming event and compares it to ALL triggers in the account.

You can see the event Id that Harness mapped to a Trigger in the Webhook's event response body `data`:

`{"status":"SUCCESS","data":"60da52882dc492490c30649e","metaData":null,...`

Harness maps the success status, execution Id, and other information to this event Id.


  
||||
|--- |--- |--- |
|<b>Payload Type</b>|<b>Event</b>|<b>Action</b>|
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



 </details>


###  Webhook Trigger Conditions
 <details>
     <summary>Click to expand</summary>

    #### Webhook Trigger Conditions

    This topic describes how to define the conditions that cause a Webhook Trigger to start a build. Harness triggers are highly configurable and flexible. For example, you can trigger builds based on specific header values, payload values, tag conventions, and changes in specific files or Pull Requests. 

    #### Table of contents

    - [Conditions are ANDs](#conditions-are-ands)
    - [Source and Target Branch](#source-and-target-branch)
    - [Header Conditions](#header-conditions)
    - [Payload Conditions](#payload-conditions)
    - [Referencing Payload Fields](#referencing-payload-fields)

    #### Conditions are ANDs

    You can think of each Trigger as a complex filter in which all Conditions are `AND`\-ed together. To execute a Trigger, the event payload must match all Conditions in the Trigger.

    ![](https://files.helpdocs.io/i5nl071jo5/articles/rset0jry8q/1624924312486/clean-shot-2021-06-28-at-16-51-34.png)

    In this example, an event must match all conditions under **Source Branch**, **Target Branch**, **Header Conditions**, **Payload Conditions**, and **JEXL Conditions** for the Trigger to be filtered.

    To use `OR`, `NOT`, or other operators across the payload, use a **JEXL Condition** and leave the rest empty.

    The JEXL `in` operator is not supported in **JEXL Condition**.

    #### Source and Target Branch

    The source and target branches of the Git merge that must be matched.

    These are available depending on the type of event selected. Any event that belongs to a merge will have Source Branch and Target Branch conditions.

    For example:

    *   Source Branch starts with `new-`
    *   Target Branch equals `main`

    ![](https://files.helpdocs.io/i5nl071jo5/articles/rset0jry8q/1613776102338/image.png)

    #### Header Conditions

    Valid JSON cannot contain a dash (–), but headers are not JSON strings and often contain dashes. For example, X-Github-Event, content-type:

    Request URL: https://app.harness.io:  
    Request method: POST  
    Accept: \*/\*  
    content-type: application/json  
    User-Agent: GitHub-Hookshot/0601016  
    X-GitHub-Delivery: be493900-000-11eb-000-000  
    X-GitHub-Event: create  
    X-GitHub-Hook-ID: 281868907  
    X-GitHub-Hook-Installation-Target-ID: 250384642  
    X-GitHub-Hook-Installation-Target-Type: repository

    The header expression format is `<+trigger.header['key-name']>`. For example. `<+trigger.header['X-GitHub-Event']>`.

    ![](https://files.helpdocs.io/i5nl071jo5/articles/hndnde8usz/1624919275031/clean-shot-2021-06-28-at-15-27-08.png)

    If the header key doesn't contain a dash (`–`), then the format `<+trigger.header.['key name']>` will work also.

    When Harness evaluates the header key you enter, the comparison is case insensitive.

    In **Matches Value**, you can enter multiple values separated by commas and use wildcards.

    #### Payload Conditions

    Conditions based on the values of the JSON payload. Harness treats the JSON payload as a data model and parses the payload and listens for events on a JSON payload key.

    To reference payload values, you use `<+eventPayload.` followed by the path to the key name.

    For example, a payload will have a repository owner:

    ...  
    \>   "repository" : {  
    \>     "id": 1296269,  
    \>     "full\_name": "octocat/Hello-World",  
    \>     "owner": {  
    \>       "login": "octocat",  
    \>       "id": 1,  
    \>       ...  
    \>     },  
    ...

    To reference the repository owner, you would use `<+eventPayload.repository.owner>`. Here's an example using `name`:

    ![](https://files.helpdocs.io/i5nl071jo5/articles/hndnde8usz/1624919275031/clean-shot-2021-06-28-at-15-27-08.png)

    Next, you enter an operator and the value to match. For example:

    ![](https://files.helpdocs.io/i5nl071jo5/articles/rset0jry8q/1613777562060/image.png)

    #### Referencing Payload Fields

    You can reference any payload fields using the expression `<+trigger.payload.pathInJson>`, where `pathInJson` is the path to the field in the JSON payload.

    For example: `<+trigger.payload.pull_request.user.login>`

    How you reference the path depends on a few things:

    *   There are different payloads for different events.
    *   Different Git providers send JSON payloads formatted differently, even for the same event. For example, a GitHub push payload might be formatted differently than a Bitbucket push payload. Always make sure the path you use works with the provider's payload format.



###  Webhook Trigger Expressions and Operators
 <details>
     <summary>Click to expand</summary>
 
 #### Webhook Trigger Expressions and Operators

 This topic describes how to define the conditions that cause a Webhook Trigger to start a build. Harness triggers are highly configurable and flexible. For example, you can trigger builds based on specific header values, payload values, tag conventions, and changes in specific files or Pull Requests. 

 #### Table of contents

 - [Built-in Git Trigger and Payload Expressions](#built-in-git-trigger-and-payload-expressions)
   * [Main Expressions](#main-expressions)
   * [PR and Issue Comment Expressions](#pr-and-issue-comment-expressions)
   * [Push Expressions](#push-expressions)
 - [JEXL Expressions](#jexl-expressions)
 - [Operators](#operators)


 #### Built-in Git Trigger and Payload Expressions

 Harness includes built-in expressions for referencing trigger details such as a PR number.

 #### Main Expressions

 *   `<+trigger.type>`
     *   Webhook.
 *   `<+trigger.sourceRepo>`
     *   Github, Gitlab, Bitbucket, Custom
 *   `<+trigger.event>`
     *   PR, PUSH, etc.

 #### PR and Issue Comment Expressions

 *   `<+trigger.targetBranch>`
 *   `<+trigger.sourceBranch>`
 *   `<+trigger.prNumber>`
 *   `<+trigger.prTitle>`
 *   `<+trigger.gitUser>`
 *   `<+trigger.repoUrl>`
 *   `<+trigger.commitSha>`
 *   `<+trigger.baseCommitSha>`
 *   `<+trigger.event>`
     *   PR, PUSH, etc.

 #### Push Expressions

 *   `<+trigger.targetBranch>`
 *   `<+trigger.gitUser>`
 *   `<+trigger.repoUrl>`
 *   `<+trigger.commitSha>`
 *   `<+trigger.event>`
 *   PR, PUSH, etc.


 #### JEXL Expressions

 You can refer to payload data and headers using [JEXL expressions](https://commons.apache.org/proper/commons-jexl/reference/syntax.html). That includes all constants, methods, and operators in [JexlOperator](https://commons.apache.org/proper/commons-jexl/apidocs/org/apache/commons/jexl3/JexlOperator.html).

 Be careful when you combine Harness variables and JEXL expressions.

 *   **Invalid expression:** `<+pipeline.variables.MAGIC.toLowerCase()>`  
     This expression is ambiguous. It could be evaluated as a Harness variable (return the value of variable `pipeline.variables.MAGIC.toLowerCase()`) or as a JEXL operation (return the lowercase of literal string `pipeline.variables.MAGIC`).
 *   **Valid expression:** `<+<+pipeline.variables.MAGIC>.toLowerCase()>` First it gets the value of variable `pipeline.variables.MAGIC`. Then it returns the value converted to all lowercase.

 Here are some examples:

 *   `<+trigger.payload.pull_request.diff_url>.contains("triggerNgDemo")`
 *   `<+trigger.payload.pull_request.diff_url>.contains("triggerNgDemo") || <+trigger.payload.repository.owner.name> == "wings-software"`
 *   `<+trigger.payload.pull_request.diff_url>.contains("triggerNgDemo") && (<+trigger.payload.repository.owner.name> == "wings-software" || <+trigger.payload.repository.owner.name> == "harness")`

 #### Operators

 Some operators work on single values and some work on multiple values:

 **Single values:** `equals`, `not equals`, `starts with`, `ends with`, `regex`.

 **Multiple values:** `in`, `not in`.

 The **IN** and **NOT IN** operators don't support Regex.

</details>
 
###  Webhook Trigger Inputs
 <details>
     <summary>Click to expand</summary>
 
 #### Webhook Trigger Inputs

 Runtime Inputs for the Trigger to use, such as Harness Service and artifact.

 You can use the [Built-in Git Payload Expressions](#built_in_git_trigger_and_payload_expressions) and JEXL expressions in this setting.

 See [Run Pipelines using Input Sets and Overlays](/article/gfk52g74xt-run-pipelines-using-input-sets-and-overlays).

 #### Table of contents

 - [Webhook](#webhook)
 - [Git Events Automatically Registered with Webhooks](#git-events-automatically-registered-with-webhooks)
 - [GitHub](#github)
 - [GitLab](#gitlab)
 - [Bitbucket Cloud](#bitbucket-cloud)
 - [Bitbucket Server](#bitbucket-server)

 #### Webhook

 For all Git providers supported by Harness, the Webhook is created in the repo automatically. You don't need to copy it and add it to your repo webhooks.

 ### Git Events Automatically Registered with Webhooks

 The following Git events are automatically added to the webhooks Harness registers.

 #### GitHub

 [GitHub events](https://docs.github.com/en/developers/webhooks-and-events/webhooks/webhook-events-and-payloads):

 *   `create`
 *   `push`
 *   `delete`
 *   `deployment`
 *   `pull_request`
 *   `pull_request_review`

 #### GitLab

 [GitLab events](https://docs.gitlab.com/ee/user/project/integrations/webhooks.html):

 *   Comment events
 *   Issue events
 *   Merge request events
 *   Push events

 #### Bitbucket Cloud

 [Bitbucket Cloud events](https://support.atlassian.com/bitbucket-cloud/docs/event-payloads/):

 *   `issue`
 *   `pull request`

 #### Bitbucket Server

 [Bitbucket Server events](https://confluence.atlassian.com/bitbucketserver/event-payload-938025882.html):

 *   Pull requests
 *   Branch push tag

</details>


## Test the Trigger

1) Make a change on the repo and see if it executes the Trigger. For example, change a file, commit it on a branch, and make a pull request. In your Git provider repo, you can see that the request and response were successful.

  <img src="https://files.helpdocs.io/i5nl071jo5/articles/hndnde8usz/1614104307757/image.png" alt="drawing" width="50%"/>

2) View the Pipeline execution: In Harness CI, click **Builds** (1). You can now see the source branch (2), the target branch (3), and the push request comment and number (4).

  <img src="https://files.helpdocs.io/i5nl071jo5/articles/10y3mvkdvk/1656340605211/webhook-connector-build-fields.png" alt="drawing"/>

3) Click the pull request number. This link opens the Git provider repo at the pull request. If you open the Trigger in the Pipeline, you will see a status in **Last Activation Details**.

  <img src="https://files.helpdocs.io/i5nl071jo5/articles/hndnde8usz/1624922961169/clean-shot-2021-06-28-at-16-29-13.png" alt="drawing" width="50%"/>

Activation means the Trigger was able to request Pipeline execution. It does not mean that the Webhook didn't work.

## See Also 
*   [Triggers Reference](https://ngdocs.harness.io/article/rset0jry8q-triggers-reference)
*   [Harness Git Sync Overview](https://ngdocs.harness.io/article/utikdyxgfz)
*   [Trigger Pipelines Using Git Events](https://ngdocs.harness.io/article/hndnde8usz)
*   [Manage Input Sets and Triggers in Git Experience](https://ngdocs.harness.io/article/8tdwp6ntwz)
