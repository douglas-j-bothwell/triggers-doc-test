- [Webhook Triggers](https://douglas-j-bothwell.github.io/triggers-doc-test)
  - [Define a Webhook Trigger](https://douglas-j-bothwell.github.io/triggers-doc-test/define-a-webhook-trigger)
  - [Webhook Trigger Configuration](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-configuration)
  - [Webhook Trigger Conditions](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-conditions)
  - [Webhook Trigger Inputs](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-inputs)


# Webhook Trigger Conditions

This topic describes how to define the conditions that cause a Webhook Trigger to start a build. Harness triggers are highly configurable and flexible. For example, you can trigger builds based on specific header values, payload values, tag conventions, and changes in specific files or Pull Requests. 

Topics discussed:

- [Conditions are ANDs](#conditions-are-ands)
- [Source and Target Branch](#source-and-target-branch)
- [Built-in Git Trigger and Payload Expressions](#built-in-git-trigger-and-payload-expressions)
- [Main Expressions](#main-expressions)
- [PR and Issue Comment Expressions](#pr-and-issue-comment-expressions)
- [Push Expressions](#push-expressions)
- [Header Conditions](#header-conditions)
- [Payload Conditions](#payload-conditions)
- [Referencing Payload Fields](#referencing-payload-fields)
- [JEXL Expressions](#jexl-expressions)
- [Operators](#operators)



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

#### Built-in Git Trigger and Payload Expressions

Harness includes built-in expressions for referencing trigger details such as a PR number.

##### Main Expressions

*   `<+trigger.type>`
    *   Webhook.
*   `<+trigger.sourceRepo>`
    *   Github, Gitlab, Bitbucket, Custom
*   `<+trigger.event>`
    *   PR, PUSH, etc.

##### PR and Issue Comment Expressions

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

##### Push Expressions

*   `<+trigger.targetBranch>`
*   `<+trigger.gitUser>`
*   `<+trigger.repoUrl>`
*   `<+trigger.commitSha>`
*   `<+trigger.event>`
    *   PR, PUSH, etc.

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
