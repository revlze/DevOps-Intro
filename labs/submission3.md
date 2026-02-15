# Lab 3

## Task 1

### Task 1.1

I followed the [GitHub Actions quickstart guide](https://docs.github.com/en/actions/quickstart) and created a workflow file at `.github/workflows/github-actions-demo.yml`.

**Workflow file contents:**

```yaml
name: GitHub Actions Demo
run-name: ${{ github.actor }} is testing out GitHub Actions
on: [push]
jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      - name: Check out repository code
        uses: actions/checkout@v5
      - run: echo "The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "The workflow is now ready to test your code on the runner."
      - name: List files in the repository
        run: |
          ls ${{ github.workspace }}
      - run: echo "This job's status is ${{ job.status }}."
```

**Key concepts learned:**

- **Workflow** — an automated process defined in a YAML file inside `.github/workflows/`. Triggered by events, schedules, or manually.
- **Job** — a set of steps that execute on the same runner. In this workflow there is one job: `Explore-GitHub-Actions`.
- **Step** — an individual task within a job. Can be a shell command (`run:`) or a reusable action (`uses:`).
- **Runner** — a virtual machine (hosted by GitHub) that executes the job. Here we use `ubuntu-latest`.
- **Trigger** — the event that starts the workflow. Here it is `push` — any push to any branch triggers the workflow.
- **Action** — a reusable unit of code (e.g. `actions/checkout@v5` clones the repository onto the runner).

### Task 1.2

**Successful run link:** [GitHub Actions Demo — Run #22031908377](https://github.com/revlze/DevOps-Intro/actions/runs/22031908377)

**What caused the run to trigger:**
The workflow was triggered by a `push` event — I committed and pushed the workflow file to the `feature/lab3` branch. Since the trigger is `on: [push]`, any push to any branch starts the workflow.

**Workflow execution analysis:**

1. GitHub detected the push event and found the workflow file in `.github/workflows/`.
2. A fresh `ubuntu-latest` runner was provisioned.
3. The job `Explore-GitHub-Actions` started executing steps sequentially:
   - Printed event metadata (event type, OS, branch, repo).
   - Checked out the repository code using `actions/checkout@v5`.
   - Listed the repository files in the workspace.
   - Reported the final job status as `success`.
4. The entire workflow completed in ~6 seconds.

