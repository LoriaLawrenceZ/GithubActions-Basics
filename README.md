<div name="readme-top">
  <h1 align=center>GithubActions-Basics</h1>
</div>

---

## Understanding the workflow file

```YML
name: learn-github-actions
run-name: ${{ github.actor }} is learning GitHub Actions
on: [push]
jobs:
  check-bats-version:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
      - run: npm install -g bats
      - run: bats -v

```

### YML Syntax

---

```YML
name: learn-github-actions
```

> **Optional** - The name of the workflow as it will appear in the "Actions" tab of the GitHub repository. If this field is omitted, the name of the workflow file will be used instead.

---

```YML
run-name: ${{ github.actor }} is learning GitHub Actions
```

> **Optional** - The name for workflow runs generated from the workflow, which will appear in the list of workflow runs on your repository's "Actions" tab. This example uses an expression with the `github` context to display the username of the actor that triggered the workflow run. For more information, see "[Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#run-name)"

---

```YML
on: [push]
```

> Specifies the trigger for this workflow. This example uses the `push` event, so a workflow run is triggered every time someone pushes a change to the repository or merges a pull request. This is triggered by a push to every branch; for examples of syntax that runs only on pushes to specific branches, paths, or tags, see "[Workflow syntex for Github Actions](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#onpushpull_requestpull_request_targetpathspaths-ignore)"

---

```YML
jobs:
```

> Groups together all the jobs that run in the `learn-github-actions` workflow.

---

```YML
  check-bats-version:
```

> Defines a job named `check-bats-version`. The child keys will define properties of the job.

---

```YML
    runs-on: ubuntu-latest
```

> Configures the job to run on the latest version of an **Ubuntu Linux runner**. This means that the job will execute on a fresh virtual machine hosted by GitHub. For syntax examples using other runners, see "[Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idruns-on)"

---

```YML
    steps:
```

> Groups together all the steps that run in the `check-bats-version` job. Each item nested under this section is a separate action or shell script.

---

```YML
      - uses: actions/checkout@v4
```

> The `uses` keyword specifies that this step will run `v4` of the `actions/checkout` action. This is an action that checks out yous repository onto the runner, allowing you to run scripts or other actions against your code (such as build and test tools). You should use the checkout action any time your workflow will use the repositorys code.

---

```YML
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
```

> This step uses the `actions/setup-node@v4` action to install the specified version of the Node.js. (This example uses version 14.) This puts both the `node` and `npm` commands in your `PATH`.

---

```YML
      - run: npm install -g bats
```

> The `run` keyword tells the job to execute a command on the runner. In this case, you are using `npm` to install the `bats` software testing package.

---

```YML
      - run: bats -v
```

> Finnaly, you'll run the `bats` command with a parameter that outputs the software version.

### Visualizing the workflow file

This diagram represents the file that was just created and how the GitHub Actions components are organized in a hierarchy. Each step executes a single action or shell script. Steps 1 and 2 runs actions, while steps 3 and 4 run shell scripts. To find more prebuilt actions for your workflows, see "[Finding and customizing actions](https://docs.github.com/en/actions/learn-github-actions/finding-and-customizing-actions)"

![image](https://github.com/LoriaLawrenceZ/GithubActions-Basics/assets/97912499/0006dd99-92f8-44de-8dd8-ce746324a4ef)

