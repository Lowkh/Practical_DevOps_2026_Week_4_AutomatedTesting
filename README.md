# Automated Testing Tools Group Practical

> A guided, hands-on introduction to browser automation using Windows and Google Chrome or Microsoft Edge.

> [!NOTE]
> ## Educational Practice Materials
>
> This practical uses a public demonstration website. Use fictional task names only. Do not enter or share passwords, API keys, identification numbers, personal contact details or confidential information. Screenshots and traces may contain page content.

Learn automated testing by opening a task-list website, automating browser actions and checking the results.

No previous automated testing experience is needed. You have already completed a basic Python module. This practical builds on that knowledge to introduce automated testing. Complete Python examples and explanations are provided to help you get started. You do not need to build a website, learn JavaScript or create an application server.

Work in a small group. Each member runs the activities on their own computer, saves changes on their own branch and combines their test file with the shared project. Move through the activities at a comfortable pace and use the troubleshooting section when needed.

### Tools used in this practical

| Tool | What you will use it for |
| --- | --- |
| Windows | The operating system used throughout this guide. |
| Python | Run the test code. |
| Visual Studio Code, or VS Code | Create and edit files. |
| Microsoft Python extension for VS Code | Help the editor work with Python. |
| Google Chrome or Microsoft Edge | Run the main browser activities. Choose either one. |
| Browser Developer Tools | Look at page elements and their attributes. |
| Playwright | Control the browser and check page behaviour. |
| Playwright Codegen | Record actions and create starting code. |
| pytest | Find and run tests. |
| pytest-html | Create an HTML results report. |
| Playwright Trace Viewer | Look back through test actions and page snapshots. |
| Git | Save versions of the project on your computer. |
| GitHub | Share branches and combine group changes. |

Codegen and Trace Viewer are included with Playwright. Developer Tools is included with Chrome and Edge.

### Browser options

| Browser | Use in this guide | Selection |
| --- | --- | --- |
| Microsoft Edge | Main option. Use installed stable Edge. | `--browser chromium --browser-channel msedge` |
| Google Chrome | Equally suitable main option. Use installed stable Chrome. | `--browser chromium --browser-channel chrome` |
| Playwright Chromium | Optional additional browser. | `--browser chromium` without a channel |
| Playwright Firefox | Optional additional browser. | `--browser firefox` |
| Playwright WebKit | Optional additional browser. | `--browser webkit` |

> [!IMPORTANT]
> Chrome and Edge are Chromium-based browsers. For pytest, `--browser chromium` selects the browser family. The channel selects installed Chrome or Edge.
>
> You do not need to download Playwright Chromium for the main activities. Ordinary Firefox does not replace Playwright's supported Firefox build. Playwright WebKit is not installed Safari.

### Practical overview

| Item | Details |
| --- | --- |
| Operating system | Windows. |
| Group size | Suggested: 3–5 members. |
| Working arrangement | Each member uses their own computer and GitHub account. |
| Previous testing knowledge | None. |
| Python knowledge | Basic Python, from the module completed earlier. |
| Main browser | Installed stable Chrome or Edge. |
| Terminal | Windows Command Prompt inside VS Code. |
| Project location | A folder of your choice where you can save files. |
| Test website | [Playwright TodoMVC demonstration](https://demo.playwright.dev/todomvc/) |
| Project | One shared repository with a separate test file for each member. |

## Contents

1. [Understand the workflow](#1-understand-the-workflow)
2. [Prepare your Windows computer](#2-prepare-your-windows-computer)
3. [Create and clone the group repository](#3-create-and-clone-the-group-repository)
4. [Create the shared starting files](#4-create-the-shared-starting-files)
5. [Prepare your branch and Python environment](#5-prepare-your-branch-and-python-environment)
6. [Explore the website](#6-explore-the-website)
7. [Create your first automated check](#7-create-your-first-automated-check)
8. [Check task completion](#8-check-task-completion)
9. [Run one test with different inputs](#9-run-one-test-with-different-inputs)
10. [Record and replay browser actions](#10-record-and-replay-browser-actions)
11. [Create a results report](#11-create-a-results-report)
12. [Investigate a failed check](#12-investigate-a-failed-check)
13. [Combine the group files](#13-combine-the-group-files)
14. [Troubleshooting and command reference](#14-troubleshooting-and-command-reference)
15. [Optional browsers and further practice](#15-optional-browsers-and-further-practice)

***

## 1. Understand the workflow

Playwright performs browser actions. pytest runs your test functions. Assertions check whether the page matches the expected result.

```text
Open a page → Perform an action → Check the result
```

### Key terms

| Term | Simple meaning |
| --- | --- |
| Test | Steps that perform an activity and check its result. |
| Locator | An instruction that finds part of a page. |
| Action | Something the browser does, such as typing or clicking. |
| Assertion | A check of an expected result. |
| Negative test | A test of invalid input or an invalid action. |
| Parametrization | Running the same test with different inputs. |
| Virtual environment | A separate set of Python packages for this project. |
| Browser channel | The installed Chrome or Edge selected for a run. |
| Headed / headless | Running with / without a visible browser window. |
| Report | A summary of a test run. |
| Trace | A record for looking back through a run. |
| Repository | A project whose changes are tracked by Git. |
| Clone | Make a local copy of a GitHub repository. |
| Branch | A separate line of work in the repository. |
| Commit | A saved record of selected changes on your computer. |
| Push | Upload your commits to GitHub. |
| Pull request, or PR | A request to combine a branch with another branch. |
| Merge | Combine changes from branches. |
| Pull | Bring shared changes into your local branch. |
| `.gitignore` | A file listing local files and folders that Git should leave out when adding new files. |

### Actions and assertions

These actions enter and submit a task:

```python
task_input.fill("Read testing notes")
task_input.press("Enter")
```

This assertion checks the text:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

These snippets explain the idea. Complete code follows later.

A script that only clicks and types may finish without checking that the correct task appeared.

| Scenario | Expected behaviour | Passing outcome |
| --- | --- | --- |
| Add a normal task. | A task appears. | Its text is correct. |
| Submit an empty task. | No task is added. | The list stays empty. |

A negative test passes when invalid input is handled as expected.

### Shared work pattern

```text
Update main → Create your branch → Edit and run your test
            → Save → Commit → Push → Open a PR → Merge
            → Everyone updates main
```

Saving does not commit. Committing does not upload. Pushing does not merge.

> [!IMPORTANT]
> Enter commands in the terminal and Python code in the named `.py` file. Save before running. Copy code without the surrounding Markdown backticks.

> [!WARNING]
> Use fictional data and small, deliberate runs. Do not run load tests, security scans or continuous loops against the public website. Do not force-push or use destructive Git commands to bypass problems.

***

## 2. Prepare your Windows computer

### 2.1 Install Python and VS Code

Use Python 3.12 or 3.13 for this guide. Do not reinstall suitable existing software.

1. Install Python from [Python Downloads](https://www.python.org/downloads/) if needed.
2. Select `Add Python to PATH` if offered.
3. Install [Visual Studio Code](https://code.visualstudio.com/) if needed.
4. In VS Code, open Extensions, search for `Python` and install the extension published by Microsoft.
5. Reopen VS Code after installing software.

The extension does not install Python itself.

### 2.2 Open Command Prompt in VS Code

1. Select Terminal → New Terminal.
2. Open the dropdown beside the terminal's `+` button.
3. Select Command Prompt. If needed, use Select Default Profile → Command Prompt, then open a new terminal.

Use Command Prompt throughout this guide. If you see Python's `>>>` prompt, enter `exit()` first.

Check Python:

```bat
python --version
```

If unavailable:

```bat
py -3 --version
```

### 2.3 Check Chrome or Edge

Choose installed stable Chrome or Edge. Open it from Start and confirm you can load a website. You do not need both browsers or a signed-in personal profile.

If installation is needed, use an approved installer for [Chrome](https://www.google.com/chrome/) or [Edge](https://www.microsoft.com/edge/download).

### 2.4 Install or check Git

```bat
git --version
```

If missing, install Git for Windows from [Git Downloads](https://git-scm.com/downloads), then reopen VS Code.

Set the identity used for your commits. Replace the example values before running:

```bat
git config --global user.name "Your Name"
git config --global user.email "YOUR_GITHUB_COMMIT_EMAIL"
```

Use an email linked to GitHub or your GitHub no-reply email. These settings identify commits; they do not sign you in.

Open GitHub in your browser and sign in to your account. When Git asks you to authenticate later, follow its browser sign-in instructions. Do not paste passwords or tokens into project files.

> [!NOTE]
> Use approved installation methods on managed computers. Ask IT support when administrator access is required. Do not bypass restrictions. If one browser is unavailable, use the other approved browser.

***

## 3. Create and clone the group repository

### 3.1 Agree member numbers

Choose one coordinator for the initial setup. Give each member a number, starting at 1. Everyone still completes the testing activities on their own computer.

| Member | Personal test file | Personal branch |
| --- | --- | --- |
| 1 | `tests/test_member_1.py` | `testing/member-1` |
| 2 | `tests/test_member_2.py` | `testing/member-2` |
| 3 | `tests/test_member_3.py` | `testing/member-3` |
| 4, if present | `tests/test_member_4.py` | `testing/member-4` |
| 5, if present | `tests/test_member_5.py` | `testing/member-5` |

Examples below use Member 1. Replace member numbers in filenames, paths and branch names with your own. Keep the Python function names unchanged.

### 3.2 Coordinator: create the repository

On GitHub:

1. Create a repository, for example `automated-testing-group-01`.
2. Use the visibility approved for your group. A private repository limits access to invited people.
3. Add a README. Confirm the starting branch is `main`.
4. Put this guide in `README.md`.
5. Open Settings → Collaborators, or the equivalent access page.
6. Invite the other group members using their GitHub usernames.
7. Ask members to accept their invitations.

### 3.3 Everyone: clone the repository

Choose where you want to keep the project on your computer.

1. Open Windows File Explorer.
2. Open a folder of your choice where you can save files.
3. Click the address bar and copy the full folder path.
4. In the VS Code Command Prompt terminal, enter the command below, replacing the placeholder with your copied path. Keep the quotation marks.

```bat
cd /d "PASTE_YOUR_CHOSEN_FOLDER_PATH_HERE"
```

On the GitHub repository page, select Code → HTTPS and copy the repository URL.

Type `git clone`, add a space and paste the copied URL:

```bat
git clone PASTE_THE_COPIED_HTTPS_URL_HERE
```

Replace the placeholder. Do not type it literally.

Git creates a new project folder inside your chosen folder. Enter that new folder using its actual name. For example:

```bat
cd automated-testing-group-01
```

In VS Code, select File → Open Folder and open that project folder. Open a new Command Prompt terminal.

> [!TIP]
> Each member may choose a different location on their own computer. Use the cloned project folder for the remaining commands, not its parent folder.

### 3.4 Check the copy

```bat
git status
git remote -v
```

You should be on `main`, and `origin` should point to the shared repository. `origin` is Git's short name for that remote location.

***

## 4. Create the shared starting files

> [!IMPORTANT]
> The coordinator completes this section first. Others continue with Section 5 after the setup changes have been merged.

### 4.1 Create the setup branch

```bat
git switch main
git pull --ff-only origin main
git switch -c setup/testing-files
```

`switch -c` creates and selects a new branch. `pull --ff-only` updates the branch only when Git can move it forward directly.

### 4.2 Create the files

In VS Code's file explorer, use New File and New Folder to create:

```text
README.md
.gitignore
requirements.txt
pytest.ini
tests/
```

Keep the existing README. Git does not store empty folders. It is normal for `tests` to be absent from other members' copies until a test file has been added.

### 4.3 Create `.gitignore`

Create a file named exactly `.gitignore` in the main project folder, beside `README.md`. Do not name it `.gitignore.txt`.

Paste and save:

```gitignore
.venv/
__pycache__/
.pytest_cache/
reports/
recordings/
test-results/
.env
```

This file tells Git to leave out the local files and folders listed below. They stay on your computer but are not normally added to commits.

| Entry | What stays local |
| --- | --- |
| `.venv/` | Your project's Python environment and installed packages. |
| `__pycache__/` | Temporary files created by Python. |
| `.pytest_cache/` | Temporary information saved by pytest. |
| `reports/` | Generated HTML results reports. |
| `recordings/` | Browser recordings used for individual practice. |
| `test-results/` | Generated screenshots, traces and other browser output. |
| `.env` | A local settings file that may hold private values. This guide does not require one. |

Commit `.gitignore` itself so everyone who clones the repository uses the same rules. Create it before adding environments or generated files to Git.

Keep test source and configuration files shared:

```text
README.md
.gitignore
requirements.txt
pytest.ini
tests/test_member_1.py
tests/test_member_2.py
...
```

> [!IMPORTANT]
> `.gitignore` is not a security tool. It does not remove files already tracked by Git or erase information from earlier commits. Always inspect selected changes before committing.
>
> For this practical, recordings stay local. If your group later chooses to share a useful recorded script, copy its cleaned-up test code into an appropriately named file under `tests/` and run it before committing.

### 4.4 Create `requirements.txt`

```text
pytest-playwright
pytest-html
```

### 4.5 Create `pytest.ini`

```ini
[pytest]
testpaths = tests
addopts = -v --browser chromium
```

Members select installed Chrome or Edge through their commands, so the shared file does not need to change when members use different browsers.

### 4.6 Save, commit and push

Save the files, then run:

```bat
git status
git add .gitignore requirements.txt pytest.ini
git diff --staged
git commit -m "Add shared testing configuration and ignore rules"
git push -u origin setup/testing-files
```

`git add` selects changes for the commit. `git diff --staged` shows those selected changes. `-u` links the local branch to its GitHub branch, allowing later pushes with `git push`.

### 4.7 Merge the setup

On GitHub:

1. Open a pull request for `setup/testing-files`.
2. Set base to `main` and compare to `setup/testing-files`.
3. Inspect Files changed.
4. Confirm only intended files are included and no private data appears.
5. Merge the pull request using the available merge option.

The base is the destination. The compare branch contains the changes.

***

## 5. Prepare your branch and Python environment

### 5.1 Everyone: update and create your branch

After the setup PR has merged:

```bat
git switch main
git pull --ff-only origin main
git switch -c testing/member-1
git status
```

Use your own member number. You should now be on your personal branch and able to open `.gitignore` and the configuration files.

### 5.2 Create the virtual environment

```bat
python -m venv .venv
```

If only the Windows launcher works, use this instead:

```bat
py -3 -m venv .venv
```

A virtual environment separates this project's Python packages from other projects. A `.venv` folder should appear; the command may finish without a message.

### 5.3 Activate it

```bat
.venv\Scripts\activate.bat
```

Check:

```bat
python -c "import sys; print(sys.executable)"
```

The path should contain this project's `.venv\Scripts\python.exe`.

> [!TIP]
> If activation fails, confirm you are using Command Prompt. You can also replace `python` at the start of later commands with `.venv\Scripts\python.exe`. Do not weaken security settings.

### 5.4 Select Python in VS Code

Press Ctrl+Shift+P, search for `Python: Select Interpreter` and select the Python inside `.venv`.

### 5.5 Install packages

```bat
python -m pip install -r requirements.txt
python -m pytest --version
python -m playwright --version
```

Wait for installation to finish before running the version commands. Each version command should display a version number.

No Playwright browser download is needed for installed Chrome or Edge used in the main activities.

### 5.6 Select your browser for this terminal

Run one command:

Microsoft Edge:

```bat
set "TEST_BROWSER=msedge"
```

Google Chrome:

```bat
set "TEST_BROWSER=chrome"
```

Check:

```bat
echo %TEST_BROWSER%
```

You should see `msedge` or `chrome`. `%TEST_BROWSER%` lets later commands use your choice without changing shared files. This setting lasts only for the current Command Prompt session.

### 5.7 Create local folders and check ignore rules

Use VS Code to create `tests`, `recordings` and `reports` if missing.

Run:

```bat
git status
git check-ignore .venv/
```

`.venv/` should not appear as a new file to commit. The second command should print `.venv/`, confirming that an ignore rule matches it.

### Returning another day

Open the cloned project folder in your chosen location and a Command Prompt terminal. Activate `.venv` and set `TEST_BROWSER` again. Check your branch with `git status`. Continue your existing branch; do not create it again.

***

## 6. Explore the website

### 6.1 Try the task list

Open [Playwright TodoMVC](https://demo.playwright.dev/todomvc/) in Chrome or Edge.

1. Click `What needs to be done?`.
2. Enter `Read testing notes` and press Enter.
3. Find the task and select its checkbox.
4. Try All, Active and Completed.

The automated browser uses a separate session, not your usual signed-in profile. You do not need to delete tasks in your everyday browser before testing.

### 6.2 Inspect the input

1. Right-click the input and select Inspect.
2. Find `placeholder="What needs to be done?"` in the selected element.
3. Close Developer Tools.

An attribute is extra information attached to a page element. The placeholder supplies the input's hint text. Playwright can use it to find the input.

***

## 7. Create your first automated check

### 7.1 Create your personal file

Member 1 creates `tests/test_member_1.py`. Use your own member number.

Paste all of this code and save. Keep the indentation: spaces at the start of lines inside the function.

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

### 7.2 Run it

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed --slowmo 300
```

### What you should see

Your chosen Chrome or Edge opens, adds a task and closes. If all checks succeed, the terminal reports `1 passed`. Read the actual result; use Section 14 if it differs.

| Code or option | Meaning |
| --- | --- |
| `def test_add_task(...)` | Defines a test. pytest recognises names beginning with `test_`. |
| `page` | A browser page supplied by the Playwright pytest package. |
| `page: Page` | A type hint that helps the editor understand `page`. |
| `page.goto(URL)` | Opens the website. |
| `get_by_placeholder(...)` | Finds the task input by its hint text. |
| `exact=True` | Requires the whole hint text to match. |
| `locator(".todo-list li")` | Finds task rows using a CSS selector. |
| `task_items.locator("label")` | Finds their text labels. |
| `fill(...)` / `press("Enter")` | Enter text / submit it. |
| `to_have_count(...)` | Checks the number of rows. |
| `to_have_text([...])` | Checks the expected labels. |
| `to_have_value("")` | Checks the input is empty. |
| `--headed` | Displays the browser. |
| `--slowmo 300` | Slows actions so you can watch. |

Square brackets in the text check hold a list of expected labels. You can reuse the CSS selector without learning CSS first. Playwright's page assertions wait briefly for the expected condition; arbitrary pauses are not needed.

### 7.3 Save your first test in Git

```bat
git status
git add tests/test_member_1.py
git diff --staged
git commit -m "Add first task creation test"
git push -u origin testing/member-1
```

Use your own filename and branch. On GitHub, switch to your branch to find the file. It will not be on `main` until merged.

***

## 8. Check task completion

### 8.1 Add another test

Append this to your personal test file. Keep the existing code.

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

### 8.2 Run both tests

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed
```

If both succeed, the terminal reports `2 passed`.

`first` selects the first task row. `get_by_role("checkbox")` finds its checkbox. `check()` selects it, and `to_be_checked()` checks its state.

Each test gets a fresh browser session and creates its own task. Tests do not depend on tasks left by other tests.

***

## 9. Run one test with different inputs

An empty or spaces-only task should not be added. These negative tests pass when the list stays empty.

### 9.1 Add an import

Add this at the top of your test file, keeping its other import, URL and tests:

```python
import pytest
```

### 9.2 Add the test

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

The line starting with `@` tells pytest to run once per input. This is parametrization.

| Part | Meaning |
| --- | --- |
| `""` | No characters. |
| `" "` | One space. |
| `"   "` | Three spaces. |
| `task_text` | Receives the current input. |
| `ids` | Gives the runs readable names. |
| `task_text: str` | A type hint saying the input is text. |

### 9.3 Run and save

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed
```

Two earlier tests plus three input cases produce five runs. If all succeed, the terminal reports `5 passed`.

```bat
git add tests/test_member_1.py
git diff --staged
git commit -m "Add completion and blank input checks"
git push
```

These examples do not cover every possible invalid input.

***

## 10. Record and replay browser actions

### 10.1 Start Codegen

Check that `recordings` exists, then run:

```bat
python -m playwright codegen --channel %TEST_BROWSER% --target python-pytest -o recordings/member_1.py https://demo.playwright.dev/todomvc/
```

Codegen uses `--channel`, while pytest uses `--browser-channel`. Your shared `pytest.ini` does not configure Codegen.

### 10.2 Record a scenario

1. Enter `Try the recorder` in the recording browser.
2. Press Enter.
3. Find the text assertion control in the recording toolbar. Hover over controls to read their labels.
4. Select it, then select the new task's text.
5. Look for an `expect(...)` check in the generated code.
6. Close the recording windows.

### 10.3 Add a check if needed

If the recording has no task-text assertion, open the recording file and add this inside its test function, after the action that presses Enter:

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

The recording is separate from the five cases in your personal test file. It stays local because `recordings` is ignored by Git. A recording with only actions may finish without checking the intended result; read its code.

***

## 11. Create a results report

Check that `reports` exists, then run:

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --html=reports/member-1.html --self-contained-html
```

This runs your chosen Chrome or Edge without a visible window because it leaves out `--headed`.

Open the project in Windows File Explorer, open `reports`, then double-click `member-1.html`.

The report shows test names, results, durations and errors. Expand failed results to read more. It remains local and is not added to Git.

***

## 12. Investigate a failed check

You will deliberately introduce an incorrect expectation. This demonstrates troubleshooting, not a confirmed website defect.

### 12.1 Change one check

In `test_add_task()`, change:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

temporarily to:

```python
expect(task_labels).to_have_text(["A different task"])
```

Do not change the text entered by `fill(...)`.

### 12.2 Run that test

```bat
python -m pytest tests/test_member_1.py::test_add_task --browser-channel %TEST_BROWSER% --headed --screenshot only-on-failure --tracing retain-on-failure --output test-results/member-1-failure
```

| Option | Purpose |
| --- | --- |
| `::test_add_task` | Select only this function. |
| `--screenshot only-on-failure` | Save a screenshot if it fails. |
| `--tracing retain-on-failure` | Keep the failed run's trace. |
| `--output ...` | Choose where output is saved. |

The test should fail: it enters `Read testing notes` but expects `A different task`. Find the expected and actual text in the terminal error. Here, the test expectation is wrong.

### 12.3 Open the screenshot and trace

In VS Code, open `test-results/member-1-failure` and its generated test subfolder. Open the screenshot.

Find `trace.zip`. Right-click it and select Copy Relative Path. Replace the placeholder below with that path, keeping the quotation marks:

```bat
python -m playwright show-trace "PASTE_RELATIVE_PATH_HERE" --browser-channel %TEST_BROWSER%
```

Look through the page loading, input, Enter key and failed check.

### 12.4 Restore and rerun

Restore the correct assertion:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

Save and run:

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER%
```

If all checks succeed, the summary reports `5 passed` again.

```bat
git diff
```

If you restored the file exactly, Git may show no changes. That is normal; no extra commit is needed.

> [!IMPORTANT]
> Do not commit the deliberately wrong assertion. Restore the meaningful check before combining your work.
>
> Later runs may replace generated outputs. Copy a file elsewhere only if you want to keep it locally.

***

## 13. Combine the group files

### 13.1 Finish your branch

```bat
git status
git push
```

If your personal source file still has changes you intend to keep, run your tests, then add and commit that file before pushing. Do not add local environments, recordings, reports or traces. Use explicit filenames rather than adding everything without checking.

### 13.2 Open your pull request

On GitHub:

1. Open a pull request from `testing/member-1` to `main`, using your number.
2. Use a title such as `Add Member 1 browser tests`.
3. In Files changed, check that the changes belong to your work.
4. Ask another group member to look through the file with you.
5. Check that the assertions are correct, the deliberate mistake is gone and no private data or generated output is included.
6. Merge one member's pull request at a time.

Members use different filenames, so their guided tests can sit beside one another without replacing each other's work. Do not edit another member's file during this activity.

### 13.3 Everyone: update local main

Start with a clean working directory. If `git status` shows unfinished changes, save them in an appropriate commit before switching.

```bat
git switch main
git pull --ff-only origin main
git status
```

Merging on GitHub does not automatically update your computer. You should now see the merged member files.

### 13.4 Check the combined project once

Choose one member to run the combined tests:

```bat
python -m pytest --browser-channel %TEST_BROWSER% --html=reports/group-results.html --self-contained-html
```

If every member has only the five guided cases, there are five runs per member file. Additional practice tests increase that total.

The repeated guided cases show the same behaviours from different source files; they do not represent different functional coverage. Avoid repeatedly running the whole group suite without a reason.

If a test fails, use its filename and error message to identify the relevant member file. Make any correction on a new branch and combine it through another PR.

### 13.5 Inspect the shared history

```bat
git log --oneline --graph --decorate --all -15
```

Use an actual commit ID from that output:

```bat
git show COMMIT_ID
```

This displays what changed in the selected commit. Press `q` if Git opens a scrolling view.

For a later activity, start a new branch from updated `main`:

```bat
git switch -c practice/member-1-next
```

***

## 14. Troubleshooting and command reference

### Before attempting a fix

Save your file, read the error and check the folder, interpreter, branch and browser setting:

```bat
python -c "from pathlib import Path; import sys; print('Folder:', Path.cwd()); print('Python:', sys.executable)"
git status
echo %TEST_BROWSER%
```

The folder should be your cloned project folder in the location you chose. The Python path should contain that project's `.venv` folder.

### Common problems

| Problem | What to try |
| --- | --- |
| Python is not recognised | Reopen VS Code. Try `py -3 --version`. Review installation if neither command works. |
| Packages cannot be imported | Activate `.venv`, check the Python path and repeat `python -m pip install -r requirements.txt`. |
| Activation fails | Use Command Prompt and `.venv\Scripts\activate.bat`. |
| Browser variable displays as `%TEST_BROWSER%` or is empty | Run `set "TEST_BROWSER=msedge"` or `set "TEST_BROWSER=chrome"` in this Command Prompt terminal. |
| Chrome or Edge cannot be found | Check it opens from Start. Use the other installed, approved browser if needed and set the variable again. |
| Playwright Chromium executable is missing | For main tests include `--browser-channel %TEST_BROWSER%`. For recording include `--channel %TEST_BROWSER%`. |
| No tests are found | Save the file. Check its `.py` extension, its `test_` filename and its `test_` function names. |
| File cannot be found | Check your member number, spelling and current project folder. |
| `IndentationError` | Match the leading spaces. Use four spaces inside a function. |
| `SyntaxError` | Check quotes, brackets and colons. Do not paste Markdown backticks into Python. |
| Browser is not visible | Add `--headed`. |
| Browser closes quickly | Normal after a run. Use `--headed --slowmo 300` and read the terminal result. |
| Expected text differs | Compare spelling, capital letters and spaces in the input and check. |
| Website cannot load | Try the URL manually. Check the connection. If unavailable, save your work and retry later. |
| Locator times out | Check the website loaded and the locator matches the current page. Use Inspect or Codegen. |
| Report has no screenshot | Open screenshots separately under `test-results`. |
| Generated files disappeared | Later runs may replace output. Copy files locally first if you want to keep them. |
| Browser or download blocked by policy | Use approved software and network processes. Do not disable security controls. |
| Repository not found | Check the URL, GitHub sign-in and accepted collaborator invitation. |
| Push is rejected | Confirm authentication, access, current branch and remote. Do not force-push. |
| Nothing to commit | The file may already be committed, unchanged, unsaved or ignored. Use `git status` and `git diff`. |
| Local main does not show merged files | Run `git pull --ff-only origin main` from clean local `main`. |
| Git asks about overwriting local changes | Stop and inspect `git status`. Commit intended source changes on your work branch before switching. |
| Many environment or report files appear in Git | Check `.gitignore` is saved in the main project folder with the correct name. Read the steps below if the files were already added. |

### If `.gitignore` does not appear to work

First check whether an ignore rule matches a path:

```bat
git check-ignore -v .venv/
```

If nothing appears, check the file's name, location and contents. Make sure it is `.gitignore`, not `.gitignore.txt`.

If generated files were selected with `git add` but have not been committed, remove that selection without deleting the files:

```bat
git restore --staged .venv/
```

Use the actual unwanted path, then check `git status` again.

If a non-sensitive local folder was already committed, `.gitignore` alone does not stop Git tracking it. To stop tracking the folder while keeping your local copy:

```bat
git rm -r --cached .venv/
git status
git diff --staged
```

Use this only for a local-only folder that was mistakenly tracked, not a source folder. Review the staged removal, then commit it and the ignore rules on your branch:

```bat
git add .gitignore
git commit -m "Stop tracking local Python environment"
git push
```

Combine that correction through a PR. This removes the folder from the current project version, not from earlier Git history.

> [!WARNING]
> If credentials or private information were committed, do not treat `.gitignore` or a later deletion as a complete fix. Stop sharing the affected content and use the relevant account or organisation process to revoke exposed credentials and handle the disclosure.

### If a merge conflict appears

Do not delete the repository or run destructive reset commands.

If a local merge is in progress, `git status` identifies the conflicting files. Open each file in VS Code, compare both versions and keep the intended content. Remove conflict markers such as `<<<<<<<`, `=======` and `>>>>>>>`, save, then run the relevant tests before completing the merge.

Do not blindly accept one version of another member's file. Work through that file with its owner. If you have not resolved the conflict and want to return to the state before the local merge, use `git merge --abort` only when `git status` confirms a merge is in progress.

If `git pull --ff-only` refuses because histories have diverged, it has not started a merge. Preserve your commits and inspect the history first:

```bat
git fetch origin
git log --oneline --graph --decorate --all -15
```

### Main command reference

Use your own member number.

| Goal | Command |
| --- | --- |
| Select Edge for this terminal | `set "TEST_BROWSER=msedge"` |
| Select Chrome for this terminal | `set "TEST_BROWSER=chrome"` |
| Watch your tests | `python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed --slowmo 300` |
| Run your tests without a visible window | `python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER%` |
| Inspect changes | `git diff` |
| Select your source file | `git add tests/test_member_1.py` |
| Inspect selected changes | `git diff --staged` |
| Check an ignore rule | `git check-ignore -v .venv/` |
| Save selected changes | `git commit -m "Describe the change"` |
| Upload commits | `git push` |

***

## 15. Optional browsers and further practice

### 15.1 Try the other main browser

Set `TEST_BROWSER` to the other installed browser and rerun your personal test file. Your Python code and shared configuration stay unchanged.

### 15.2 Try Playwright Chromium, Firefox or WebKit

The following commands override the shared `addopts` for that run. Do not add a Chrome or Edge channel to Firefox or WebKit.

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

Skip unsupported or blocked optional browsers. Compare functional results, not browser speed. After upgrading Playwright, reinstall any Playwright-managed browsers you use; this does not mean reinstalling ordinary Chrome or Edge.

### 15.3 Change a task name

Start a new personal branch from updated `main`. In your file, change `Read testing notes` in both the input action and assertion. Save, run, commit and push, then combine the change through a PR.

### 15.4 Add another blank-input case

Replace the parametrization block above your blank-input function with:

```python
@pytest.mark.parametrize(
    "task_text",
    ["", " ", "   ", "    "],
    ids=["empty", "one-space", "three-spaces", "four-spaces"],
)
```

Keep the function unchanged. There is one ID per input. Your file now runs six cases.

### 15.5 Add a helper and a two-task test

A helper is a function that performs reusable steps. Add both functions to your personal test file. Keep its imports and URL.

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

Run your personal file. This adds one test. The helper performs actions; the test contains the checks. Save the working source on your branch and combine it through a PR.

### 15.6 Record another action

Try completing, editing or deleting a task manually. Record it in your main browser, read the code and reuse assertion patterns to check the result.

If expected behaviour is unclear, treat the result as an observation rather than a confirmed defect.

***

## Closing reminder

A passing test means its particular checks succeeded in that run. It does not prove that the whole website is error-free.

Keep examples small and understandable. Use failed checks to understand what happened. Share working source changes without uploading private data or local browser outputs.

```text
Choose a behaviour → Define the expectation → Automate → Run
                   → Investigate → Improve → Commit → Push → Merge
```
