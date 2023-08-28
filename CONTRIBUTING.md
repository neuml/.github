# How to contribute

*NOTE: Please file an issue or post a message in Slack before working on a pull request. This will ensure there is no wasted or duplication of effort.*

Thank you for showing an interest in contributing! Pull Requests are welcome and encouraged! This document gives an overview of the development standards for the project. Please note that this file covers contributing to any of our projects, most of which are in Python. For non-Python projects, everything regarding how to Submit a Pull Request (PR) applies.

## Principles

### 💡 Quality

This project strives to develop clean, well documented code with comprehensive test coverage. Test-driven development does add some overhead in having to think hard about test cases and ensure all major functionality is covered in the tests. That doesn't mean that simple methods need to have tests but all major components should have tests. All methods should be well-documented and easy to understand.

### ⚙️ Performance

Machine learning is not fast to begin with, runtime performance is a top priority. 

### ❓ Questions welcome

We're here to help! The best place to reach out is via the `Issues` tab for the project on GitHub. If you want to bounce ideas and verify what you're seeing before digging in, please reach out!

## Set up a development environment

Fork the repository and clone it locally. Linux, macOS and Windows setups should all work but Linux is the most tested dev environment.

```bash
git clone https://github.com/<your github username>/<project name>
cd <project name> 
git remote add upstream https://github.com/neuml/<project name>
```

Run the following commands to install all dependencies (including dev dependencies) and install the pre-commit hook. 

```bash
pip install -e .[dev]
pre-commit install
```

_Note: txtai requires an additional `all` argument when installing. In other words, `pip install -e .[all,dev]`_

Once complete, run the tests to validate everything is working properly

```bash
make data
make coverage
coverage report
```

An IDE isn't required but highly-recommended for any substantial changes. The recommended IDE is Visual Studio Code with the Python extension installed. This project can be directly loaded with VS Code.

## Review the project

The README is the best place to start to learn more about the project. There is a series of example notebooks that covers all major components and functionality in the project. It's suggested that you run through those examples on Google Colab to see how the code currently works.

All the code should have ample documentation to help understand the logic flow. Hopefully, the code is self documenting in itself but for particularly complex situations/edge cases, additional documentation will be there to provide context.

## Style guide

There are a couple tools integrated to help with streamlining code formatting/styling.

- [Pylint](https://github.com/PyCQA/pylint) enforces best practices for code usage across the project
- [Black](https://github.com/psf/black) enforces code formatting standards
- [Google Python Style](https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings) is the standard for documentation strings

## Make the changes

Once comfortable with the code, let's get to developing!

- If you're looking to contribute but don't know where to start, look at the list of issues marked as `Good First Issue` and assign it to yourself.
- If you ran into a specific bug or have an idea for an enhancement, great! Please first file an issue to ensure it's not already being worked.

Once an area of work is identified, the first thing to do is to create a branch to hold the changes. It's best to have a branch for each individual Pull Request (PR), ideally tied to an open issue. Example below of creating a branch.

```bash
git checkout -b descriptive-name
```

The best way to develop is incrementally, testing along the way. A good practice is to start with a test covering the desired functionality. This may be an existing test in the case of a bug/enhancement or a new test when building new functionality. 

An individual test can be run as follows:

```bash
python -m unittest -v test/python/<testname>.py
```

## Submit a Pull Request (PR)

On each commit to GitHub (including forks), a GitHub Action script runs a full build process. This build validates that the build runs, all tests pass and that all code meets code standards. Anything that runs in the build script has a corresponding way to run locally and should be run locally before committing as shown below.

1. Run all tests locally

    ```bash
    make data
    make coverage
    coverage report
    ```

    Ensure that the test coverage has not decreased. If so, additional tests are needed to cover the new functionality.

2. Run the pre-commit checks for styling/linting.

    Note that the commit will fail if the pre-commit hook tests don't successfully run. If VS Code is used as the development environment, any errors would be visible during development in the problems panel. The pre-commit checks can be directly run as follows:

    ```bash
    pre-commit run
    ```

3. Stage and commit the changes locally.

    Before pushing and during development, it's good practice to sync with the main repository regularly as follows. This helps reduce the likelihood of merge errors. 

    ```bash
    git fetch upstream
    git rebase upstream/master
    ```

    ```bash
    git add . 
    git commit -m "<descriptive message - include link to #issue and/or #pr>"
    ```

4. Push the changes

    ```bash
    git push -u origin descriptive-name
    ```

5. Submit the PR on GitHub

    Go to the main project on GitHub and submit your PR via the `Pull Requests` tab for the project on GitHub.

6. Changes reviewed

    Pull requests are carefully reviewed before merging. Please don't be discouraged if a there is follow up or questions on the changes. We want to help get the changes into a state where they can be merged in!
