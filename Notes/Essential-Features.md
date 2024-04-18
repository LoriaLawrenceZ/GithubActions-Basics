<div name="readme-top">
  <h1 align=center>Essential Features of GitHub Actions</h1>
</div>

---

## 📌 Overview

GitHub Actions allow you to customize your workflows to meet the unique needs of your application and team. There are some essencial customization techniques such as using variables, running scripts, and sharing data and artifacts between jobs.

## 🔵 Using Variables in Your Workflows

GitHub Actions include default environment variables for each workflow run. If you need to use custom environment variables, you can set these in your YAML workflow file. This example demonstrates how to create custom variables named `POSTGRES_HOST` and `POSTGRES_PORT`. These variables are then available to the `node client.js` script.

```YML
jobs:
  example-job:
    runs-on: ubuntu-latest
    steps:
      - name: Connect to PostgreSQL
        run: node client.js
        env:
          POSTGRES_HOST: postgres
          POSTGRES_PORT: 5432
```

For more information, see "[Variables](https://docs.github.com/en/actions/learn-github-actions/variables#default-environment-variables)

## 🔵 Adding Scripts to Your Workflow

You can use a GitHub Actions workflow to run scripts and shell commands, which are then executed on the assigned runner. This example demonstrates how to use the `run` keyword to execute the command `npm install -g bats` on the runner.

```YML
jobs:
  example-job:
    runs-on: ubuntu-latest
    steps:
      - run: npm install -g bats
```

To use a workflow to run a script stored in your repository you must first check out the repository to the runner. Having done this, you can use the `run` keyword to run the script on the runner. The following example runs two scripts, each in a separate job step. The location of the scripts on the runner is specified by setting a default working directory for run commands. For more information, see "[Setting default values for jobs](https://docs.github.com/en/actions/using-jobs/setting-default-values-for-jobs)."

```YML
jobs:
  example-job:
    runs-on: ubuntu-latest
    defaults:
      run:
        working-directory: ./scripts
    steps:
      - name: Check out the repository to the runner
        uses: actions/checkout@v4  
      - name: Run a script
        run: ./my-script.sh
      - name: Run another script
        run: ./my-other-script.sh
```

Any scripts that you want a workflow job to run must be executable. You can do this either within the workflow by passing the script as an argument to the interpreter that will run the script - for example, `run: bash script.sh` - or by making the file itself executable. You can give the file the execute permission by using the command `git update-index --chmod=+x PATH/TO/YOUR/script.sh` locally, then committing and pushing the file to the repository. Alternatively, for workflows that are run on Linux and Mac runners, you can add a command to give the file the execute permission in the workflow job, prior to running the script:

```YML
jobs:
  example-job:
    runs-on: ubuntu-latest
    defaults:
      run:
        working-directory: ./scripts
    steps:
      - name: Check out the repository to the runner
        uses: actions/checkout@v4  
      - name: Make the script files executable
        run: chmod +x my-script.sh my-other-script.sh
      - name: Run the scripts
        run: |
          ./my-script.sh
          ./my-other-script.sh
```

For more information about the `run` keyword, see "[Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idstepsrun)."


