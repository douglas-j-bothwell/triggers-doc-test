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
  <summary>Click here to see how you can create and run a Trigger in response to Git events.</summary>

<iframe  width="640"  height="480" src="https://www.youtube.com/embed/y8s351IJLXw"  frameborder="0" allow="autoplay; encrypted-media" allowfullscreen> </iframe>
  
</details>

##### Table of contents

- [Important Notes](#important-notes)
- [Visual Summary](#visual-summary)
- [Before You Begin](#before-you-begin)
- [Define the Trigger](#define-the-trigger)
- [Test the Trigger](#test-the-trigger)


## Limitations

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

3) The New Webhook setup wizard has three tabs: Configure, Conditions, and Pipeline Inputs. Set up the Trigger as described in:

- [Webhook Trigger Configuration](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-configuration)
- [Webhook Trigger Conditions](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-conditions)
- [Webhook Trigger Expressions and Operators](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-expressions)
- [Webhook Trigger Inputs](https://douglas-j-bothwell.github.io/triggers-doc-test/webhook-trigger-inputs)

4) Save and test the filter as described below.

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
