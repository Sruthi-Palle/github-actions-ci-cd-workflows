1. Core Concepts: Workflows, Jobs, and Steps

GitHub Actions automation is built upon a hierarchy of three main components:

Workflows: The highest-level entity, attached to a specific repository. A workflow is defined by a single YAML file and can contain one or more jobs. A repository can have multiple workflow files.

Jobs: A set of steps that execute on the same runner. By default, jobs run in parallel, but they can be configured to run sequentially.

Steps: The smallest unit of a job. A step can be a shell command or a pre-built, reusable unit of code called an action. Steps within a job are executed in order.

It is noted that while the term "action" is often used as a synonym for "workflow," it also refers to a specific, separate feature (reusable units of code). The primary construct being created in this process is a workflow.

2. Workflow File Definition

GitHub Actions workflows are defined in YAML (.yml) files. The structure and naming of these files are critical for their detection by GitHub.

2.1. File Location

For GitHub to recognise a workflow, the YAML file must be placed in a specific directory within the repository:

Path: .github/workflows/

Any .yml or .yaml file within this directory will be treated as a workflow definition.

3. Configuring Workflow Components

3.1. Triggering the Workflow with on

The on key determines when the workflow will be executed. While many events can automatically trigger workflows (e.g., a push to a branch), the initial example uses a manual trigger:

workflow_dispatch: This specific event allows a user to manually trigger the workflow from the Actions tab in the GitHub UI. This is useful for testing and on-demand automation.

3.2. Defining the Runner Environment with runs-on

The runs-on key specifies the virtual machine environment where the job will execute. GitHub provides and maintains several runner environments.

Available Environments: At the time of recording, supported environments include various versions of Ubuntu, Windows Server, and macOS.

Identifier Usage: The workflow file must use the specific identifiers provided by GitHub (e.g., ubuntu-latest, windows-latest). The latest tag points to the most recent stable version of the specified OS.

Hardware Specifications: GitHub predefines the hardware specifications (CPU, RAM, storage) for each runner type.

3.3. Defining Steps

Steps are listed under the steps key within a job. Each step is denoted by a dash (-) as it is an item in a list.

name: Assigning a name to a step is a best practice, as this name appears in the execution logs, making it easier to identify and debug.

run: This key is used to execute a command directly in the runner's shell. The command is provided as the value for this key.

4. Committing, Executing, and Analysing the Workflow

4.1. Committing the Workflow File

Since the workflow definition is a file within the repository, creating or modifying it is a standard Git operation.

Workflows as Code: The workflow file is treated as part of the project's code. Saving the file in the GitHub editor creates a new commit in the repository. This ensures that automation logic is version-controlled alongside the application code.

4.2. Executing the Workflow

Once the workflow file is committed to the repository, it becomes active.

Navigate to the Actions tab.

The new workflow will be listed in the left-hand sidebar, identified by the name specified in the YAML file.

Because the on trigger was set to workflow_dispatch, a button will be present allowing the user to "Run workflow" manually.

Clicking this button queues the workflow for execution.

4.3. Analysing the Workflow Run

The Actions tab provides a detailed view of both in-progress and completed workflow runs.

Run Status: Each run is marked with an icon indicating its status: a yellow dot for "in-progress" and a green checkmark for "successful."

Detailed View: Clicking on a specific workflow run provides a breakdown of the jobs executed.

Job and Step Logs: Clicking on a job reveals the sequence of steps that were performed.

Automatic Steps: GitHub automatically adds setup and cleanup steps to each job to prepare and tear down the runner environment.

User-Defined Steps: Each step defined in the YAML file can be expanded to show the exact command that was run and its corresponding output in the command line.

This granular logging is essential for verifying that the workflow executed as expected and for debugging any issues that may arise. The workflow can be re-run manually as many times as needed directly from this interface.
