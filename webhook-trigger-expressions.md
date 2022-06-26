- [Webhook Triggers](https://douglas-j-bothwell.github.io/triggers-doc-test)
  - [Define a Webhook Trigger](https://douglas-j-bothwell.github.io/triggers-doc-test/define-a-webhook-trigger)
  - [Webhook Trigger Configuration](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-configuration)
  - [Webhook Trigger Conditions](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-conditions)
	- [Webhook Trigger Expressions and Operators](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-expressions)
	- [Webhook Trigger Inputs](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-inputs)


# Webhook Trigger Expressions and Operators

This topic describes how to define the conditions that cause a Webhook Trigger to start a build. Harness triggers are highly configurable and flexible. For example, you can trigger builds based on specific header values, payload values, tag conventions, and changes in specific files or Pull Requests. 

Topics discussed:

- [Built-in Git Trigger and Payload Expressions](#built-in-git-trigger-and-payload-expressions)
  * [Main Expressions](#main-expressions)
  * [PR and Issue Comment Expressions](#pr-and-issue-comment-expressions)
  * [Push Expressions](#push-expressions)
- [JEXL Expressions](#jexl-expressions)
- [Operators](#operators)


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