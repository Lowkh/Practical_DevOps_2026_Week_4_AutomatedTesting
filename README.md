# Automated Testing Tools Group Practical

> A two-hour, hands-on introduction to browser automation using Windows and Google Chrome or Microsoft Edge.

> [!NOTE]
> ## Educational Practice Materials
>
> Use fictional task names only. Do not enter or share personal passwords, API keys, identification numbers, personal contact details or confidential information. Screenshots and traces may contain page content.

Learn automated testing by opening practice websites, automating browser actions and checking results.

No previous automated testing experience is needed. You have already completed a basic Python module. This practical builds on that knowledge. Complete Python examples and explanations are provided. You do not need to build a website, learn JavaScript or create an application server.

Work in a group of 3–5. Each member uses their own computer and GitHub account, creates a separate test file and runs their own tests. Work together when solving problems, but do not divide the guided tests among members. Each member also creates two distinct additional tests, with no scenario duplicated within the group. The coordinator prepares only the shared repository and starting files.

### Practical overview

| Item | Details |
| --- | --- |
| Main lesson | Two hours: 120 minutes. |
| Before you start | Use the checklist in Section 1 to confirm your existing software, accounts and access. |
| Operating system | Windows. |
| Python knowledge | Basic Python, from the module completed earlier. |
| Main browser | Installed stable Google Chrome or Microsoft Edge. |
| Terminal | Windows Command Prompt inside VS Code. |
| Project location | A folder of your choice where you can save files. |
| Task-list website | [Playwright TodoMVC](https://demo.playwright.dev/todomvc/) |
| Login website | [The Internet login demonstration](https://the-internet.herokuapp.com/login) |
| Personal source file | `tests/test_member_1.py`, using your own member number. |
| Cases per member | Eight guided cases plus two distinct individual cases: ten in total before optional additions. |
| After the lesson | Optional activities in Section 16. |

### Tools used

| Tool | What it does |
| --- | --- |
| Python | Runs test code. |
| VS Code and its Microsoft Python extension | Help you create and edit files. |
| Chrome or Edge | Runs the browser activities. Choose either one. |
| Playwright | Controls the browser and checks page behaviour. |
| Codegen | Records browser actions and creates starting code. |
| pytest | Finds and runs tests. |
| pytest-html | Creates an HTML results report. |
| Git and GitHub | Save, share and combine changes. |
| Trace Viewer, used after the lesson | Helps you look back through a test run. |

### Browser choices

| Browser | Use | Selection |
| --- | --- | --- |
| Microsoft Edge | Main option. | `--browser chromium --browser-channel msedge` |
| Google Chrome | Equally suitable main option. | `--browser chromium --browser-channel chrome` |
| Playwright Chromium | Optional post-lesson browser. | `--browser chromium` without a channel |
| Playwright Firefox | Optional post-lesson browser. | `--browser firefox` |
| Playwright WebKit | Optional post-lesson browser. | `--browser webkit` |

> [!IMPORTANT]
> Chrome and Edge are Chromium-based browsers. In pytest, `--browser chromium` selects the browser family. The channel selects installed Chrome or Edge.
>
> Do not use `--browser chrome` or `--browser edge`. Use `--browser-channel chrome` or `--browser-channel msedge`.
>
> You do not need to download Playwright Chromium for the main lesson.


### How this practical connects to the lesson slides

| Lesson material | Connection to the activities |
| --- | --- |
| `OAL-03-1-Why-Do-We-Test.pptx` | Testing purpose, levels, positive and negative cases, input groups, boundaries and test parameters. |
| `OAL-03-2-Manual-vs-Automated.pptx` | Manual exploration, repeatable checks, regression testing, reusable code and maintenance. |
| `03-3-Testing-Tools.pptx` | Match tools to goals, distinguish built-in and external tools, black-box testing and diagnostic outputs. |

The slides provide the concepts. This practical applies selected concepts through small browser checks rather than attempting every testing type or tool.

## Contents

1. [Before you start: check what you have](#1-before-you-start-check-what-you-have)
2. [The two-hour lesson plan](#2-the-two-hour-lesson-plan)
3. [Understand the workflow](#3-understand-the-workflow)
4. [Create and clone the group repository](#4-create-and-clone-the-group-repository)
5. [Create the shared starting files](#5-create-the-shared-starting-files)
6. [Prepare your branch and Python environment](#6-prepare-your-branch-and-python-environment)
7. [Explore and run your first test](#7-explore-and-run-your-first-test)
8. [Check task completion](#8-check-task-completion)
9. [Run one test with different inputs](#9-run-one-test-with-different-inputs)
10. [Test a simple login](#10-test-a-simple-login)
11. [Record and replay browser actions](#11-record-and-replay-browser-actions)
12. [Use a helper to add two tasks](#12-use-a-helper-to-add-two-tasks)
13. [Create a report and capture screenshots](#13-create-a-report-and-capture-screenshots)
14. [Combine the group files](#14-combine-the-group-files)
15. [Simple syntax reference](#15-simple-syntax-reference)
16. [Optional post-lesson practice](#16-optional-post-lesson-practice)
17. [Troubleshooting common errors](#17-troubleshooting-common-errors)
18. [Quick command reference](#18-quick-command-reference)

***

## 1. Before you start: check what you have

You should already have the software and accounts used in this practical. Use this checklist to confirm that you are ready.

### 1.1 Computer and software

- [ ] I am using a Windows computer.
- [ ] I have Python 3.12 or 3.13.
- [ ] I have Visual Studio Code.
- [ ] I have the Python extension published by Microsoft in VS Code.
- [ ] I have Git.
- [ ] I have stable Google Chrome or Microsoft Edge.
- [ ] I have a folder of my choice where I can save the project.

You do not need both Chrome and Edge. Choose either one for the main activities.

### 1.2 Terminal and version checks

Use Command Prompt inside VS Code throughout this practical.

To open it:

1. Select Terminal → New Terminal.
2. Open the dropdown beside the terminal's `+` button.
3. Select Command Prompt.

Run these commands one at a time:

```bat
python --version
```

```bat
git --version
```

You should see a version number for each tool. If the Python command does not work, try:

```bat
py -3 --version
```

- [ ] Command Prompt is open in VS Code.
- [ ] Python displays a version number.
- [ ] Git displays a version number.

> [!TIP]
> If the terminal shows Python's `>>>` prompt, enter `exit()` and press Enter before running terminal commands.

### 1.3 Browser and website access

Open your chosen browser and check that both practice websites load:

- [ ] [Playwright TodoMVC task list](https://demo.playwright.dev/todomvc/)
- [ ] [The Internet login demonstration](https://the-internet.herokuapp.com/login)

You do not need to sign in to a personal browser profile or create an account on either practice website.

### 1.4 GitHub and commit identity

- [ ] I have my own GitHub account.
- [ ] I can sign in to GitHub.
- [ ] I know my GitHub username.

Check the name and email Git will use for your commits:

```bat
git config --global user.name
```

```bat
git config --global user.email
```

- [ ] Git displays my intended commit name.
- [ ] Git displays my intended commit email.

If either value is missing or incorrect, replace the example values below with your own details:

```bat
git config --global user.name "Your Name"
git config --global user.email "YOUR_GITHUB_COMMIT_EMAIL"
```

Use an email linked to GitHub or your GitHub no-reply email.

> [!NOTE]
> Your commit name and email identify your changes. They do not sign you in to GitHub.
>
> Never put passwords or access tokens in project files.

### 1.5 Group details

Confirm these details with your group:

- [ ] We know who will coordinate the initial repository setup.
- [ ] We have agreed on a repository name.
- [ ] Each member has a member number, starting at 1.
- [ ] We have shared our GitHub usernames with the coordinator.
- [ ] Each member knows which personal test filename and branch to use.

Each member will create and run their own tests. The coordinator creates only the shared repository and starting files.

### If something is missing

Check the relevant troubleshooting instructions in Section 17. If software access requires administrator permission, use the approved IT support process. Do not bypass computer or browser restrictions.

The project-specific Python environment and testing packages will be set up together in Section 6.

***

## 2. The two-hour lesson plan

| Time | Activity | Sections |
| --- | --- | --- |
| 0–15 minutes | Create and clone the repository; agree distinct scenarios and share starting files. | 3–5 |
| 15–25 minutes | Prepare personal branches, packages and browser choice. | 6 |
| 25–35 minutes | Explore the task list and run the first test. | 7 |
| 35–40 minutes | Add the completion test. | 8 |
| 40–50 minutes | Test blank inputs. | 9 |
| 50–65 minutes | Test correct and incorrect login details. | 10 |
| 65–75 minutes | Record, add a check and replay. | 11 |
| 75–80 minutes | Use the helper to add two tasks. | 12.1–12.3 |
| 80–100 minutes | Create and run two distinct tests of your own. | 12.4 |
| 100–110 minutes | Generate a report and inspect screenshots. | 13 |
| 110–120 minutes | Combine completed files and update local main. | 14 |
| Total | 120 minutes | |

The timing assumes the software, accounts and website access in Section 1 are already available. If a check reveals a problem, use Section 17 and preserve your progress. Continue unfinished main activities afterwards if necessary. Do not hide errors or remove checks to keep to the timing.

Use Section 15 as a syntax reference, Section 17 when an error appears and Section 18 for common commands. Section 16 provides further practice after the lesson.

***

## 3. Understand the workflow

Playwright performs browser actions. pytest runs test functions. Assertions check the result.

```text
Open a page → Perform an action → Check the result
```

### Key terms

| Term | Simple meaning |
| --- | --- |
| Locator | An instruction that finds part of a page. |
| Action | Something the browser does, such as typing or clicking. |
| Assertion | A check of an expected result. |
| Negative test | A test of invalid input or an invalid action. |
| Parametrization | Running one test with different inputs. |
| Helper | A function that performs steps you want to reuse. |
| Virtual environment | A separate set of Python packages for this project. |
| Browser channel | Installed Chrome or Edge selected for a run. |
| Repository | A project whose changes are tracked by Git. |
| Branch | A separate line of work in a repository. |
| Commit | A saved record of selected changes on your computer. |
| Push | Upload commits to GitHub. |
| Pull request, or PR | A request to combine a branch with another branch. |
| Merge | Combine changes from branches. |
| `.gitignore` | Lists local files and folders to leave out when adding new files to Git. |

Actions:

```python
task_input.fill("Read testing notes")
task_input.press("Enter")
```

Assertion:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

These snippets explain the idea. Complete examples follow later. A script that only clicks and types may finish without checking the intended result.

A negative test can pass. The incorrect-password test passes when the website rejects the password as expected.


### Why test, and where do these checks fit?

Tests help reveal problems before users depend on the software. A failed check needs investigation: the cause may be the application, the test, the environment or an unavailable website. Passing selected checks does not prove that all defects are absent.

| Idea from the slides | Meaning here |
| --- | --- |
| System-level functional checking | Use the running website through its external interface. |
| Black-box approach | Choose inputs and check outputs without reading application source. |
| Web GUI testing | Interact with fields, buttons, links and task rows. |
| Automated execution | The tool performs predefined steps after you start pytest. |

These are small user-flow checks near the top of the testing pyramid. They do not replace unit or integration tests. Using pytest does not make a browser check a unit test. The `add_task()` helper is test-support code, not an isolated function from the demonstration application's implementation.

This practical does not measure code coverage, perform load or security testing, validate internal service integration, or provide formal acceptance sign-off. Login checks verify visible login behaviour, not the security of the login system. Test durations are not performance benchmarks.

### Built-in and external tools complement each other

| Tool | Source and purpose |
| --- | --- |
| Browser Developer Tools | Built into Chrome or Edge; inspect elements, messages and requests. |
| Python `unittest` | Built into Python; suitable for focused local checks. |
| Playwright, including Codegen and Trace Viewer | Additional project tooling for browser automation and investigation. |
| pytest and pytest-html | Additional Python packages for running tests and reporting. |
| Git and GitHub | Separate version-control tools and service for sharing source. |

Choose tools according to the testing goal. Being available through an editor does not make a package part of Python's standard library.

### Positive or negative is different from pass or fail

A normal task and correct login details are positive examples. Blank task input and an incorrect password are negative examples. Both types pass when the expected behaviour occurs.

The slides describe cases where invalid input should be rejected. In pytest output, `FAILED` means a test step or assertion did not succeed; negative cases should not automatically report `FAILED`.

### Shared work pattern

```text
Update main → Create a branch → Edit and run
            → Save → Commit → Push → Open a PR → Merge
            → Everyone updates main
```

Saving does not commit. Committing does not upload. Pushing does not merge.

> [!IMPORTANT]
> Enter commands in the terminal and Python code in the named `.py` file. Save before running. Copy only code inside a code block, not surrounding backticks.

> [!WARNING]
> Use only small practice runs. Do not run load tests, security scans or continuous loops against public websites. Do not force-push or use destructive Git commands to bypass a problem.

***

## 4. Create and clone the group repository

### 4.1 Use your member number

| Member | Personal file | Personal branch |
| --- | --- | --- |
| 1 | `tests/test_member_1.py` | `testing/member-1` |
| 2 | `tests/test_member_2.py` | `testing/member-2` |
| 3 | `tests/test_member_3.py` | `testing/member-3` |
| 4, if present | `tests/test_member_4.py` | `testing/member-4` |
| 5, if present | `tests/test_member_5.py` | `testing/member-5` |

Examples use Member 1. Replace member numbers in filenames, paths and branches with your own. Keep Python function names unchanged.

### 4.2 Coordinator: create the repository

On GitHub:

1. Create a repository, for example `automated-testing-group-01`.
2. Use approved visibility. A private repository limits access to invited people.
3. Add a README and confirm the starting branch is `main`.
4. Put this guide in `README.md`.
5. Open Settings → Collaborators, or the equivalent access page.
6. Invite members using their GitHub usernames.
7. Members accept their invitations.

### 4.3 Everyone: clone the repository

Choose where to keep the project.

1. In Windows File Explorer, open a folder of your choice where you can save files.
2. Click the address bar and copy its full path.
3. Replace the placeholder below with that path. Keep the quotation marks.

```bat
cd /d "PASTE_YOUR_CHOSEN_FOLDER_PATH_HERE"
```

On GitHub, select Code → HTTPS and copy the repository URL. Replace the placeholder:

```bat
git clone PASTE_THE_COPIED_HTTPS_URL_HERE
```

Enter the new folder using its actual name, for example:

```bat
cd automated-testing-group-01
```

In VS Code, use File → Open Folder to open that project folder. Open a new Command Prompt terminal.

```bat
git status
git remote -v
```

You should be on `main`. `origin`, Git's short name for the remote repository, should point to your group repository.

> [!TIP]
> Members may choose different locations. Run remaining commands inside the cloned project folder, not its parent folder.


### 4.4 Agree your two additional scenarios

Look ahead at the ideas in Section 12.4. As a group, reserve two different scenarios for each member. No scenario should be allocated twice within your group, and the two choices must go beyond the guided cases.

The coordinator records the agreed choices in the setup file described in Section 5.5. Members may help each other, but everyone implements and runs their own two scenarios.

***

## 5. Create the shared starting files

> [!IMPORTANT]
> The coordinator completes this section first. Others continue with Section 6 after the setup changes are merged.

### 5.1 Create a setup branch

```bat
git switch main
git pull --ff-only origin main
git switch -c setup/testing-files
```

`switch -c` creates a branch. `pull --ff-only` updates only when Git can move the branch directly forward.

### 5.2 Create `.gitignore`

In VS Code, create `.gitignore` beside `README.md`. Do not name it `.gitignore.txt`.

```gitignore
.venv/
__pycache__/
.pytest_cache/
reports/
recordings/
test-results/
.env
```

These files stay on your computer but are not normally added to commits.

| Entry | What stays local |
| --- | --- |
| `.venv/` | Python environment and installed packages. |
| `__pycache__/` | Temporary Python files. |
| `.pytest_cache/` | Temporary pytest information. |
| `reports/` | Generated HTML reports. |
| `recordings/` | Individual recording experiments. |
| `test-results/` | Screenshots, traces and other generated output. |
| `.env` | A possible local settings file; not required here. |

Commit `.gitignore` itself so everyone uses the same rules. Create it before adding generated files or environments to Git.

> [!IMPORTANT]
> `.gitignore` is not a security tool. It does not remove files already tracked by Git or erase earlier commits. Inspect selected changes before committing.

### 5.3 Create `requirements.txt`

```text
pytest-playwright
pytest-html
```

### 5.4 Create `pytest.ini`

```ini
[pytest]
testpaths = tests
addopts = -v --browser chromium
```

Keep `--browser chromium`. Members choose Chrome or Edge through their commands.


### 5.5 Create the shared scenario plan

Create a `docs` folder and a file named `docs/test-plan.md`. The coordinator fills in the choices agreed in Section 4.4:

```markdown
# Group test choices

Each member creates two additional tests beyond the guided cases.
No two rows should reserve the same behaviour and condition.

| Member | First additional scenario | Second additional scenario |
| --- | --- | --- |
| 1 | | |
| 2 | | |
| 3 | | |
| 4, if present | | |
| 5, if present | | |
```

Remove unused member rows. Use short scenario descriptions, not just function names. Keep this shared table in the setup changes so everyone receives the same plan before starting individual branches.

### 5.6 Commit, push and merge

Save the files:

```bat
git add .gitignore requirements.txt pytest.ini docs/test-plan.md
git diff --staged
git commit -m "Add testing configuration and ignore rules"
git push -u origin setup/testing-files
```

`git add` selects changes. `git diff --staged` displays them. `-u` links the local branch to its GitHub branch.

On GitHub, open a PR with base `main` and compare `setup/testing-files`. Inspect Files changed, confirm only intended files appear, then merge.

The base is the destination. The compare branch contains proposed changes.

***

## 6. Prepare your branch and Python environment

### 6.1 Update and create your branch

Use your member number:

```bat
git switch main
git pull --ff-only origin main
git switch -c testing/member-1
git status
```

### 6.2 Create and activate the environment

```bat
python -m venv .venv
```

If only the Windows launcher works, use `py -3 -m venv .venv` instead.

```bat
.venv\Scripts\activate.bat
python -c "import sys; print(sys.executable)"
```

The path should contain this project's `.venv\Scripts\python.exe`.

Press Ctrl+Shift+P in VS Code, search for `Python: Select Interpreter` and select the Python inside `.venv`.

### 6.3 Install packages

```bat
python -m pip install -r requirements.txt
python -m pytest --version
python -m playwright --version
```

Wait for installation before the version commands. No Playwright browser download is needed for the installed Chrome or Edge used here.

### 6.4 Choose your browser for this terminal

Run one command.

Edge:

```bat
set "TEST_BROWSER=msedge"
```

Chrome:

```bat
set "TEST_BROWSER=chrome"
```

Check:

```bat
echo %TEST_BROWSER%
```

You should see `msedge` or `chrome`. This setting lasts only for the current Command Prompt session.

### 6.5 Create local folders

Create in VS Code:

```text
tests/
recordings/
reports/
```

Git does not store empty folders. Members may need to create them locally.

```bat
git status
git check-ignore .venv/
```

The second command should print `.venv/`. The environment should not appear as new files to commit.

> [!TIP]
> On another day, reopen the project, activate `.venv` and set `TEST_BROWSER` again. Continue your existing branch; do not recreate it.

***

## 7. Explore and run your first test

### 7.1 Try the task list manually

Open [Playwright TodoMVC](https://demo.playwright.dev/todomvc/).

1. Enter `Read testing notes` in `What needs to be done?`.
2. Press Enter and find the task.
3. Select its checkbox.
4. Try All, Active and Completed.

The automated browser uses a separate session. You do not need to clear your usual browser's tasks.


#### Manual observation and browser diagnostics

You chose actions and observed the result yourself. Next, automation will repeat predefined checks. Briefly notice whether the completion control is easy to find: a task-count assertion cannot decide whether the interface feels easy to use.

Right-click the task input and select Inspect. Find its `placeholder` attribute and compare it with `What needs to be done?`. Look at Console to see where messages appear; it may show no errors. Open Network and refresh once to see requests, then close Developer Tools. This is diagnostic exploration, not a performance test.

### 7.2 Create your personal file


#### Understand the test parameters

| Parameter | Add-task example |
| --- | --- |
| Scenario | Add one valid task. |
| Condition | A fresh session and empty list. |
| Values | `Read testing notes`. |
| Description | Open the page, fill the input and press Enter. |
| Expected outcome | One task with that text; input is empty. |

The assertions turn expected outcomes into checks. Actual results come from execution.


Member 1 creates `tests/test_member_1.py`. Use your number. Paste the complete code and save. Keep the indentation.

```python
from playwright.sync_api import Page, expect

URL = "https://demo.playwright.dev/todomvc/"


def test_add_task(page: Page):
    page.goto(URL)

    task_input = page.get_by_placeholder(
        "What needs to be done?",
        exact=True,
    )
    task_items = page.locator(".todo-list li")
    task_labels = task_items.locator("label")

    expect(task_items).to_have_count(0)

    task_input.fill("Read testing notes")
    task_input.press("Enter")

    expect(task_items).to_have_count(1)
    expect(task_labels).to_have_text(["Read testing notes"])
    expect(task_input).to_have_value("")
```

### 7.3 Run it

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed --slowmo 300
```

The browser opens, adds the task and closes. If all checks succeed, the terminal reports `1 passed`.

| Code or option | Meaning |
| --- | --- |
| `def test_add_task(...)` | Defines a test. pytest recognises `test_` function names. |
| `page` | A browser page supplied by the Playwright pytest package. |
| `page: Page` | A type hint that helps the editor understand `page`. |
| `page.goto(URL)` | Opens the website. |
| `get_by_placeholder(...)` | Finds the input by hint text. |
| `exact=True` | Requires the whole hint text to match. |
| `locator(".todo-list li")` | Finds task rows using a CSS selector. |
| `task_items.locator("label")` | Finds text labels in those rows. |
| `fill(...)` / `press("Enter")` | Enter text / submit it. |
| `to_have_count(...)` | Checks the number of rows. |
| `to_have_text([...])` | Checks expected labels. |
| `to_have_value("")` | Checks the input is empty. |
| `--headed` | Shows the browser. |
| `--slowmo 300` | Slows actions so you can watch. |

You can reuse the CSS selector without learning CSS first. Square brackets contain a list of expected labels. Playwright's page checks wait briefly for the expected condition; arbitrary pauses are not needed.

### 7.4 Commit and push

```bat
git add tests/test_member_1.py
git diff --staged
git commit -m "Add first task creation test"
git push -u origin testing/member-1
```

Use your filename and branch. The file is on your branch, not `main`, until merged.

***

## 8. Check task completion

Append below the first test, keeping earlier code:

```python
def test_complete_task(page: Page):
    page.goto(URL)

    task_input = page.get_by_placeholder(
        "What needs to be done?",
        exact=True,
    )
    task_items = page.locator(".todo-list li")

    expect(task_items).to_have_count(0)

    task_input.fill("Practise automated testing")
    task_input.press("Enter")

    expect(task_items).to_have_count(1)

    checkbox = task_items.first.get_by_role("checkbox")
    checkbox.check()
    expect(checkbox).to_be_checked()

    page.get_by_role("link", name="Completed", exact=True).click()

    expect(task_items).to_have_count(1)
    expect(task_items.locator("label")).to_have_text(
        ["Practise automated testing"]
    )
```

Save and run:

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed
```

If both succeed, the terminal reports `2 passed`.

`first` selects the first task row. `get_by_role("checkbox")` finds its checkbox. `check()` selects it, and `to_be_checked()` checks its state.

Each test gets a fresh browser session and creates its own task. It does not depend on an earlier test.

***

## 9. Run one test with different inputs

An empty or spaces-only task should not be added. This negative test passes when the list stays empty.


### Choose inputs for a reason

Equivalent testing, or equivalence partitioning, groups inputs expected to behave similarly. Meaningful task text is an accepted group; empty and whitespace-only text form a rejection group. The three blank values below are variations in one rejection group, not three distinct boundaries.

Sampling does not prove every possible input behaves identically. Boundary testing checks values at or next to a defined limit. No maximum task length is specified here, so do not invent one. Optional Section 16.8 explores lengths zero, one and two around the minimum non-empty length.

### 9.1 Add an import

At the top of your file, keep existing code and add:

```python
import pytest
```

### 9.2 Append the test

```python
@pytest.mark.parametrize(
    "task_text",
    ["", " ", "   "],
    ids=["empty", "one-space", "three-spaces"],
)
def test_blank_task_is_not_added(page: Page, task_text: str):
    page.goto(URL)

    task_input = page.get_by_placeholder(
        "What needs to be done?",
        exact=True,
    )
    task_items = page.locator(".todo-list li")

    expect(task_items).to_have_count(0)

    task_input.fill(task_text)
    task_input.press("Enter")

    expect(task_items).to_have_count(0)
```

The line starting with `@` runs the function once per input. This is parametrization.

| Part | Meaning |
| --- | --- |
| `""` | No characters. |
| `" "` | One space. |
| `"   "` | Three spaces. |
| `task_text` | Receives the current input. |
| `ids` | Gives each run a readable name. |
| `task_text: str` | A type hint saying the input is text. |

### 9.3 Run and commit

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed
```

Your two earlier tests and three input cases produce five runs. If all succeed, the terminal reports `5 passed`.

```bat
git add tests/test_member_1.py
git diff --staged
git commit -m "Add completion and blank input checks"
git push
```

***

## 10. Test a simple login

The task-list website has no login activity. Use [The Internet login demonstration](https://the-internet.herokuapp.com/login).

### 10.1 Try the login manually

The page publishes these practice details:

| Field | Value |
| --- | --- |
| Username | `tomsmith` |
| Password | `SuperSecretPassword!` |

Open the page, enter the practice details, click Login and find the Secure Area heading.

> [!IMPORTANT]
> These are public demonstration details, not personal credentials. Use them only on this practice site. Copy capital letters and the final exclamation mark carefully.

### 10.2 Append a successful-login test

Add below existing tests:

```python
def test_login_with_correct_details(page: Page):
    page.goto("https://the-internet.herokuapp.com/login")

    page.get_by_label("Username").fill("tomsmith")
    page.get_by_label("Password").fill("SuperSecretPassword!")
    page.get_by_role("button", name="Login").click()

    expect(
        page.get_by_role(
            "heading",
            name="Secure Area",
            exact=True,
        )
    ).to_be_visible()
```

| New code | Meaning |
| --- | --- |
| `get_by_label("Username")` | Find the field labelled Username. |
| `get_by_label("Password")` | Find the field labelled Password. |
| `get_by_role("button", name="Login")` | Find the Login button. |
| `get_by_role("heading", name="Secure Area", exact=True)` | Find the heading named exactly Secure Area. |
| `to_be_visible()` | Check it appears. |

Save and run only this test:

```bat
python -m pytest tests/test_member_1.py::test_login_with_correct_details --browser-channel %TEST_BROWSER% --headed --slowmo 300
```

The name after `::` selects one function. A successful run reports `1 passed`.

### 10.3 Append an incorrect-password test

```python
def test_login_with_incorrect_password(page: Page):
    page.goto("https://the-internet.herokuapp.com/login")

    page.get_by_label("Username").fill("tomsmith")
    page.get_by_label("Password").fill("WrongPassword123")
    page.get_by_role("button", name="Login").click()

    expect(
        page.get_by_text("Your password is invalid!")
    ).to_be_visible()

    expect(
        page.get_by_role("button", name="Login")
    ).to_be_visible()
```

This enters an incorrect password. Checks confirm the error appears and the Login button remains visible. The test passes when the website rejects the password.

### 10.4 Run all seven cases

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed
```

| Cases so far | Count |
| --- | ---: |
| Add a task | 1 |
| Complete a task | 1 |
| Blank inputs | 3 |
| Correct login | 1 |
| Incorrect password | 1 |
| Total | 7 |

If all succeed, the terminal reports `7 passed`. Each login test starts in its own fresh session and does not depend on the other.

```bat
git add tests/test_member_1.py
git diff --staged
git commit -m "Add correct and incorrect password login tests"
git push
```

***

## 11. Record and replay browser actions

### 11.1 Understand recording and replay

Codegen watches browser actions and creates Python code.

```text
Recording: You type and click → Codegen creates code
Replaying: You run the test → Playwright types and clicks
```

Use one scenario:

```text
Open the task list → Add “Try the recorder” → Check its text
```

Actions alone are not enough. An assertion checks the result.

### 11.2 Prepare the terminal

Use the project folder and active `.venv` in Command Prompt:

```bat
echo %TEST_BROWSER%
```

If needed, set it to `msedge` or `chrome` again. Check `recordings` exists.

### 11.3 Start Codegen

```bat
python -m playwright codegen --channel %TEST_BROWSER% --target python-pytest -o recordings/member_1.py https://demo.playwright.dev/todomvc/
```

Use your number.

| Part | Meaning |
| --- | --- |
| `codegen` | Start the recorder. |
| `--channel %TEST_BROWSER%` | Use your selected browser. |
| `--target python-pytest` | Create Python code for pytest. |
| `-o recordings/member_1.py` | Save generated code here. |
| Website address | Open this page. |

> [!IMPORTANT]
> Codegen uses `--channel`. pytest uses `--browser-channel`. These names are different.

### 11.4 Find the two windows

| Window | What to do |
| --- | --- |
| Browser opened by Codegen | Perform clicks and typing. |
| Playwright Inspector | Watch generated code. |

Move them so you can see both. Do not use another browser window for recording.

### 11.5 Record one task

1. Confirm the recording browser's list is empty.
2. Click `What needs to be done?`.
3. Type `Try the recorder`.
4. Press Enter.
5. Confirm it appears. Do not add more tasks.

Inspector should show navigation, input and Enter code. An extra click is fine.

### 11.6 Try recording a text check

1. Hover over toolbar buttons to read labels.
2. Find the text assertion control, usually `Assert text`.
3. Select it, then select `Try the recorder` on the page.
4. Confirm text if prompted.
5. Look for `expect(...)` in the code.

If the control is difficult to find, continue and add the check manually.

### 11.7 Finish and read the recording

Close the recording browser and Inspector. Wait for the terminal. Open `recordings/member_1.py` in VS Code.

Find the website address, entered text and Enter action. They may look like:

```python
page.get_by_placeholder("What needs to be done?").fill(
    "Try the recorder"
)
page.get_by_placeholder("What needs to be done?").press("Enter")
```

`get_by_placeholder()` finds the input, `fill()` enters text and `press()` submits it. Generated code may differ because Codegen can identify elements in different ways.

### 11.8 Make sure there is an assertion

If no task-text check exists, add inside the function after Enter:

```python
expect(page.locator(".todo-list li label")).to_have_text(
    ["Try the recorder"]
)
```

Match indentation and check `expect` is imported. If unsure, compare with this complete example or use it to replace the recording file:

```python
from playwright.sync_api import Page, expect


def test_recorded_task(page: Page):
    page.goto("https://demo.playwright.dev/todomvc/")

    task_input = page.get_by_placeholder(
        "What needs to be done?",
        exact=True,
    )
    task_input.fill("Try the recorder")
    task_input.press("Enter")

    task_labels = page.locator(".todo-list li label")
    expect(task_labels).to_have_text(["Try the recorder"])
```

This checks labels against a list containing the expected task. Save the file.

### 11.9 Replay

```bat
python -m pytest recordings/member_1.py --browser-channel %TEST_BROWSER% --headed --slowmo 300
```

The browser opens, enters the task, checks it and closes. If this one test succeeds, the terminal reports `1 passed`.

A successful run containing only actions does not explicitly check task text. Including an assertion checks the result.

Keep this recording in ignored `recordings/`. It does not increase the count in your file under `tests/`.

> [!TIP]
> If replay fails, compare input and expected text, check only one task was added and use the complete example if needed. See Section 17.9 for recording problems.

***

## 12. Use a helper to add two tasks

A helper is simply a Python function used to repeat useful steps.

### 12.1 Add the helper

Put this helper and the test in Section 12.2 in your same personal file. Both `def` lines must start at the left edge, outside every other function. Save before running.

Put both this helper and the test in Section 12.2 in the same personal file. Both `def` lines must start at the left edge, outside every other function.

Append to your personal file, keeping existing code:

```python
def add_task(page: Page, task_name: str):
    task_input = page.get_by_placeholder(
        "What needs to be done?",
        exact=True,
    )
    task_input.fill(task_name)
    task_input.press("Enter")
```

`task_name` supplies the text. This function does not open the website or check results. Its name does not start with `test_`, so pytest does not treat it as a test.

### 12.2 Add the test

Append below the helper:

```python
def test_add_two_tasks(page: Page):
    page.goto(URL)
    task_items = page.locator(".todo-list li")

    expect(task_items).to_have_count(0)

    add_task(page, "Read the instructions")
    add_task(page, "Practise the examples")

    expect(task_items).to_have_count(2)
    expect(task_items.locator("label")).to_have_text(
        ["Read the instructions", "Practise the examples"]
    )
```

This opens the page, calls the helper twice and checks count and names. A count alone does not confirm the names.

### 12.3 Run all eight cases

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed
```

If all succeed, the summary reports `8 passed`. The helper is not an extra case; the two-task test adds one.

```bat
git add tests/test_member_1.py
git diff --staged
git commit -m "Add helper and two task creation test"
git push
```


### 12.4 Create two different tests of your own

Allow about 20 minutes. Every member creates two additional tests in their own file. Start with one, run it, then work on the second.

Your tests must:

- Check two different behaviours or clearly different conditions.
- Add checks beyond the eight guided cases.
- Be different from the two scenarios chosen by every other member in your group.
- Include their own setup and meaningful assertions.

Uniqueness is within your group. You do not need to coordinate with the whole class. The original eight guided cases remain the same for everyone.

> [!IMPORTANT]
> A different filename, function name, member number or task wording does not by itself make a test unique. The behaviour, condition or expected outcome must be meaningfully different.
>
> Changing only `Read notes` to `Read a book` in the guided add-task test does not count as one of your two additional tests.

#### Step 1: Agree two scenarios per member

Use the shared table in `docs/test-plan.md`, created during setup. Discuss choices before coding. The coordinator records two different scenarios per member before merging that setup file.

This is an allocation aid, not a separate findings report. Do not have every member edit the shared table on separate branches. If an idea changes later, agree the change with the group and let one nominated member update the shared plan on a branch.

Choose your own ideas or use these starting points:

| Scenario idea | What makes it different | Possible result to check |
| --- | --- | --- |
| Save an edited task with Enter | Changes an existing task rather than adding one. | Updated name appears and old name is absent. |
| Cancel an edit with Escape | Cancels a change rather than saving it. | Original task name remains. |
| Delete an active task | Removes an unfinished task. | Selected task disappears and another task remains. |
| Delete a completed task | Removes a finished task. | Selected completed task disappears. |
| Clear completed tasks from a mixed list | Removes completed items together. | Active tasks remain and completed tasks are gone. |
| Mark all tasks complete | Uses the whole-list control. | All prepared tasks are completed. |
| Mark all tasks active again | Reverses whole-list completion. | Prepared tasks are no longer completed. |
| Active filter on a mixed list | Checks exclusion of completed tasks. | Only the unfinished task names are visible. |
| Completed filter on a mixed list | Checks exclusion of active tasks, beyond the guided one-task example. | Only completed task names are visible. |
| Return to All from a filtered mixed list | Checks the full list is restored. | All prepared task names appear. |
| Refresh after adding tasks | Checks persistence in the same test session. | Previously added task names remain after reload. |
| Add repeated names | Checks whether two identical names are retained. | Both expected rows appear. |
| Leading and trailing spaces | Checks text normalization, not merely a different task name. | Displayed text follows the observed and agreed trimming rule. |
| Incorrect username with the practice password | Checks a different login rejection condition. | Expected username error appears and login is not completed. |

The table gives exploration ideas, not guaranteed outcomes for every future version of the public sites. Try the chosen behaviour manually and confirm the expected result before coding. If a rule is unclear, choose a clearer scenario or state the assumption honestly; do not invent a requirement.

For a five-member group, reserve ten distinct scenarios. You do not have to use every idea in the table.

#### Step 2: Try the first scenario manually

1. Open the relevant demonstration website.
2. Perform the actions once.
3. Notice which controls are used and what appears.
4. Decide which result your test will check.

Keep it small. Use the same fictional practice data and public login details already used in the guide.

#### Step 3: Identify the test parameters

Use short comments inside your test if useful:

```text
Scenario: Active shows unfinished tasks only.
Condition: A fresh session with an empty list.
Values: “Read a chapter” and “Write a summary”.
Description: Add both, complete the first, then select Active.
Expected outcome: Only “Write a summary” is displayed.
```

This is an example plan, not Python code. You do not need a separate document for each test.

#### Step 4: Add your first test

Append a uniquely named function to your personal file. For example:

```python
def test_active_filter_shows_unfinished_task(page: Page):
    page.goto(URL)

    # Add the setup and actions for your scenario.

    # Add assertions for the expected result.
```

> [!IMPORTANT]
> This skeleton is not a finished test. Without assertions, it may pass while checking nothing useful. Add the actions and at least one meaningful assertion before treating it as complete.

Keep `def` at the left edge and indent its instructions by four spaces. Keep the existing imports, `URL`, helper and guided tests.

#### Step 5: Reuse familiar code

| What you need | Pattern to reuse |
| --- | --- |
| Open task list | `page.goto(URL)` |
| Add a task | `add_task(page, "A fictional task")` |
| Find rows | `page.locator(".todo-list li")` |
| Complete a task | Checkbox code in Section 8. |
| Select a filter | The Completed-link action; change the name to the intended link. |
| Check count | `expect(task_items).to_have_count(...)` |
| Check names | `expect(task_items.locator("label")).to_have_text([...])` |

Replace `...` with meaningful expected values. These incomplete reference expressions are not finished checks.

If you call `add_task(...)`, the complete helper must exist in this same file, outside every test. It is not a built-in Playwright command.

Use Codegen to identify unfamiliar actions. Read the generated code and add meaningful assertions. Each test gets a fresh session: prepare everything it needs inside that test rather than relying on another test.

#### Step 6: Run only the first new test

Save with Ctrl+S. Use your member number and actual function name:

```bat
python -m pytest tests/test_member_1.py::test_active_filter_shows_unfinished_task --browser-channel %TEST_BROWSER% --headed --slowmo 300
```

Watch the browser and read the result. A passing result is useful only if the assertions check the intended behaviour.

If it fails, read the failing line, confirm the correct page loaded and compare the actions and expected values with your manual attempt. Change one thing at a time. Use Section 17 rather than deleting checks to obtain a pass.

#### Step 7: Add and run your second distinct test

Use the second reserved scenario. Give it a different descriptive `test_` name, its own setup and meaningful assertions. It must not depend on the first new test having run.

Briefly compare choices with your group again. If two members accidentally covered the same scenario, agree a different one before combining the files.

Use one ordinary test function for each of your two scenarios in this activity. Save more parametrized examples for post-lesson practice so the main count stays simple.

#### Step 8: Run your complete personal file

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed
```

With the eight guided cases unchanged and two completed additional functions, your personal file contains ten cases. If all checks succeed, the terminal reports `10 passed`.

Do not add a dummy test, rename a guided test or remove an assertion just to reach ten. The two extra cases must perform the two distinct checks you chose.

If you need longer, save your work and finish both scenarios after the lesson before merging your completed contribution. An unfinished draft can stay in a clearly labelled local file under ignored `recordings/` while you work on it. Do not merge empty or incomplete test functions that silently pass.

#### Step 9: Commit and push working source

```bat
git add tests/test_member_1.py
git diff --staged
git commit -m "Add two distinct browser behaviour tests"
git push
```

Use your filename. In your PR description, name your two scenarios so the group can compare them with `docs/test-plan.md`.

***

## 13. Create a report and capture screenshots


### Why rerun earlier checks?

Regression testing checks that existing behaviour still works after a change. In a real application, these checks could be rerun after application changes. Here, rerunning after changes to your test code also checks that the collection still works. We do not control releases of the public sites, so this is not a controlled application-change experiment.

Compare actual results with expected outcomes, not just screenshot appearance. A red failure may come from the application, test code or environment; investigate before calling it an application defect. A screenshot supports investigation but does not replace an assertion.


### 13.1 Run with automatic screenshots

Check `reports` exists:

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --screenshot on --output test-results/member-1 --html=reports/member-1.html --self-contained-html
```

| Option | Meaning |
| --- | --- |
| `--screenshot on` | Save each test's final page, whether it passes or fails. |
| `--output test-results/member-1` | Choose the browser-output folder. |
| `--html=reports/member-1.html` | Create an HTML results report. |
| `--self-contained-html` | Keep supporting report-page resources in its HTML file; this does not automatically embed separately saved screenshots. |

This runs without displaying the browser. Add `--headed` to watch.

### 13.2 Open the report

In Windows File Explorer, open your project, open `reports` and double-click `member-1.html`. Find names, results, durations and errors.

### 13.3 Open screenshots

In VS Code:

1. Open `test-results/member-1`.
2. Open a generated test subfolder.
3. Click the screenshot.
4. Find correct-login and incorrect-password screenshots.
5. Compare the Secure Area page with the rejected-login page.

Subfolder names may be long. Find them rather than guessing.

A screenshot shows the browser page, not the entire desktop or terminal summary.

> [!IMPORTANT]
> Assertions check behaviour. Screenshots provide pictures; they do not replace assertions. Reports and images are separate outputs here. Both stay local through `.gitignore`. Later runs using the same output location may replace browser output.

### 13.4 Failure-only screenshots

For later troubleshooting, replace `--screenshot on` with `--screenshot only-on-failure`. If all tests pass, no failure screenshots are expected.

***

## 14. Combine the group files

All tests are started manually on your computer. Pushing and merging do not trigger tests automatically: no GitHub Actions or other CI/CD workflow is configured. The slide decks describe how these tests could later fit into continuous testing.


### 14.1 Check and push

```bat
git status
git push
```

If intended source changes remain, run your file, add it, inspect staged changes, commit and push. Do not add reports, environments, recordings or screenshots.

### 14.2 Open and merge your PR

On GitHub:

1. Open a PR from your personal branch to `main`.
2. Use a title such as `Add Member 1 browser tests`.
3. Look through Files changed with another member.
4. Check changes belong to your file, all eight guided cases remain, your two additional scenarios match the group plan and are not duplicated by another member, assertions are meaningful, and no private data or local outputs appear.
5. Merge one member's PR at a time.

Separate filenames allow all files to sit beside each other. Do not edit another member's file during this activity.

### 14.3 Everyone: update main

Start with a clean working directory. Commit intended changes on your branch before switching.

```bat
git switch main
git pull --ff-only origin main
git status
```

You should see merged member files. A GitHub merge does not update your computer automatically.

### 14.4 Run the combined project once

Choose one member to run:

```bat
python -m pytest --browser-channel %TEST_BROWSER% --html=reports/group-results.html --self-contained-html
```

After every member completes the eight guided cases and their two additional tests:

| Members | Executions in the group suite |
| --- | ---: |
| 3 | 30 |
| 4 | 40 |
| 5 | 50 |

Each personal file contributes ten executions before optional additions. Check the actual collected count; extra parametrized or optional cases change it.

Execution count is not unique functional coverage. The eight guided cases are deliberately repeated in member files; each member's two additional scenarios are different within the group.

Do not rerun the whole suite repeatedly without a reason. Diagnose a failing test by its file and function name, fix it on a new branch and combine the correction through a PR. Continue longer investigations after the lesson if necessary.


***

## 15. Simple syntax reference

Refer to this as needed; you do not need to memorise it.

### Find something

| Syntax | Meaning |
| --- | --- |
| `page.get_by_label("Username")` | Find a field by its label. |
| `page.get_by_placeholder("What needs to be done?")` | Find an input by hint text. |
| `page.get_by_role("button", name="Login")` | Find a button by name. |
| `page.get_by_role("link", name="Completed")` | Find a link by name. |
| `page.get_by_role("heading", name="Secure Area")` | Find a heading by name. |
| `page.get_by_text("Your password is invalid!")` | Find an element containing this text. |
| `page.locator(".todo-list li")` | Find task rows with the supplied selector. |

### Perform an action

| Syntax | Meaning |
| --- | --- |
| `page.goto("https://example.com")` | Open a website. |
| `field.fill("Some text")` | Replace field text. |
| `field.press("Enter")` | Press Enter in that field. |
| `button.click()` | Click the button. |
| `checkbox.check()` | Select the checkbox. |

The variable names above need locators assigned first. For example:

```python
username_field = page.get_by_label("Username")
username_field.fill("tomsmith")
```

The same action on one line:

```python
page.get_by_label("Username").fill("tomsmith")
```

### Check a result

| Syntax | Meaning |
| --- | --- |
| `expect(item).to_be_visible()` | Check the item is visible. |
| `expect(checkbox).to_be_checked()` | Check the checkbox is selected. |
| `expect(items).to_have_count(1)` | Check exactly one item matches. |
| `expect(labels).to_have_text(["Read testing notes"])` | Check labels match this expected list. |
| `expect(field).to_have_value("")` | Check the input is empty. |

```text
expect(something).check_the_expected_result()
```

***

## 16. Optional post-lesson practice

Suggested times are planning guides, not limits.

| Activity | Suggested time | Focus |
| --- | --- | --- |
| 16.1 Investigate a deliberate failure | 15–20 minutes | Errors, screenshots and traces. |
| 16.2 Capture a page at a chosen step | 5–10 minutes | Screenshot code. |
| 16.3 Add a logout test | 10–15 minutes | Login followed by logout. |
| 16.4 Add input examples | 10–15 minutes | Parametrization. |
| 16.5 Try another browser | 10–15 minutes, plus downloads | Reuse tests. |
| 16.6 Improve a recording | 15–20 minutes | Useful shared code. |
| 16.7 Inspect page elements and history | 10 minutes | Connect locators and changes. |

Before changing source again, update clean `main` and create a new branch:

```bat
git switch main
git pull --ff-only origin main
git switch -c practice/member-1-follow-up
```

Use your number. Continue that branch on later sessions rather than recreating it. Run personal tests after changes, then commit, push and combine through a PR.

### 16.1 Investigate a deliberate failure

Temporarily change the task-text expectation in `test_add_task()` to:

```python
expect(task_labels).to_have_text(["A different task"])
```

Do not change input. Run:

```bat
python -m pytest tests/test_member_1.py::test_add_task --browser-channel %TEST_BROWSER% --headed --screenshot only-on-failure --tracing retain-on-failure --output test-results/member-1-failure
```

The test should fail because input and expectation differ. Find both in the error. Here the expectation is wrong; the failure does not demonstrate a website defect.

Open the generated test subfolder inside `test-results/member-1-failure` and its screenshot. Find `trace.zip`, right-click and Copy Relative Path. Replace the placeholder:

```bat
python -m playwright show-trace "PASTE_RELATIVE_PATH_HERE" --browser-channel %TEST_BROWSER%
```

Look through navigation, text entry, Enter and the failed check. Restore:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

Save and rerun your file. With the eight guided cases and both completed individual tests, success reports `10 passed`. Optional additions change the total.

```bat
git diff
```

If restored exactly, no extra commit may be needed. Never commit the deliberate mistake or delete the assertion to hide it.

### 16.2 Capture a page at a chosen step

Create `test-results` first if missing. Put this inside the correct-login test, after its heading assertion:

```python
page.screenshot(
    path="test-results/member-1-login-success.png",
    full_page=True,
)
```

Match indentation and use your number. `path` gives the filename; `full_page=True` captures the full scrollable page. An earlier failed assertion prevents this line running, so automatic failure screenshots remain useful. Rerunning replaces this image.

### 16.3 Add a logout test

Append a new test, keeping existing imports and tests:

```python
def test_logout_after_login(page: Page):
    page.goto("https://the-internet.herokuapp.com/login")

    page.get_by_label("Username").fill("tomsmith")
    page.get_by_label("Password").fill("SuperSecretPassword!")
    page.get_by_role("button", name="Login").click()

    expect(
        page.get_by_role("heading", name="Secure Area", exact=True)
    ).to_be_visible()

    page.get_by_role("link", name="Logout").click()

    expect(page.get_by_label("Username")).to_be_visible()
    expect(page.get_by_label("Password")).to_be_visible()
    expect(page.get_by_role("button", name="Login")).to_be_visible()
```

This logs in for itself and adds one case.

### 16.4 Add a blank-input example

Replace only the parametrization block above the blank-input function:

```python
@pytest.mark.parametrize(
    "task_text",
    ["", " ", "   ", "    "],
    ids=["empty", "one-space", "three-spaces", "four-spaces"],
)
```

Keep the function unchanged. There is one ID per input. This adds one case; your total depends on other additions.

### 16.5 Try another browser

For the other installed main browser, change `TEST_BROWSER` and rerun.

For managed browsers, these commands override shared `addopts` for that run. Do not attach Chrome or Edge channels to Firefox or WebKit.

Chromium:

```bat
python -m playwright install chromium
python -m pytest tests/test_member_1.py -o "addopts=-v" --browser chromium --headed
```

Firefox:

```bat
python -m playwright install firefox
python -m pytest tests/test_member_1.py -o "addopts=-v" --browser firefox --headed
```

WebKit:

```bat
python -m playwright install webkit
python -m pytest tests/test_member_1.py -o "addopts=-v" --browser webkit --headed
```

Ordinary Firefox does not replace Playwright Firefox. Playwright WebKit is not installed Safari. Skip unsupported or blocked options. Compare functional results, not browser speed. After upgrading Playwright, reinstall managed browsers if used, not ordinary Chrome or Edge.

### 16.6 Improve a recording

Try editing or deleting a task manually. Record it, read the code, remove unnecessary actions and add an assertion.

Keep experiments in ignored `recordings/`. To share, copy a working test into your own file under `tests/`, choose a unique `test_` name, run, commit and push, then combine through a PR. If expected behaviour is unclear, treat it as an observation rather than a confirmed defect.

### 16.7 Inspect elements and history

Right-click the task input and select Inspect. Find `placeholder="What needs to be done?"` and compare it with `get_by_placeholder(...)`.

```bat
git log --oneline --graph --decorate --all -15
```

Use an actual commit ID:

```bat
git show COMMIT_ID
```

Press `q` if Git opens a scrolling view.


### 16.8 Explore minimum-length boundary examples

The slides describe checking values at and next to a defined boundary. For non-whitespace task text, compare lengths zero, one and two. Do not assume a maximum length that the site has not specified.

| Input | Length | Expected result for this exercise |
| --- | ---: | --- |
| `""` | 0 | No task is added. |
| `"A"` | 1 | One task labelled A appears. |
| `"AB"` | 2 | One task labelled AB appears. |

Try these manually, then use earlier patterns to automate them. One character is the minimum non-empty length explored here. Spaces-only text is another validation consideration. Repeating the empty case adds an execution, not a wholly new behaviour. Optional additions change your total beyond ten.

### 16.9 Compare a built-in Python tool

The tools slides include Python's built-in `unittest`. Create `examples/builtin_unittest_example.py` in a new `examples` folder:

```python
import unittest


def clean_task_name(text: str):
    return text.strip()


class TestCleanTaskName(unittest.TestCase):
    def test_removes_outer_spaces(self):
        self.assertEqual(clean_task_name("  Read notes  "), "Read notes")

    def test_keeps_normal_text(self):
        self.assertEqual(clean_task_name("Read notes"), "Read notes")

    def test_spaces_become_empty_text(self):
        self.assertEqual(clean_task_name("   "), "")


if __name__ == "__main__":
    unittest.main()
```

Run:

```bat
python examples/builtin_unittest_example.py
```

`self.assertEqual(actual, expected)` compares values. `unittest.TestCase` supplies assertion methods; `self` refers to the current test object. If all three succeed, the output reports three tests and `OK`.

No browser opens. This checks the local function in this file, not TodoMVC's implementation, and does not change your personal browser-case count. It contrasts a built-in local unit-testing tool with external pytest and Playwright browser checks. The separate pytest self-help guide offers more local-function practice.

***

## 17. Troubleshooting common errors

Use this section when a step does not work. You do not need to read it all before starting.

### 17.1 Start with five checks

1. Save the file with Ctrl+S.
2. Read the error before changing anything.
3. Check you are in the cloned project folder.
4. Check Python is running from `.venv`.
5. Check your branch and chosen browser.

In Command Prompt:

```bat
cd
python -c "import sys; print(sys.executable)"
git status
echo %TEST_BROWSER%
```

Expected:

| Check | Expected result |
| --- | --- |
| Folder | Your cloned project folder, not its parent or just `tests`. |
| Python | A path containing this project's `.venv\Scripts\python.exe`. |
| Git | Your intended branch and a list of current changes. |
| Browser | `chrome` or `msedge`. |

Change one thing at a time, then rerun only the affected test. Do not repeatedly run the entire group suite while diagnosing one problem.

### 17.2 Python is not recognised

You may see:

```text
'python' is not recognized as an internal or external command
```

Meaning: Windows cannot find Python through that command.

Try:

1. Close and reopen VS Code after installation.
2. Run `py -3 --version`.
3. If that works, create the environment with `py -3 -m venv .venv`.
4. Activate it and run `python --version` again.
5. If neither works, review the approved Python installation from Section 1.

If `python` opens the Microsoft Store instead, use the working Python launcher or approved installation rather than assuming Python is ready.

### 17.3 Environment activation or package import fails

#### Activation path cannot be found

Check your folder with `cd` and confirm `.venv` exists in VS Code. If it has not been created, run the environment-creation step once.

Use Command Prompt:

```bat
.venv\Scripts\activate.bat
```

If PowerShell reports scripts are disabled, open Command Prompt instead. Do not change execution policy for this practical.

Alternatively run the environment's Python directly:

```bat
.venv\Scripts\python.exe -m pytest --version
```

#### `No module named pytest` or `No module named playwright`

Meaning: the Python being used cannot find the package.

```bat
python -c "import sys; print(sys.executable)"
python -m pip install -r requirements.txt
```

Check the Python path first. If wrong, activate `.venv` and repeat. In VS Code, also select the interpreter inside `.venv`.

#### `unrecognized arguments: --browser-channel ...` or `--screenshot ...`

Check that `pytest-playwright` is installed in this environment:

```bat
python -m pip show pytest-playwright
```

If missing, repeat installation from `requirements.txt`.

If `--html` or `--self-contained-html` is unrecognised, check:

```bat
python -m pip show pytest-html
```

Install the listed requirements in the active environment. Do not remove useful options just to silence the error.

### 17.4 Browser choice is rejected

You may see:

```text
argument --browser: invalid choice: 'chrome'
```

Meaning: a browser channel was supplied where pytest expects a browser family.

Check `pytest.ini`:

```ini
[pytest]
testpaths = tests
addopts = -v --browser chromium
```

Then use:

```bat
python -m pytest tests/test_member_1.py --browser-channel chrome --headed
```

For Edge, replace `chrome` with `msedge`. Both use the `chromium` family.

With the guide's variable:

```bat
set "TEST_BROWSER=chrome"
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed
```

Do not write `--browser %TEST_BROWSER%`.

### 17.5 Browser variable or executable is missing

#### Variable prints as `%TEST_BROWSER%`

Run one of these in the same Command Prompt terminal:

```bat
set "TEST_BROWSER=chrome"
```

or:

```bat
set "TEST_BROWSER=msedge"
```

Then `echo %TEST_BROWSER%` should show the value. Set it again whenever you open a new terminal. If the terminal uses PowerShell, switch to Command Prompt before using these commands.

#### Chrome or Edge executable cannot be found

1. Confirm the chosen stable browser opens from Windows Start.
2. Check the channel is `chrome` or `msedge`, with correct spelling.
3. If unavailable, use the other installed and approved browser.
4. Use approved installation methods if a browser needs installing.

#### Error points to missing Playwright Chromium

For the main activities, check you included the installed-browser channel. You do not need to download managed Chromium just to repair an omitted channel.

- pytest: `--browser-channel %TEST_BROWSER%`
- Codegen: `--channel %TEST_BROWSER%`

#### Browser is blocked by policy

Use an approved alternative or approved IT process. Do not bypass browser policies or disable security controls.

### 17.6 No tests or the wrong number of tests

#### `file or directory not found`

Check the current project folder, `tests` folder, member number and exact filename. Make sure it is `.py`, not `.py.txt`.

#### `no tests ran`

1. Save the file.
2. Confirm the file is named `test_member_1.py`, using your number.
3. Confirm test functions begin with `test_`.
4. Confirm they are not accidentally indented inside another function.
5. Confirm you are running the intended file.

List cases without opening a browser:

```bat
python -m pytest tests/test_member_1.py --collect-only
```

#### Unexpected number of cases

With only the main examples, expect:

```text
Add one task                         1
Complete one task                    1
Blank inputs                         3
Correct login                        1
Incorrect password                   1
Add two tasks                        1
Total                                8
```

Check you kept earlier tests when appending code. Each function in one file must have a different name; a later duplicate definition can replace an earlier one. The helper `add_task` is not a test. After Section 12.4, your two distinct additional functions bring the personal total to ten before optional additions.

Optional tests increase the total. Running without a filename selects the group suite, not just your file. The separate recording is not included by the configured `testpaths = tests`.

### 17.7 Python code errors

| Error | Meaning | What to check |
| --- | --- | --- |
| `IndentationError` | Leading spaces are incorrect. | Use four spaces inside functions and match the complete example. |
| `SyntaxError` | Python cannot read the code structure. | Check missing quotes, brackets, colons and copied Markdown backticks. |
| `NameError: name 'expect' is not defined` | The assertion tool was not imported. | Keep `from playwright.sync_api import Page, expect` at the top. |
| `NameError: name 'pytest' is not defined` | Parametrization needs the pytest import. | Add `import pytest` at the top. |
| `NameError: name 'URL' is not defined` | The shared website variable is missing. | Keep the provided `URL = ...` line above the tests. |
| `NameError: name 'add_task' is not defined` | The helper is missing, misspelled or inside another function. | Keep the complete helper in the same file as the test. Put its `def` at the left edge and save with Ctrl+S. |
| `fixture 'task_text' not found` | pytest is not receiving parameter values. | Keep the `@pytest.mark.parametrize(...)` block immediately above the correct function and match `task_text` in both. |

Fix the indicated line, but also inspect the line immediately above it. An unclosed bracket or quote can cause the next line to be reported.

### 17.8 Page, locator, login or assertion failures

#### Navigation error or page cannot load

1. Open the exact practice URL manually.
2. Check internet access and approved network settings.
3. If the demonstration site is unavailable, save and retry later.
4. Do not invent a passing result or change to an unrelated website.

#### `TimeoutError` while finding or using an element

Meaning: Playwright did not complete an action before its time limit.

Check:

1. Did the correct page load?
2. Does the locator text match the actual page?
3. Did the preceding action reach the expected page?
4. Is a site error or network problem showing instead?

Run only the affected test visibly. For example:

```bat
python -m pytest tests/test_member_1.py::test_login_with_correct_details --browser-channel %TEST_BROWSER% --headed --slowmo 300
```

Do not immediately add `time.sleep()` or increase timeouts. First find what the test is waiting for.

#### `strict mode violation` or multiple matching elements

Meaning: an action or single-element check expected one match but found several.

Use the exact role, label or supplied selector from the example. Check extra tasks were not recorded. Use `exact=True` when the example uses it. Do not blindly add `.first` to hide ambiguity.

#### Assertion says expected text differs

Compare input and expected text, including capital letters and spaces. Keep an honest expectation: do not delete the assertion or copy an incorrect result into it just to pass.

#### Correct-login test fails

Check the page is the demonstration login page and the exact values are:

```text
Username: tomsmith
Password: SuperSecretPassword!
```

The final `!` matters. Check the browser's displayed result and terminal error.

#### Incorrect-password test reports passed

This is expected if the website rejected the password and the assertions succeeded. A negative test is not supposed to report a failure when the website behaves correctly.

### 17.9 Recording problems

| Problem | What to try |
| --- | --- |
| Codegen rejects `--browser-channel` | Use Codegen's `--channel` option instead. |
| Recorder opens but no code appears | Use the browser opened by Codegen and check recording is active. |
| Cannot find Assert text | Use the manual assertion and complete example in Section 11.8. |
| Recording adds extra tasks | Remove accidental repeated actions or start a new short recording. |
| Recording replay fails but manual actions worked | Read the generated actions and assertion; check text, order and extra steps. |
| Recorder file missing | Check `recordings` exists, the member number and the output path in the command. |
| Terminal will not accept a new command | Finish and close recording windows first; the recorder may still be running. |

The recorder generates starting code, not a guaranteed complete test. Read it and include a useful check.

### 17.10 Reports, screenshots and trace problems

| Problem | Meaning and next step |
| --- | --- |
| No browser window while creating a report | Expected when `--headed` is omitted. Read the terminal result. |
| Browser closes after the test | Normal cleanup. The result remains in the terminal and generated outputs. |
| No screenshot for a passing test | Use `--screenshot on`. Failure-only mode saves none for passing tests. |
| No screenshot after a command-line or syntax error | Browser execution may never have started. Fix setup or code errors first. |
| HTML report contains no screenshot | Open separate images under `test-results`. They are not embedded automatically. |
| Cannot find output | Check the `--output` and `--html` paths and member number. |
| Old report still displayed | Check the latest run completed and reopen or refresh the correct local file. |
| Earlier screenshots disappeared | Later runs can replace browser output. Copy locally first if you need to keep it. |
| No `trace.zip` | Use `--tracing retain-on-failure` and reproduce a failure. A passing run does not retain a failure-only trace. |
| Trace path contains spaces | Put the full copied path in quotation marks. |
| Handwritten screenshot line did not run | A failed earlier assertion may have stopped execution before it. Use automatic failure screenshots. |

If a report folder is missing, create `reports` in the project and rerun the report command. Do not move outputs into `tests` just to make them visible.

### 17.11 Git identity, access and branch problems

#### `Author identity unknown`

Set the commit identity from Section 1.4 with your own details, then retry the commit. Do not use another member's identity.

#### `not a git repository`

You are outside the cloned repository. Open the actual project folder in VS Code and a new terminal. Run `git status` again.

#### `repository not found` or authentication failed

Check the copied HTTPS URL, GitHub sign-in and accepted collaborator invitation. Repository access and Git commit identity are different settings.

#### Branch already exists

If continuing your existing work, select rather than recreate it:

```bat
git switch testing/member-1
```

Use `git status` first and your number. Do not delete the branch simply to repeat an earlier command.

#### Branch has no upstream

For the first push on your personal branch:

```bat
git push -u origin testing/member-1
```

Later pushes on that branch can use `git push`.

#### `nothing to commit`

Save your file. Check `git status` and `git diff`. It may already be committed, unchanged or ignored. Select the intended source file with `git add` only if it has changes.

#### Push rejected because the remote contains new work

Stop and inspect:

```bat
git status
git branch --show-current
git fetch origin
git log --oneline --graph --decorate --all -15
```

Confirm no one else is using your personal branch. Coordinate before combining remote changes. Do not force-push or delete local work to bypass rejection.

#### Merged files do not appear locally

From clean local `main`:

```bat
git pull --ff-only origin main
```

A merge on GitHub does not update computers automatically.

### 17.12 `.gitignore` does not appear to work

```bat
git check-ignore -v .venv/
```

If no rule appears, check `.gitignore` is saved in the project root and is not `.gitignore.txt`.

If files were selected but not committed, unselect without deleting:

```bat
git restore --staged .venv/
```

If a non-sensitive local-only folder was committed, stop tracking it but keep your local copy:

```bat
git rm -r --cached .venv/
git status
git diff --staged
```

Use the actual unwanted local-only folder, never a source folder. Review before committing on your branch:

```bat
git add .gitignore
git commit -m "Stop tracking local Python environment"
git push
```

Combine through a PR. This removes current tracking, not earlier history.

> [!WARNING]
> If private credentials were committed, ignore rules or later deletion are not a complete fix. Stop sharing affected content and use the relevant account or organisation process to revoke exposed credentials and handle the disclosure.

### 17.13 Switching branches or merging is blocked

#### Local changes would be overwritten

Do not discard them. Run `git status` and `git diff`. Save intended source changes in a commit on your work branch before switching.

#### Merge conflict

Use `git status` to identify state and conflicting files. Compare versions with the file's owner. Keep intended content, remove markers such as `<<<<<<<`, `=======` and `>>>>>>>`, save and run relevant tests.

For a local merge in progress, after resolving files:

```bat
git add PATH_TO_RESOLVED_FILE
git diff --staged
git commit
```

Replace the placeholder with the actual file. Follow Git's displayed instructions; do not run these blindly outside a merge.

To return to the state before an unresolved local merge, use `git merge --abort` only when `git status` confirms a merge is in progress.

If `git pull --ff-only` refuses because histories diverged, it has not started a merge. Preserve commits and inspect history before deciding how to combine changes. Do not use a destructive reset or force-push.

### 17.14 If you still cannot continue

1. Save your source files.
2. Keep the exact command and complete error message.
3. Note the filename, branch and selected browser.
4. Compare the affected step with the guide and another group member's working setup.
5. Keep private details out of anything you share.

Do not delete the project, reinstall everything or remove assertions as a first response. If the issue requires administrator permissions or managed-browser changes, use approved IT support. Otherwise, preserve progress and return to the specific blocked step.

***

## 18. Quick command reference

Run from the cloned project folder in Command Prompt with `.venv` active. Use your member number.

| Goal | Command |
| --- | --- |
| Choose Edge | `set "TEST_BROWSER=msedge"` |
| Choose Chrome | `set "TEST_BROWSER=chrome"` |
| Check browser choice | `echo %TEST_BROWSER%` |
| Watch personal tests | `python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed --slowmo 300` |
| Run without a visible browser | `python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER%` |
| List cases without browser execution | `python -m pytest tests/test_member_1.py --collect-only` |
| Inspect changes | `git diff` |
| Select source | `git add tests/test_member_1.py` |
| Inspect selected changes | `git diff --staged` |
| Save selected changes | `git commit -m "Describe the change"` |
| Upload commits | `git push` |

### Report and screenshots

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --screenshot on --output test-results/member-1 --html=reports/member-1.html --self-contained-html
```

### Record

```bat
python -m playwright codegen --channel %TEST_BROWSER% --target python-pytest -o recordings/member_1.py https://demo.playwright.dev/todomvc/
```

### Replay

```bat
python -m pytest recordings/member_1.py --browser-channel %TEST_BROWSER% --headed --slowmo 300
```

***

## Closing reminder

A passing test means its particular checks succeeded in that run. It does not prove the whole website is error-free.

Keep examples small and understandable. Use failures to understand what happened. Share working source without uploading private data or local browser outputs.

```text
Choose a behaviour → Define the expectation → Automate → Run
                   → Inspect → Improve → Commit → Push → Merge
```
