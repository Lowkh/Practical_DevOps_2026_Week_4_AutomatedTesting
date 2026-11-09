# Automated Testing Tools Team Practical

> A guided, hands-on introduction to browser automation and testing tools for students with basic Python knowledge and no previous automated testing experience.

> [!NOTE]
> ## Educational Practice Repository
>
> This repository supports introductory practice with automated testing tools. The activities use a public demonstration task-list website.
>
> Use fictional task names and non-sensitive examples. Do not include passwords, access tokens, API keys, identification numbers, personal contact details or confidential information in code, screenshots, traces or GitHub files.
>
> Review files before uploading them. Public repositories can be viewed by anyone.

This practical helps you learn automated testing tools by using them. You will work in a small group, run browser tests on your own Windows computer and combine your source files in a shared repository.

You have already completed a basic Python module. This practical builds on that knowledge to introduce automated testing. Complete Python examples and explanations are provided to help you get started. You do not need to build a website, learn JavaScript or create an application server.

The activities cover browser inspection, recording, replay, assertions, different input values, reports and failure investigation. Use installed Google Chrome or Microsoft Edge for the main activities. Other browsers are optional.

All tests are started manually on your computer. Git and GitHub are used throughout to save and share source changes.

### Tools used in this practical

| Tool | What you will use it for |
| --- | --- |
| Python | Write and run test code. |
| Visual Studio Code, or VS Code | Edit project files. |
| Microsoft Python extension for VS Code | Select the project's Python interpreter and support code editing. |
| Google Chrome or Microsoft Edge | Run the main browser activities. |
| Browser Developer Tools | Examine page elements and their attributes. |
| Playwright | Control the browser and check page behaviour. |
| Playwright Codegen | Record actions and generate starting code. |
| pytest | Find and run test functions. |
| pytest-html | Create an HTML results report. |
| Playwright Trace Viewer | Look back through test actions, page snapshots and errors. |
| Git and GitHub | Save versions, share branches and combine source changes. |

Codegen and Trace Viewer are included with Playwright. Developer Tools is included with Chrome and Edge.

### Browser options included

| Browser | Use | Selection for pytest |
| --- | --- | --- |
| Google Chrome | Main option: installed stable Chrome. | `--browser chromium --browser-channel chrome` |
| Microsoft Edge | Main option: installed stable Edge. | `--browser chromium --browser-channel msedge` |
| Playwright Chromium | Optional: download through Playwright. | `--browser chromium` without a channel |
| Playwright Firefox | Optional: download Playwright's supported build. | `--browser firefox` |
| Playwright WebKit | Optional: download through Playwright. | `--browser webkit` |

> [!IMPORTANT]
> Chrome and Edge are Chromium-based browsers. In pytest commands, `--browser chromium` selects the browser family and `--browser-channel` selects installed Chrome or Edge.
>
> You do not need a Playwright Chromium download for the main Chrome or Edge activities. Ordinary Firefox does not replace Playwright's Firefox build. Playwright WebKit is not the installed Safari application.

### Practical overview

| Item | Details |
| --- | --- |
| Group size | Suggested: 4–5 members. |
| Operating system | Windows for every member. |
| Terminal | Windows Command Prompt inside VS Code. |
| Required knowledge | Basic Python, from the module completed earlier. |
| Main browser | Installed stable Google Chrome or Microsoft Edge. Each member chooses one. |
| Test website | [Playwright TodoMVC demonstration](https://demo.playwright.dev/todomvc/) |
| Shared work | One repository, a personal branch and a separate test file for each member. |
| Focus | Exploring automated testing tools, not developing an application. |
| Working pace | Follow the activities in order. Pause and repeat steps when needed. |

## Contents

1. [Learning outcomes](#1-learning-outcomes)
2. [Understand the workflow](#2-understand-the-workflow)
3. [Prepare your group and Windows computers](#3-prepare-your-group-and-windows-computers)
4. [Create and clone the repository](#4-create-and-clone-the-repository)
5. [Create the starting files](#5-create-the-starting-files)
6. [Prepare your individual environment](#6-prepare-your-individual-environment)
7. [Explore the website](#7-explore-the-website)
8. [Create automated checks](#8-create-automated-checks)
9. [Run data-driven tests](#9-run-data-driven-tests)
10. [Record and replay browser actions](#10-record-and-replay-browser-actions)
11. [Create an HTML report](#11-create-an-html-report)
12. [Investigate a failed test](#12-investigate-a-failed-test)
13. [Combine group contributions](#13-combine-group-contributions)
14. [Troubleshooting and command reference](#14-troubleshooting-and-command-reference)
15. [Optional extension activities](#15-optional-extension-activities)

***

## 1. Learning outcomes

The activities introduce how to:

- Use Playwright and pytest to run browser tests.
- Inspect a page element.
- Distinguish actions from assertions.
- Check valid and invalid inputs.
- Run one test with different input values.
- Record and replay browser actions.
- Generate an HTML report.
- Investigate a failed check using a screenshot and trace.
- Save source changes on a personal branch and combine them with shared work.

### Working through this practical

1. Follow the main activities in order.
2. Read the explanation before running a command.
3. Enter commands in Command Prompt.
4. Enter Python code in the named `.py` file.
5. Save files before running them.
6. Use your own member number in filenames and branch names.
7. Read actual results rather than assuming a command succeeded.
8. Use Section 14 when a result differs from the description.

> [!IMPORTANT]
> Run commands from inside your cloned project folder unless a step says otherwise. Check your branch before editing. Activate the Python environment before running Python commands.
>
> Copy only the contents of code blocks, not the surrounding backticks or the language label such as `python`.

### Suggested activity sequence

| Stage | Activities |
| --- | --- |
| Group setup | Prepare software, create the repository and share the starting files. |
| Individual setup | Create a branch, prepare Python and select Chrome or Edge. |
| First tests | Explore the website, run the examples and try different inputs. |
| Recording and diagnostics | Record actions, open a report and investigate a deliberate failure. |
| Group integration | Combine personal files and run the shared project once. |
| Further practice | Try an optional browser or extend a test. |

Allow extra time for installation and downloads. Take breaks when needed.

***

## 2. Understand the workflow

### A simple mental model

The website is the application you want to check. Playwright follows your browser instructions. pytest finds and runs tests. Assertions check whether the page matches your expectations.

```text
Open a page → Perform an action → Check the result
```

### Key terms

| Term | Meaning |
| --- | --- |
| Test | Steps that perform an activity and check its result. |
| Locator | An instruction that finds part of a page. |
| Action | Something the browser does, such as typing or clicking. |
| Assertion | A check of an expected result. |
| Positive test | A test of valid input or an expected action. |
| Negative test | A test of invalid input or an invalid action. |
| Parametrization | Running the same test with several input values. |
| Virtual environment | A separate set of Python packages for this project. |
| Browser channel | Installed Chrome or Edge selected for a run. |
| Headed / headless | Running with / without a visible browser window. |
| Report | A summary of a test run. |
| Trace | A record used to look back through a test run. |
| Repository | A project with changes tracked by Git. |
| Clone | Make a local copy of a repository. |
| Branch | A separate line of work in a repository. |
| Commit | A saved record of selected changes on your computer. |
| Push | Upload commits to GitHub. |
| Pull request, or PR | A request to combine a branch with another branch. |
| Merge | Combine branch changes. |
| Pull | Bring shared changes into your local branch. |

### Actions and assertions

These actions enter and submit a task:

```python
task_input.fill("Read testing notes")
task_input.press("Enter")
```

This assertion checks its text:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

These are explanatory snippets. Complete examples follow later.

A script that only clicks and types may finish without checking that the correct task appeared.

### Positive and negative do not mean pass and fail

| Scenario | Expected behaviour | Passing outcome |
| --- | --- | --- |
| Add a normal task. | A task appears. | Its text is correct. |
| Submit an empty task. | No task is added. | The task list stays empty. |

A negative test passes when invalid input is handled as expected.

### Saving, committing and sharing

```text
Save   → Write changes to a file.
Commit → Record selected changes locally.
Push   → Upload local commits to GitHub.
PR     → Propose combining your branch with main.
Merge  → Combine the proposed changes.
Pull   → Update your local copy with shared changes.
```

Saving does not commit. Committing does not upload. Pushing does not merge.

### Group working rules

- Use your own branch and test file.
- Run the examples on your own computer.
- Keep shared configuration changes with the coordinator during initial setup.
- Discuss changes before editing another member's file.
- Keep commit messages short and meaningful.
- Keep generated browser outputs local.
- Use fictional data and small, deliberate runs.

> [!WARNING]
> Do not perform load testing, security scanning or continuous repeated runs against the public website. Do not force-push or use destructive reset commands to bypass a Git problem. Preserve your files and inspect the current state first.

***

## 3. Prepare your group and Windows computers

### 3.1 Agree member numbers

Choose a coordinator for the initial repository setup. Give each member a number.

| Member | Personal test file | Personal branch |
| --- | --- | --- |
| 1 | `tests/test_member_1.py` | `testing/member-1` |
| 2 | `tests/test_member_2.py` | `testing/member-2` |
| 3 | `tests/test_member_3.py` | `testing/member-3` |
| 4 | `tests/test_member_4.py` | `testing/member-4` |
| 5, if present | `tests/test_member_5.py` | `testing/member-5` |

The coordinator also completes the individual testing activities.

Examples use Member 1. Replace member numbers in file paths and branch names with your own. Keep the test function names unchanged.

### 3.2 Check Python

Use Python 3.12 or 3.13 for this guide. Keep a suitable existing installation.

If needed, install Python from [Python Downloads](https://www.python.org/downloads/). Select `Add Python to PATH` if offered, then reopen VS Code.

### 3.3 Prepare VS Code

1. Install [VS Code](https://code.visualstudio.com/) if needed.
2. Open Extensions.
3. Search for `Python`.
4. Install the extension published by Microsoft.

The extension does not install Python itself.

### 3.4 Open Command Prompt in VS Code

1. Select Terminal → New Terminal.
2. Open the dropdown beside the terminal's `+` button.
3. Select Command Prompt. If necessary, choose Select Default Profile → Command Prompt, then open a new terminal.

Use this terminal throughout the practical. If you see Python's `>>>` prompt, type `exit()` and press Enter before entering terminal commands.

Check Python:

```bat
python --version
```

If unavailable:

```bat
py -3 --version
```

You should see a Python version number.

### 3.5 Check Chrome or Edge

Open installed stable Chrome or Edge from Start and confirm it loads a website. You do not need both browsers or a signed-in personal profile.

If needed, use an approved installer for [Google Chrome](https://www.google.com/chrome/) or [Microsoft Edge](https://www.microsoft.com/edge/download).

### 3.6 Check Git and GitHub

```bat
git --version
```

If missing, install Git for Windows from [Git Downloads](https://git-scm.com/downloads), then reopen VS Code.

Replace the values below before running:

```bat
git config --global user.name "Your Name"
git config --global user.email "YOUR_GITHUB_COMMIT_EMAIL"
```

Use an email linked to GitHub or your GitHub no-reply email. These settings identify commits; they do not sign you in.

Sign in to GitHub in your browser. When Git later requests authentication, follow the browser sign-in instructions. Never put passwords or tokens in project files.

> [!NOTE]
> Use approved installation methods on managed computers. Ask IT support when administrator access is required. Do not bypass restrictions. If one browser is unavailable, use the other approved browser.

### Before continuing

Each member should be able to open VS Code and Chrome or Edge, display Python and Git versions, and sign in to GitHub.

***

## 4. Create and clone the repository

### 4.1 Coordinator: create the shared repository

On GitHub:

1. Create a repository such as `automated-testing-tools-team-01`.
2. Use the visibility approved for your group. A private repository limits access to invited people.
3. Add a README and confirm the starting branch is `main`.
4. Put this guide in `README.md`.
5. Open Settings → Collaborators, or the equivalent access page.
6. Invite the other members using their GitHub usernames.
7. Ask members to accept their invitations.

### 4.2 Everyone: clone the repository

On the repository page, select Code → HTTPS and copy the URL.

In Command Prompt, move to a parent folder where you want to keep the project. For example:

```bat
cd /d "%USERPROFILE%\Documents"
```

Type `git clone`, add a space and paste the copied URL:

```bat
git clone PASTE_THE_COPIED_HTTPS_URL_HERE
```

Replace the placeholder. Do not type it literally or use Markdown link syntax.

Enter the created folder, using its actual name:

```bat
cd automated-testing-tools-team-01
```

In VS Code, select File → Open Folder and open that folder. Open a new Command Prompt terminal.

### 4.3 Inspect your copy

```bat
git status
git branch
git remote -v
git log --oneline -5
```

| Command | What to check |
| --- | --- |
| `git status` | You are on `main`, with no uncommitted changes. |
| `git branch` | The `*` marks the current branch. |
| `git remote -v` | `origin` points to your shared repository. |
| `git log --oneline -5` | Recent commits are visible. |

`origin` is Git's short name for that remote repository. Press `q` if a scrolling view opens.

***

## 5. Create the starting files

> [!IMPORTANT]
> The coordinator completes this section first. Other members continue with Section 6 after the setup PR has merged.

### 5.1 Create the setup branch

```bat
git switch main
git pull --ff-only origin main
git switch -c setup/testing-files
```

The commands select `main`, update it and create a setup branch. `--ff-only` updates only when Git can move the branch forward directly.

### 5.2 Prepare the structure

Use VS Code's New File and New Folder controls:

```text
README.md
.gitignore
requirements.txt
pytest.ini
tests/
```

Git does not store empty folders. Other members may not see `tests` until it contains a committed file. That is normal.

### 5.3 Create `.gitignore`

```gitignore
.venv/
__pycache__/
.pytest_cache/
reports/
recordings/
test-results/
.env
```

This keeps local environments and generated outputs out of shared commits.

### 5.4 Create `requirements.txt`

```text
pytest-playwright
pytest-html
```

### 5.5 Create `pytest.ini`

```ini
[pytest]
testpaths = tests
addopts = -v --browser chromium
```

This selects the browser family and displays test names. Each member selects installed Chrome or Edge in their commands, without changing the shared file.

### 5.6 Stage, commit and push

Save the files, then run:

```bat
git status
git add .gitignore requirements.txt pytest.ini
git diff --staged
git commit -m "Add shared testing configuration"
git push -u origin setup/testing-files
```

`git add` selects changes for a commit. `git diff --staged` displays them. `-u` links the local branch to its remote branch so later uploads can use `git push`.

### 5.7 Create and merge the setup PR

On GitHub:

1. Open a PR from `setup/testing-files` to `main`.
2. Confirm base is `main` and compare is `setup/testing-files`.
3. Inspect Files changed.
4. Confirm only intended files are included and no private data appears.
5. Merge the PR.

The base is the destination. The compare branch contains your changes.

Let the group know when the setup is merged.

***

## 6. Prepare your individual environment

### 6.1 Everyone: update and create a personal branch

```bat
git switch main
git pull --ff-only origin main
git switch -c testing/member-1
git status
```

Use your own member number. You should now be on your personal branch and able to open the starting files.

### 6.2 Create a virtual environment

```bat
python -m venv .venv
```

If only the launcher worked earlier, use this instead:

```bat
py -3 -m venv .venv
```

A virtual environment separates this project's packages from other projects. A `.venv` folder should appear. The command may finish without a message.

### 6.3 Activate and check it

```bat
.venv\Scripts\activate.bat
python -c "import sys; print(sys.executable)"
```

The displayed path should contain this project's `.venv\Scripts\python.exe`.

> [!TIP]
> If activation fails, confirm you are using Command Prompt. You can also replace `python` at the start of later commands with `.venv\Scripts\python.exe`. Do not weaken security settings.

### 6.4 Select the VS Code interpreter

Press Ctrl+Shift+P, search for `Python: Select Interpreter` and choose the Python inside `.venv`.

### 6.5 Install and verify the packages

Run these one at a time, waiting for each to finish:

```bat
python -m pip install -r requirements.txt
python -m pytest --version
python -m playwright --version
```

Each version command should display a version number. No Playwright browser download is needed for the main activities using installed Chrome or Edge.

### 6.6 Choose your browser for this terminal

Run only one of these commands.

Google Chrome:

```bat
set "TEST_BROWSER=chrome"
```

Microsoft Edge:

```bat
set "TEST_BROWSER=msedge"
```

Check:

```bat
echo %TEST_BROWSER%
```

You should see `chrome` or `msedge`. `%TEST_BROWSER%` is a Command Prompt variable. Later commands use it to insert your choice. It lasts only for the current terminal session.

### 6.7 Create local folders

Use VS Code to create `tests`, `recordings` and `reports` if missing.

### Returning another day

1. Open the same repository folder.
2. Open Command Prompt.
3. Activate `.venv`.
4. Set `TEST_BROWSER` again.
5. Run `git status` and continue on your existing branch.

Do not recreate a branch that already exists. Use `git switch testing/member-1` to return to it, using your number.

***

## 7. Explore the website

### 7.1 Try the task list manually

Open [Playwright TodoMVC](https://demo.playwright.dev/todomvc/) in Chrome or Edge.

1. Click `What needs to be done?`.
2. Enter `Read testing notes` and press Enter.
3. Find the task.
4. Select its checkbox.
5. Try All, Active and Completed.

The tests will perform similar actions. The automated browser uses a separate session, not your everyday signed-in profile. You do not need to delete tasks from your usual browser before testing.

### 7.2 Inspect the input

1. Right-click the task input and select Inspect.
2. Find the selected input in Developer Tools.
3. Look for `placeholder="What needs to be done?"`.
4. Close Developer Tools.

An attribute is extra information attached to a page element. Here, the placeholder supplies the hint text. Playwright can use it to find the input.

***

## 8. Create automated checks

### 8.1 Create your personal test file

Member 1 creates `tests/test_member_1.py`. Use your own number.

Paste this complete code and save it. Keep the spaces at the start of indented lines.

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

### 8.2 Run your first test

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed --slowmo 300
```

### What you should see

Your selected Chrome or Edge opens, loads the website, adds a task and closes. If all checks succeed, the terminal reports `1 passed`.

Read the actual result. Use Section 14 if it differs.

### 8.3 Understand the code

| Code or option | Purpose |
| --- | --- |
| `from ... import ...` | Makes Playwright's tools available. |
| `URL = ...` | Stores the website address. |
| `def test_add_task(...)` | Defines a test. pytest recognises names beginning with `test_`. |
| `page` | A browser page supplied by the Playwright pytest package. |
| `page: Page` | A type hint that helps the editor understand `page`. |
| `page.goto(URL)` | Opens the website. |
| `get_by_placeholder(...)` | Finds the task input by its hint text. |
| `exact=True` | Requires the whole hint text to match. |
| `locator(".todo-list li")` | Finds task rows using a CSS selector. |
| `task_items.locator("label")` | Finds text labels inside those rows. |
| `fill(...)` and `press("Enter")` | Enter text and submit it. |
| `to_have_count(...)` | Checks the number of rows. |
| `to_have_text([...])` | Checks task labels against a list of expected labels. |
| `to_have_value("")` | Checks that the input is empty. |
| `--browser-channel %TEST_BROWSER%` | Selects your chosen installed browser. |
| `--headed` | Displays its window. |
| `--slowmo 300` | Slows actions so you can watch. |

You can reuse the CSS selector without learning CSS first. Playwright's page assertions wait briefly for the expected condition. Do not add arbitrary pauses to make a test work.

### 8.4 Commit the first test

```bat
git status
git add tests/test_member_1.py
git diff --staged
git commit -m "Add first task creation test"
git push -u origin testing/member-1
```

Use your own filename and branch. On GitHub, switch to your branch to find the file. It is not on `main` until merged.

### 8.5 Add a completion test

Append this to the same file. Keep the existing import, URL and test.

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

### 8.6 Run both tests

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed
```

If both succeed, the terminal reports `2 passed`.

`first` selects the first task row. `get_by_role("checkbox")` finds its checkbox. `check()` selects it. `to_be_checked()` checks its state. The Completed link then shows completed tasks.

Each test gets a fresh browser session and creates its own task. It does not rely on a previous test's data.

***

## 9. Run data-driven tests

### 9.1 Understand the expected behaviour

An empty or spaces-only task should not be added. These negative tests pass when the list stays empty.

### 9.2 Add the import

Add `import pytest` at the top of your test file. Keep everything else.

The top should now look like this:

```python
import pytest
from playwright.sync_api import Page, expect

URL = "https://demo.playwright.dev/todomvc/"
```

### 9.3 Add the parametrized test

Append:

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

The line starting with `@` tells pytest to run the function once per input. This is parametrization.

| Part | Meaning |
| --- | --- |
| `""` | An empty string: no characters. |
| `" "` | One space. |
| `"   "` | Three spaces. |
| `task_text` | Receives the current input. |
| `ids` | Gives each run a readable name. |
| `task_text: str` | A type hint saying the input is text. |

### 9.4 Run the file

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed
```

### What you should see

Two earlier tests plus three input cases produce five runs. If all succeed, the terminal reports `5 passed`.

These examples do not cover every possible invalid input.

### 9.5 Commit and push

```bat
git add tests/test_member_1.py
git diff --staged
git commit -m "Add completion and blank input checks"
git push
```

***

## 10. Record and replay browser actions

### 10.1 Start Codegen

Check that `recordings` exists, then run:

```bat
python -m playwright codegen --channel %TEST_BROWSER% --target python-pytest -o recordings/member_1.py https://demo.playwright.dev/todomvc/
```

> [!NOTE]
> Codegen uses `--channel`. pytest uses `--browser-channel`. Your shared `pytest.ini` does not configure Codegen.

### 10.2 Record a scenario

1. Enter `Try the recorder` in the recording browser.
2. Press Enter.
3. Find the text assertion control in the recording toolbar. Hover over controls to read their labels.
4. Select it, then select the new task's text.
5. Look for an `expect(...)` check in the generated code.
6. Close the recording windows to finish.

### 10.3 Add a check if needed

If the recording has no task-text assertion, open `recordings/member_1.py`. Inside its test function, after the action that presses Enter, add:

```python
expect(page.locator(".todo-list li label")).to_have_text(
    ["Try the recorder"]
)
```

Match the indentation of the function's other lines. If `expect` is not already imported, add this at the top:

```python
from playwright.sync_api import expect
```

### 10.4 Replay

```bat
python -m pytest recordings/member_1.py --browser-channel %TEST_BROWSER% --headed --slowmo 300
```

The recording runs separately from the five cases in your personal test file. It stays local because `recordings` is ignored by Git.

A recording with only actions may finish without checking the intended result. Read the generated code before relying on it.

***

## 11. Create an HTML report

### 11.1 Generate the report

Check that `reports` exists, then run:

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --html=reports/member-1.html --self-contained-html
```

Your selected Chrome or Edge runs without a visible window because this command leaves out `--headed`.

### 11.2 Open the report

1. Open the project folder in Windows File Explorer.
2. Open `reports`.
3. Double-click `member-1.html` to open it in a browser.

The report shows test names, results, durations and errors. Expand a failed result to read more.

The report stays local and is not added to Git. It summarises one run; it does not prove that the whole website has been checked.

***

## 12. Investigate a failed test

You will deliberately introduce an incorrect expectation. This demonstrates troubleshooting, not a confirmed website defect.

### 12.1 Change one expectation

In `test_add_task()`, change:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

temporarily to:

```python
expect(task_labels).to_have_text(["A different task"])
```

Do not change the input text in `fill(...)`.

### 12.2 Run with diagnostic options

```bat
python -m pytest tests/test_member_1.py::test_add_task --browser-channel %TEST_BROWSER% --headed --screenshot only-on-failure --tracing retain-on-failure --output test-results/member-1-failure
```

| Option | Purpose |
| --- | --- |
| `::test_add_task` | Select only this test function. |
| `--screenshot only-on-failure` | Save a screenshot if it fails. |
| `--tracing retain-on-failure` | Keep the failed run's trace. |
| `--output ...` | Choose where generated output is saved. |

### What you should see

The test fails: it enters `Read testing notes` but expects `A different task`. Find the expected and actual text in the terminal error.

The deliberately incorrect expectation caused this failure. It does not demonstrate a website defect.

### 12.3 Open the screenshot

In VS Code's file explorer, open `test-results/member-1-failure` and its generated test subfolder. Open the screenshot.

The subfolder name is generated automatically. Find it rather than guessing it.

### 12.4 Open the trace

Find `trace.zip` in the same subfolder. Right-click it and select Copy Relative Path.

Replace the placeholder below with that path. Keep the quotation marks.

```bat
python -m playwright show-trace "PASTE_RELATIVE_PATH_HERE" --browser-channel %TEST_BROWSER%
```

In Trace Viewer, look through the page loading, text entry, Enter key and failed check.

### 12.5 Restore and rerun

Restore:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

Save and run:

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER%
```

If all checks succeed, the terminal reports `5 passed` again.

Inspect your changes:

```bat
git diff
```

If you restored the file exactly, Git may show no changes. That is normal; no extra commit is needed.

> [!IMPORTANT]
> Do not delete or skip the assertion to hide a failure. Restore the meaningful expectation before sharing the code. Do not commit the deliberately incorrect version.
>
> Later runs may replace generated output. Copy a screenshot or trace elsewhere only if you want to keep it locally.

***

## 13. Combine group contributions

### 13.1 Finish your personal branch

```bat
git status
git push
```

If your source file still has intended changes, run your tests, add and commit that file, then push again. Do not add the virtual environment, recordings, reports or traces.

### 13.2 Create your PR

On GitHub:

1. Open a PR from your personal branch to `main`.
2. Confirm the base and compare branches.
3. Use a title such as `Add Member 1 browser tests`.
4. Open Files changed.
5. Look through the changes with another group member.

```text
base: main
compare: testing/member-1
```

A short PR description can state what changed and which browser you used. Keep it factual and brief.

### 13.3 Merge one contribution at a time

Before merging, check that:

- The test file uses the correct member number.
- No other member's file is replaced.
- The deliberately wrong expectation has been restored.
- No private data or generated outputs are included.

Merge one member's PR at a time. Different member filenames allow the guided tests to sit beside one another without overwriting them.

### 13.4 Everyone: update local main

Start with a clean working directory. Commit intended source changes on your work branch before switching.

```bat
git switch main
git pull --ff-only origin main
git status
```

Merging on GitHub does not automatically update your computer. You should now see the merged test files.

### 13.5 Run the combined project once

Choose one member to run:

```bat
python -m pytest --browser-channel %TEST_BROWSER% --html=reports/group-results.html --self-contained-html
```

If each member has only the five guided cases, there are five runs per member file. Additional tests increase that count.

Repeated guided cases cover the same behaviours; they are not extra unique functional coverage. Avoid repeatedly running the full group suite without a reason.

If a test fails, use the filename and error to locate the relevant source. Make corrections on a new branch and combine them through another PR.

### 13.6 Inspect Git history

```bat
git log --oneline --graph --decorate --all -15
```

Use an actual commit ID from the output:

```bat
git show COMMIT_ID
```

This shows what changed in that commit. Press `q` if a scrolling view opens.

For another activity, start a new branch from updated `main`:

```bat
git switch -c practice/member-1-next
```

***

## 14. Troubleshooting and command reference

### Before attempting a fix

1. Save the file.
2. Read the error message.
3. Check the folder, interpreter, branch and browser setting.
4. Preserve your work before making larger changes.

```bat
python -c "from pathlib import Path; import sys; print('Folder:', Path.cwd()); print('Python:', sys.executable)"
git status
echo %TEST_BROWSER%
```

The folder should be your repository. The Python path should contain `.venv`. The browser value should be `chrome` or `msedge`.

### Common problems

| Problem | What to try |
| --- | --- |
| Python is not recognised | Reopen VS Code. Try `py -3 --version`. Review installation if neither command works. |
| Packages cannot be imported | Activate `.venv`, check the Python path and repeat `python -m pip install -r requirements.txt`. |
| Activation fails | Use Command Prompt and `.venv\Scripts\activate.bat`. |
| Browser setting is empty or displays `%TEST_BROWSER%` | Run `set "TEST_BROWSER=chrome"` or `set "TEST_BROWSER=msedge"` in this terminal. |
| Chrome or Edge cannot be found | Check it opens from Start. Use the other installed approved browser if needed, then set the variable again. |
| Playwright Chromium executable is missing | For main tests include `--browser-channel %TEST_BROWSER%`. For Codegen include `--channel %TEST_BROWSER%`. |
| No tests are found | Save the file. Check its `.py` extension, its `test_` filename and its `test_` function names. |
| A file cannot be found | Check your member number, spelling and current folder. |
| `IndentationError` | Match the leading spaces. Use four spaces inside a function. |
| `SyntaxError` | Check quotes, brackets and colons. Do not paste Markdown backticks into Python. |
| Browser is not visible | Add `--headed`. |
| Browser closes quickly | Normal after a run. Use `--headed --slowmo 300`, then read the terminal result. |
| Expected text differs | Compare spelling, capital letters and spaces in the input and assertion. |
| Website cannot load | Try the URL manually. Check the connection. If unavailable, save your work and retry later. |
| Locator times out | Check the page loaded and the locator matches it. Use Inspect or Codegen. |
| HTML report has no screenshot | Open screenshots separately under `test-results`. |
| Generated output disappeared | Later runs may replace it. Copy files locally first if you want to keep them. |
| Browser or download blocked by policy | Use approved software and network processes. Do not disable security controls. |
| Repository not found | Check the URL, GitHub sign-in and accepted collaborator invitation. |
| Push is rejected | Check authentication, permissions, branch and remote. Do not force-push. |
| Nothing to commit | The file may be unchanged, already committed, unsaved or ignored. Use `git status` and `git diff`. |
| Local main lacks merged files | From clean local `main`, run `git pull --ff-only origin main`. |
| Git warns about overwriting local changes | Stop. Inspect `git status` and commit intended source changes on your work branch before switching. |

### If you accidentally committed on main

Preserve those commits by creating a branch at the current position:

```bat
git switch -c recovery/member-1-main-work
```

Use your number. Inspect the history and compare the work with shared `main` before deciding how to combine it. Do not reset or force-push simply to make the warning disappear.

### If `git pull --ff-only` refuses

A refusal because histories have diverged does not start a merge. Inspect first:

```bat
git status
git fetch origin
git log --oneline --graph --decorate --all -15
```

Keep your commits. Do not use destructive reset commands. If shared files are involved, look through the history with the member who changed them before choosing how to combine the work.

### If a merge conflict appears

`git status` identifies conflicting files when a local merge is in progress. Open each file in VS Code, compare both versions and keep the intended content. Remove conflict markers such as `<<<<<<<`, `=======` and `>>>>>>>`, save and run the relevant tests before completing the merge.

Do not blindly accept one version of another member's file. Work through that file with its owner.

If you want to cancel an unresolved local merge, use `git merge --abort` only when `git status` confirms a merge is in progress. Do not delete the repository.

### Testing command reference

Use your own member number.

| Goal | Command |
| --- | --- |
| Select Chrome in this terminal | `set "TEST_BROWSER=chrome"` |
| Select Edge in this terminal | `set "TEST_BROWSER=msedge"` |
| Watch your tests | `python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed --slowmo 300` |
| Run without a visible window | `python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER%` |
| Run one test | `python -m pytest tests/test_member_1.py::test_add_task --browser-channel %TEST_BROWSER% --headed` |
| Create a report | `python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --html=reports/member-1.html --self-contained-html` |
| Replay a recording | `python -m pytest recordings/member_1.py --browser-channel %TEST_BROWSER% --headed` |

### Git command reference

| Command | Purpose |
| --- | --- |
| `git status` | Inspect the branch and working state. |
| `git branch --show-current` | Display the current branch. |
| `git diff` | Inspect unstaged changes to tracked files. |
| `git add tests/test_member_1.py` | Select changes in your test file. |
| `git diff --staged` | Inspect selected changes. |
| `git commit -m "Describe the change"` | Record selected changes locally. |
| `git push` | Upload commits after the branch's first linked push. |
| `git fetch origin` | Download information about shared changes. |
| `git log --oneline` | Inspect compact history. |
| `git show COMMIT_ID` | Inspect an actual commit. |

***

## 15. Optional extension activities

Choose an activity when you are comfortable with the main examples. For source changes, start a new personal branch from updated `main`, work in your own file, run it and combine changes through a PR.

### A. Try the other main browser

Set `TEST_BROWSER` to the other installed browser and rerun your personal test file. Your source code and shared configuration stay unchanged.

### B. Try Playwright Chromium, Firefox or WebKit

These browsers need separate downloads. The commands below override shared `addopts` for the current run and select one browser explicitly. Do not add Chrome or Edge channels to Firefox or WebKit.

Playwright Chromium:

```bat
python -m playwright install chromium
python -m pytest tests/test_member_1.py -o "addopts=-v" --browser chromium --headed
```

Playwright Firefox:

```bat
python -m playwright install firefox
python -m pytest tests/test_member_1.py -o "addopts=-v" --browser firefox --headed
```

Playwright WebKit:

```bat
python -m playwright install webkit
python -m pytest tests/test_member_1.py -o "addopts=-v" --browser webkit --headed
```

Skip unsupported or blocked optional browsers. Compare functional results, not browser speed. These small runs are not performance benchmarks.

After upgrading Playwright, reinstall any Playwright-managed browsers you use. This does not mean reinstalling ordinary Chrome or Edge.

### C. Change the task name

In `test_add_task()`, replace `Read testing notes` with another fictional name in both the input action and assertion. Save and rerun.

### D. Add another blank-input case

Replace the parametrization block above your blank-input function with:

```python
@pytest.mark.parametrize(
    "task_text",
    ["", " ", "   ", "    "],
    ids=["empty", "one-space", "three-spaces", "four-spaces"],
)
```

Keep the function unchanged. There is one ID per input. Your file now runs six cases.

### E. Create a reusable helper

A helper performs steps you want to reuse. Append both functions to your personal test file. Keep its imports and URL.

```python
def add_task(page: Page, task_name: str):
    task_input = page.get_by_placeholder(
        "What needs to be done?",
        exact=True,
    )
    task_input.fill(task_name)
    task_input.press("Enter")


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

Run your personal file. This adds one test. The helper performs actions; the test contains the assertions.

Suggested commit message:

```text
Add reusable task entry helper and two-task check
```

### F. Record another action

Try completing, editing or deleting a task manually. Record it in your chosen Chrome or Edge, read the generated code and reuse earlier assertion patterns to check the result.

If expected behaviour is unclear, treat the result as an observation rather than a confirmed defect.

***

## Closing reminder

A passing test means its particular checks succeeded in that run. It does not prove that the whole website is error-free.

Keep examples small and understandable. Use failed checks to understand what happened. Share working source without uploading private data or local browser outputs.

```text
Choose a behaviour → Define the expectation → Automate → Run
                   → Investigate → Improve → Commit → Push → Merge
```
