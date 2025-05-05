# Notes
#### What is matrix in Github Actions?
- `matrix strategy is used to run the same job with different parameters. it's important because it allows us to test the code on different environments.`

#### Cache Dependencies.  Example (package.json file)
- Used to speed up workflows
- Re-use dependencies
- `cache action` when a job is triggered if `cache` is available it'll skip steps which makes the workflow run faster.

## Job containers and service containers
#### Service containers to overcome production database issues.
- Ideally we want to run sample (mock) database in testing or code coverage stages.
- We do not want to use Producation database for testing or codecoverage purpose. 
- services are containers that are started before the job runs and are available to the job during its execution. they are useful for running databases or other services that the job depends on. 

#### Job containers 
- job container is a lightweight, stand-alone, executable package of software that includes everything needed to run a piece of software, including the code, runtime, libraries, and system tools. it allows us to run the job in a specific environment without having to set up the environment on the host machine.  this is useful for running jobs that require a specific version of a language or framework, or for running jobs that require a specific set of dependencies. 

---
# Github Action Pipeline workflow
 * Key (.github/workflows) file to store the workflow yaml file.
 1) "Name" of workflow
 2) "on" is used to specify the events that trigger the workflow.
 3) "env" are # environment variables are variables that are available to all jobs and steps in the workflow. they are defined at the top level of the workflow file.
 4) "jobs" are the main building blocks of a workflow. Each job runs in a fresh instance of the virtual environment and can run in parallel or sequentially.

 5) Unit testing
    - Strategy:  Used to test on different OS and nodejs versions
    - Matrix:  matrix strategy is used to run the same job with different parameters. it's important because it allows us to test the code on different environments.
    - Checkout Repository
    - Cache: Chaching to speed up the workflow
    - Unit testing
    - Archive test results

 6) Code coverage
    - Checkout Repository
    - Cache: Chaching to speed up the workflow
    - Check code coverate (continue-on-error)
    - Archive test results


---
# Expressions

- `continue-on-error: true`               # skip if there's an error
- `if:  always()`                         # excute even the previous step fails
- `needs: [unit-testing, code-coverage]`  # this job will run after the unit-testing and code-coverage jobs are completed successfully
- `context: .`  # context is the path to the Dockerfile. it can be a local path or a URL.
-  `permissions: packages: write `        # In case of adding images to GHCR this job will have write access to the package registries