# Automated Testing Tools Group Practical

> A 90-minute, hands-on introduction to browser automation using Windows and Google Chrome or Microsoft Edge.

> [!NOTE]
> ## Educational Practice Materials
>
> Use fictional task names only. Do not enter or share passwords, API keys, identification numbers, personal contact details or confidential information. Screenshots and traces may contain page content.

Learn automated testing by opening a task-list website, automating browser actions and checking results.

No previous automated testing experience is needed. You have already completed a basic Python module. This practical builds on that knowledge. Complete Python examples and explanations are provided. You do not need to build a website, learn JavaScript or create an application server.

Work in a group of 3–5. Each member uses their own computer and GitHub account. Each member creates a separate test file, saves changes on a personal branch and combines that file with the shared project.

### Practical overview

| Item | Details |
| --- | --- |
| Main lesson | 1.5 hours: 90 minutes. |
| Before the lesson | Complete the software preparation in Section 1. |
| Operating system | Windows. |
| Python knowledge | Basic Python, from the module completed earlier. |
| Main browser | Installed stable Google Chrome or Microsoft Edge. |
| Terminal | Windows Command Prompt inside VS Code. |
| Project location | A folder of your choice where you can save files. |
| Test website | [Playwright TodoMVC demonstration](https://demo.playwright.dev/todomvc/) |
| Shared project | One repository with a separate test file for each member. |
| After the lesson | Optional activities in Section 13. |

### Tools used

| Tool | What it does |
| --- | --- |
| Python | Runs the test code. |
| VS Code and its Microsoft Python extension | Help you create and edit Python files. |
| Google Chrome or Microsoft Edge | Runs the main browser activities. Choose either one. |
| Playwright | Controls the browser and checks page behaviour. |
| Playwright Codegen | Records browser actions and creates starting code. |
| pytest | Finds and runs tests. |
| pytest-html | Creates an HTML results report. |
| Git and GitHub | Save, share and combine changes. |
| Trace Viewer, used after the lesson | Helps you look back through a test run. |

### Browser choices

| Browser | When to use it | Selection |
| --- | --- | --- |
| Microsoft Edge | Main lesson option. | `--browser chromium --browser-channel msedge` |
| Google Chrome | Equally suitable main lesson option. | `--browser chromium --browser-channel chrome` |
| Playwright Chromium | Optional post-lesson practice. | `--browser chromium` without a channel |
| Playwright Firefox | Optional post-lesson practice. | `--browser firefox` |
| Playwright WebKit | Optional post-lesson practice. | `--browser webkit` |

> [!IMPORTANT]
> Chrome and Edge are Chromium-based browsers. In pytest, `--browser chromium` selects the browser family. The channel selects installed Chrome or Edge.
>
> Do not use `--browser chrome` or `--browser edge`. Use `--browser-channel chrome` or `--browser-channel msedge`.
>
> You do not need to download Playwright Chromium for the main lesson.

## Contents

1. [Before the lesson: prepare your software](#1-before-the-lesson-prepare-your-software)
2. [The 90-minute lesson plan](#2-the-90-minute-lesson-plan)
3. [Understand the workflow](#3-understand-the-workflow)
4. [Create and clone the group repository](#4-create-and-clone-the-group-repository)
5. [Create the shared starting files](#5-create-the-shared-starting-files)
6. [Prepare your branch and Python environment](#6-prepare-your-branch-and-python-environment)
7. [Explore and run your first test](#7-explore-and-run-your-first-test)
8. [Check task completion](#8-check-task-completion)
9. [Run one test with different inputs](#9-run-one-test-with-different-inputs)
10. [Record and replay browser actions](#10-record-and-replay-browser-actions)
11. [Create a results report](#11-create-a-results-report)
12. [Combine the group files](#12-combine-the-group-files)
13. [Optional post-lesson practice](#13-optional-post-lesson-practice)
14. [Troubleshooting and command reference](#14-troubleshooting-and-command-reference)

***

## 1. Before the lesson: prepare your software

Complete these steps before starting the 90-minute lesson. Downloads, account setup and installation are not included in the lesson timing.

### 1.1 Check Python and VS Code

Use Python 3.12 or 3.13 for this guide. Do not reinstall suitable existing software.

1. Install Python from [Python Downloads](https://www.python.org/downloads/) if needed.
2. Select `Add Python to PATH` if offered.
3. Install [VS Code](https://code.visualstudio.com/) if needed.
4. In VS Code, open Extensions, search for `Python` and install the extension published by Microsoft.
5. Reopen VS Code after installing software.

The extension does not install Python itself.

### 1.2 Open Command Prompt in VS Code

1. Select Terminal → New Terminal.
2. Open the dropdown beside the terminal's `+` button.
3. Select Command Prompt. If needed, use Select Default Profile → Command Prompt, then open a new terminal.

Use Command Prompt throughout this guide. If you see Python's `>>>` prompt, enter `exit()` first.

```bat
python --version
```

If unavailable:

```bat
py -3 --version
```

You should see a Python version.

### 1.3 Check Chrome or Edge

Choose installed stable Chrome or Edge. Open it from Start and confirm you can load the [demonstration website](https://demo.playwright.dev/todomvc/).

You do not need both browsers or a signed-in personal browser profile.

If installation is needed, use an approved installer for [Chrome](https://www.google.com/chrome/) or [Edge](https://www.microsoft.com/edge/download).

### 1.4 Check Git and GitHub

```bat
git --version
```

If missing, install Git for Windows from [Git Downloads](https://git-scm.com/downloads), then reopen VS Code.

Replace the example values and set your commit identity:

```bat
git config --global user.name "Your Name"
git config --global user.email "YOUR_GITHUB_COMMIT_EMAIL"
```

Use an email linked to GitHub or your GitHub no-reply email. These settings identify commits; they do not sign you in.

Sign in to GitHub in your browser. When Git later asks you to authenticate, follow its browser sign-in instructions. Never put passwords or tokens in project files.

### 1.5 Agree the group details

Before the lesson, agree:

- Who will coordinate the initial repository setup.
- A group identifier for the repository name.
- Each member's number, starting at 1.
- Each member's GitHub username.

> [!NOTE]
> Use approved software installation methods on managed computers. Ask IT support when administrator access is needed. Do not bypass restrictions. If one browser is unavailable, use the other approved browser.

***

## 2. The 90-minute lesson plan

| Time | Activity | Sections |
| --- | --- | --- |
| 0–10 minutes | Create and clone the repository; share the starting files. | 3–5 |
| 10–20 minutes | Create personal branches, install packages and choose a browser. | 6 |
| 20–35 minutes | Explore the website and run the first test. | 7 |
| 35–45 minutes | Add the task-completion test. | 8 |
| 45–55 minutes | Try three blank-input cases using one test. | 9 |
| 55–70 minutes | Record browser actions, add a check and replay. | 10 |
| 70–75 minutes | Generate and open an HTML report. | 11 |
| 75–90 minutes | Push, combine the group files and update local main. | 12 |
| Total | 90 minutes | |

The timing assumes the software and accounts in Section 1 are ready and the network is working. If setup takes longer, save your progress and continue unfinished steps after the lesson. Do not skip checks or hide errors to keep to the timing.

The detailed explanations are there when you need them. During each activity, follow the numbered steps first and use the explanation tables to understand unfamiliar lines.

Failure investigation, additional browsers and extended test writing are in the optional post-lesson section.

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
| Virtual environment | A separate set of Python packages for this project. |
| Browser channel | Installed Chrome or Edge selected for a run. |
| Repository | A project whose changes are tracked by Git. |
| Branch | A separate line of work in a repository. |
| Commit | A saved record of selected changes on your computer. |
| Push | Upload commits to GitHub. |
| Pull request, or PR | A request to combine a branch with another branch. |
| Merge | Combine changes from branches. |
| `.gitignore` | A file listing local files and folders to leave out when adding new files to Git. |

### Actions and assertions

Actions:

```python
task_input.fill("Read testing notes")
task_input.press("Enter")
```

Assertion:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

These are explanatory snippets, not complete tests. Complete code follows later.

A script that only clicks and types may finish without checking that the correct task appeared.

A negative test can pass: submitting an empty task should leave the list empty. The test passes when that expected behaviour occurs.

### Shared work pattern

```text
Update main → Create a branch → Edit and run
            → Save → Commit → Push → Open a PR → Merge
            → Everyone updates main
```

Saving does not commit. Committing does not upload. Pushing does not merge.

> [!IMPORTANT]
> Enter commands in the terminal and Python code in the named `.py` file. Save before running. Copy only code inside a code block, not its surrounding backticks.

> [!WARNING]
> Use fictional data and small, deliberate runs. Do not run load tests, security scans or continuous loops against the public website. Do not force-push or use destructive Git commands to bypass a problem.

***

## 4. Create and clone the group repository

### 4.1 Use your member number

| Member | Personal test file | Personal branch |
| --- | --- | --- |
| 1 | `tests/test_member_1.py` | `testing/member-1` |
| 2 | `tests/test_member_2.py` | `testing/member-2` |
| 3 | `tests/test_member_3.py` | `testing/member-3` |
| 4, if present | `tests/test_member_4.py` | `testing/member-4` |
| 5, if present | `tests/test_member_5.py` | `testing/member-5` |

Examples use Member 1. Replace member numbers in filenames, paths and branch names with your own. Keep the Python function names unchanged.

### 4.2 Coordinator: create the repository

On GitHub:

1. Create a repository, for example `automated-testing-group-01`.
2. Use approved visibility. A private repository limits access to invited people.
3. Add a README and confirm the starting branch is `main`.
4. Put this guide in `README.md`.
5. Open Settings → Collaborators, or the equivalent access page.
6. Invite the group members using their GitHub usernames.
7. Members accept the invitations.

### 4.3 Everyone: clone the repository

Choose where to keep the project on your computer.

1. Open Windows File Explorer.
2. Open a folder of your choice where you can save files.
3. Click the address bar and copy the full path.
4. In Command Prompt, replace the placeholder below with that path. Keep the quotation marks.

```bat
cd /d "PASTE_YOUR_CHOSEN_FOLDER_PATH_HERE"
```

On GitHub, select Code → HTTPS and copy the repository URL. Replace the placeholder below:

```bat
git clone PASTE_THE_COPIED_HTTPS_URL_HERE
```

Git creates a project folder inside your chosen folder. Enter it using its actual name, for example:

```bat
cd automated-testing-group-01
```

In VS Code, use File → Open Folder to open that project folder. Open a new Command Prompt terminal.

```bat
git status
git remote -v
```

You should be on `main`. `origin`, Git's short name for the shared remote location, should point to your group repository.

> [!TIP]
> Members may choose different locations on their own computers. Run the remaining commands inside the cloned project folder, not its parent folder.

***

## 5. Create the shared starting files

> [!IMPORTANT]
> The coordinator completes this section first. Other members continue with Section 6 after these changes have been merged.

### 5.1 Create a setup branch

```bat
git switch main
git pull --ff-only origin main
git switch -c setup/testing-files
```

`switch -c` creates a branch. `pull --ff-only` updates a branch only when Git can move it directly forward.

### 5.2 Create `.gitignore`

In VS Code, create `.gitignore` beside `README.md`. Use that exact name, not `.gitignore.txt`.

```gitignore
.venv/
__pycache__/
.pytest_cache/
reports/
recordings/
test-results/
.env
```

This tells Git to leave out these local files and folders when adding new files. They remain on your computer.

| Entry | What stays local |
| --- | --- |
| `.venv/` | Your Python environment and installed packages. |
| `__pycache__/` | Temporary Python files. |
| `.pytest_cache/` | Temporary pytest information. |
| `reports/` | Generated HTML reports. |
| `recordings/` | Individual browser-recording experiments. |
| `test-results/` | Screenshots, traces and other generated output. |
| `.env` | A possible local settings file. This guide does not require one. |

Commit `.gitignore` itself so everyone uses the same rules. Create it before adding environments or outputs to Git.

> [!IMPORTANT]
> `.gitignore` is not a security tool. It does not stop tracking files already added to Git or erase earlier commits. Inspect selected changes before committing.

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

Keep `--browser chromium`. Members select Chrome or Edge through their commands.

### 5.5 Commit, push and merge the setup

Save the files:

```bat
git add .gitignore requirements.txt pytest.ini
git diff --staged
git commit -m "Add testing configuration and ignore rules"
git push -u origin setup/testing-files
```

`git add` selects changes. `git diff --staged` displays them. `-u` links your local branch to its GitHub branch.

On GitHub:

1. Open a PR from `setup/testing-files` to `main`.
2. Check base is `main` and compare is `setup/testing-files`.
3. Inspect Files changed.
4. Confirm only intended files appear, then merge.

The base is the destination. The compare branch contains the proposed changes.

***

## 6. Prepare your branch and Python environment

### 6.1 Update and create your branch

Everyone runs, using their member number:

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

The Python path should contain this project's `.venv\Scripts\python.exe`.

In VS Code, press Ctrl+Shift+P, search for `Python: Select Interpreter` and select the Python inside `.venv`.

### 6.3 Install packages

```bat
python -m pip install -r requirements.txt
python -m pytest --version
python -m playwright --version
```

Wait for installation before running the version commands. No Playwright browser download is needed for the installed Chrome or Edge used here.

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

### 6.5 Create folders and check Git

In VS Code, create:

```text
tests/
recordings/
reports/
```

Git does not store empty folders. Each member may need to create them locally.

```bat
git status
git check-ignore .venv/
```

The second command should print `.venv/`. Your environment should not appear as new files to commit.

> [!TIP]
> When you return another day, open this project folder, activate `.venv` and set `TEST_BROWSER` again. Continue your existing branch; do not recreate it.

***

## 7. Explore and run your first test

### 7.1 Try the website manually

Open [Playwright TodoMVC](https://demo.playwright.dev/todomvc/) in your usual browser.

1. Enter `Read testing notes` in `What needs to be done?`.
2. Press Enter and find the new task.
3. Select its checkbox.
4. Try All, Active and Completed.

The automated browser uses a separate session. You do not need to clear tasks from your usual browser before testing.

### 7.2 Create your personal test file

Member 1 creates `tests/test_member_1.py`. Use your own number.

Paste all the code below and save. Keep the indentation inside the function.

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

Your chosen browser opens, adds the task and closes. If all checks succeed, the terminal reports `1 passed`.

| Code or option | Meaning |
| --- | --- |
| `def test_add_task(...)` | Defines a test. pytest recognises `test_` function names. |
| `page` | A browser page supplied by the Playwright pytest package. |
| `page: Page` | A type hint that helps the editor understand `page`. |
| `page.goto(URL)` | Opens the website. |
| `get_by_placeholder(...)` | Finds the input using its hint text. |
| `exact=True` | Requires the whole hint text to match. |
| `locator(".todo-list li")` | Finds task rows using a CSS selector. |
| `task_items.locator("label")` | Finds task text inside those rows. |
| `fill(...)` / `press("Enter")` | Enter text / submit it. |
| `to_have_count(...)` | Checks the number of rows. |
| `to_have_text([...])` | Checks the expected task labels. |
| `to_have_value("")` | Checks the input is empty. |
| `--headed` | Shows the browser. |
| `--slowmo 300` | Slows actions so you can watch. |

You can reuse the CSS selector without learning CSS first. Square brackets contain a list of expected labels. Playwright's page assertions wait briefly for the expected condition; arbitrary pauses are not needed.

### 7.4 Commit and push

```bat
git add tests/test_member_1.py
git diff --staged
git commit -m "Add first task creation test"
git push -u origin testing/member-1
```

Use your own filename and branch. The file is on your branch, not `main`, until merged.

***

## 8. Check task completion

### 8.1 Append another test

Add this below the first test in your file. Keep the existing code.

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

### 8.2 Save and run

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed
```

If both tests succeed, the terminal reports `2 passed`.

`first` selects the first row. `get_by_role("checkbox")` finds its checkbox. `check()` selects it. `to_be_checked()` checks its state.

Each test receives a fresh browser session and creates its own task. It does not rely on tasks from another test.

***

## 9. Run one test with different inputs

An empty or spaces-only task should not be added. This negative test passes when the list stays empty.

### 9.1 Add the import

Add at the top of your file, keeping the existing import, URL and tests:

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

These examples do not cover every possible invalid input.

***

## 10. Record and replay browser actions

Use the next 15 minutes to record one short scenario, check the generated code and replay it. The explanations below are there to help if a step is unfamiliar.

### 10.1 Understand recording and replay

Codegen watches your actions in a browser and creates Python code.

```text
Recording: You type and click → Codegen creates code
Replaying: You run the test → Playwright types and clicks
```

Use one scenario:

```text
Open the website → Add “Try the recorder” → Check its text
```

Recording actions alone is not enough. An assertion checks that the expected task appeared.

### 10.2 Check the terminal

You should still be in the project folder with `.venv` active. Check your browser:

```bat
echo %TEST_BROWSER%
```

If needed, choose Edge with `set "TEST_BROWSER=msedge"` or Chrome with `set "TEST_BROWSER=chrome"`. Use the same terminal. Check that `recordings` exists.

### 10.3 Start the recorder

```bat
python -m playwright codegen --channel %TEST_BROWSER% --target python-pytest -o recordings/member_1.py https://demo.playwright.dev/todomvc/
```

Use your member number.

| Part | Meaning |
| --- | --- |
| `codegen` | Start the recorder. |
| `--channel %TEST_BROWSER%` | Use your selected installed browser. |
| `--target python-pytest` | Generate Python code for pytest. |
| `-o recordings/member_1.py` | Save code in this file. |
| Website address | Open this page. |

> [!IMPORTANT]
> Codegen uses `--channel`. pytest uses `--browser-channel`. Do not interchange these option names.

### 10.4 Find the recording windows

You should see a browser and Playwright Inspector.

| Window | What to do |
| --- | --- |
| Recording browser | Perform your clicks and typing. |
| Playwright Inspector | Watch the generated code. |

Move the windows so you can see both. Use the browser opened by Codegen, not another browser window you opened earlier.

### 10.5 Record adding one task

In the recording browser:

1. Confirm the task list is empty.
2. Click `What needs to be done?`.
3. Type `Try the recorder`.
4. Press Enter.
5. Confirm the task appears. Do not add more tasks.

Look at Inspector. Code should appear for opening the website, entering text and pressing Enter. An extra recorded click is fine for this first activity.

### 10.6 Try recording a check

1. Hover over the recording-toolbar buttons to read their labels.
2. Find the text assertion control, usually labelled `Assert text`.
3. Select it, then select the task text `Try the recorder`.
4. Confirm the text if prompted.
5. Look for an `expect(...)` line in the code.

> [!TIP]
> If you cannot find the control, continue. Section 10.9 provides a complete example with the check included.

### 10.7 Finish recording

Close the recording browser and Inspector. Wait for the terminal to be ready.

Open `recordings/member_1.py` in VS Code, using your number.

### 10.8 Read the main actions

The recorded actions may look like:

```python
page.get_by_placeholder("What needs to be done?").fill(
    "Try the recorder"
)
page.get_by_placeholder("What needs to be done?").press("Enter")
```

| Code | Meaning |
| --- | --- |
| `get_by_placeholder(...)` | Find the input using its hint text. |
| `fill(...)` | Enter the task name. |
| `press("Enter")` | Submit it. |

Generated code may look different because the recorder can find an element in different ways. Start by identifying the website address, entered task text and Enter action.

### 10.9 Make sure there is a check

Look for an `expect(...)` line checking the task text. If it is missing, add this after the Enter action, inside the test function:

```python
expect(page.locator(".todo-list li label")).to_have_text(
    ["Try the recorder"]
)
```

Match the indentation. Make sure `expect` is imported at the top.

If you are unsure where the check belongs, use this complete example to compare with your file. You can replace the recording file's contents with it if needed:

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

The locator finds task labels. The assertion checks that those labels match the expected list containing one task. Save the file.

### 10.10 Replay

```bat
python -m pytest recordings/member_1.py --browser-channel %TEST_BROWSER% --headed --slowmo 300
```

Playwright opens the page, enters the task, submits it and checks the text. The browser then closes. If this one test succeeds, the terminal reports `1 passed`.

The browser family is already set to `chromium` in `pytest.ini`. Use `--browser-channel`, not `--browser chrome`, to select installed Chrome.

### 10.11 Understand the result and file location

```text
Actions → Do something
Assertions → Check what happened
```

A successful run containing only actions does not explicitly check the task text. With the assertion included, a successful run confirms that the text matched.

Keep this recording in `recordings/`. It stays local through `.gitignore` and does not change the five-case count in your personal file under `tests/`.

If a recording fails, check the input and expected text, ensure only one task was recorded and read the error. For longer investigation, use Section 13.1 after the lesson.

***

## 11. Create a results report

Check that `reports` exists:

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --html=reports/member-1.html --self-contained-html
```

This runs without displaying the browser because `--headed` is omitted.

In Windows File Explorer, open your project folder, open `reports`, then double-click `member-1.html`.

Find the test names, results and durations. Expand errors if any appear. The generated report stays local through `.gitignore`.

***

## 12. Combine the group files

### 12.1 Check and push your branch

```bat
git status
git push
```

If your source file has changes you want to keep, run it, add that file, inspect `git diff --staged`, commit and push. Do not add reports, environments, recordings or traces.

### 12.2 Open and merge your PR

On GitHub:

1. Open a PR from `testing/member-1` to `main`, using your number.
2. Use a title such as `Add Member 1 browser tests`.
3. Ask another member to look through Files changed with you.
4. Confirm the changes belong to your file, checks are meaningful and no private data or local outputs appear.
5. Merge one member's PR at a time.

Do not edit another member's test file during this activity. Separate filenames allow the group files to sit beside each other.

### 12.3 Everyone: update local main

Start with a clean working directory. Commit intended unfinished source changes on your branch before switching.

```bat
git switch main
git pull --ff-only origin main
git status
```

You should now see the merged member files. A GitHub merge does not update your computer automatically.

### 12.4 Run the combined project once

Choose one member to run:

```bat
python -m pytest --browser-channel %TEST_BROWSER% --html=reports/group-results.html --self-contained-html
```

With only the guided cases, there are five runs per member file. Additional tests increase the total. Repeated guided cases do not mean additional unique functional coverage.

If this final run needs more time, save the result and continue investigating after the lesson. Avoid repeated full-group runs without a reason.

### End of the main lesson

Keep your source in the shared repository and your generated outputs locally. The next section provides optional activities to continue after the lesson.

***

## 13. Optional post-lesson practice

Choose activities that help you revisit something unfamiliar or explore further. Work at your own pace. Suggested times are planning guides, not limits.

| Activity | Suggested time | Main focus |
| --- | --- | --- |
| 13.1 Investigate a deliberate failure | 15–20 minutes | Errors, screenshots and traces. |
| 13.2 Inspect a page element | 5–10 minutes | How the input locator relates to the page. |
| 13.3 Try another browser | 10–15 minutes, plus any downloads | Reuse the same tests. |
| 13.4 Expand input examples | 10–15 minutes | Parametrization. |
| 13.5 Use a reusable helper | 15–20 minutes | Reduce repeated actions. |
| 13.6 Improve a recording | 15–20 minutes | Turn generated code into a useful shared test. |
| 13.7 Inspect Git history | 5–10 minutes | Find saved changes. |

Before changing shared source again, update clean local `main` and create a new branch:

```bat
git switch main
git pull --ff-only origin main
git switch -c practice/member-1-follow-up
```

Use your number. On a later session, continue that branch rather than creating it again. Run your personal file after changes, then commit, push and combine source changes through a PR.

### 13.1 Investigate a deliberate failure

A failed test does not automatically mean the website is broken. In this activity, the test expectation will be deliberately wrong.

#### Change one check

In `test_add_task()`, temporarily replace:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

with:

```python
expect(task_labels).to_have_text(["A different task"])
```

Do not change the entered text in `fill(...)`.

#### Run just that test

```bat
python -m pytest tests/test_member_1.py::test_add_task --browser-channel %TEST_BROWSER% --headed --screenshot only-on-failure --tracing retain-on-failure --output test-results/member-1-failure
```

| Option | Purpose |
| --- | --- |
| `::test_add_task` | Run only that function. |
| `--screenshot only-on-failure` | Save a screenshot if it fails. |
| `--tracing retain-on-failure` | Keep the failed run's trace. |
| `--output ...` | Choose the output folder. |

The test should fail because entered and expected text differ. Find the expected and actual values in the error.

#### Open the screenshot and trace

In VS Code, open `test-results/member-1-failure` and its generated test subfolder. Open the screenshot.

Find `trace.zip`, right-click it and select Copy Relative Path. Replace the placeholder with that path, keeping the quotes:

```bat
python -m playwright show-trace "PASTE_RELATIVE_PATH_HERE" --browser-channel %TEST_BROWSER%
```

Select the actions in order and look at page loading, input, Enter and the failed check.

#### Restore and rerun

Restore:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER%
git diff
```

With only the guided cases, a successful run reports `5 passed`. If the file was restored exactly, Git may show no changes and no extra commit is needed.

> [!IMPORTANT]
> Do not commit the deliberate mistake or delete the assertion to hide the failure. Restore the meaningful check. Later runs may replace generated output; copy it elsewhere first only if you want to keep it locally.

### 13.2 Inspect the task input

1. Open the demonstration website in Chrome or Edge.
2. Right-click the task input and select Inspect.
3. Find `placeholder="What needs to be done?"` in the selected element.
4. Compare this with `get_by_placeholder(...)` in your test.

An attribute is extra information attached to a page element. The placeholder supplies the hint text that your locator uses.

### 13.3 Try another browser

#### The other installed main browser

Choose the other browser with `set "TEST_BROWSER=chrome"` or `set "TEST_BROWSER=msedge"`, then rerun your personal file. The source stays unchanged.

#### Playwright-managed browsers

The commands below override shared `addopts` for that run. Do not add a Chrome or Edge channel to Firefox or WebKit.

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

Ordinary Firefox does not replace Playwright Firefox. Playwright WebKit is not installed Safari. Skip unsupported or blocked options rather than bypassing restrictions.

Compare functional results, not browser speed. These runs are not performance benchmarks. After upgrading Playwright, reinstall its managed browsers if you use them; this does not mean reinstalling ordinary Chrome or Edge.

### 13.4 Expand input examples

#### Add another blank-input case

Replace the parametrization block above your blank-input function with:

```python
@pytest.mark.parametrize(
    "task_text",
    ["", " ", "   ", "    "],
    ids=["empty", "one-space", "three-spaces", "four-spaces"],
)
```

Keep the function unchanged. There is one ID per input. Your file now runs six cases if this is the only addition.

#### Change a valid task name

In the add-task test, change `Read testing notes` in both the input and assertion. Save and rerun. Changing only one of them may make the test fail because the expected and entered values differ.

### 13.5 Use a helper to add two tasks

A helper is a function that performs reusable steps. Append both functions below to your personal file. Keep the imports and URL.

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

Run your personal file. This adds one test. The helper performs actions; the test contains the checks.

### 13.6 Improve a recorded test

1. Try editing or deleting a task manually.
2. Record the action with Codegen using Section 10.
3. Read the generated code and remove unnecessary actions.
4. Add a useful assertion for the resulting task text or count.
5. Add the working test to your own file under `tests/` if you want to share it.
6. Give it a name different from existing test functions.
7. Run, commit and push the source, then combine it through a PR.

Keep experiments in ignored `recordings/`. If expected behaviour is unclear, treat it as an observation rather than a confirmed defect.

### 13.7 Inspect Git history

```bat
git log --oneline --graph --decorate --all -15
```

Use an actual commit ID from the output:

```bat
git show COMMIT_ID
```

This displays what changed. Press `q` if Git opens a scrolling view.

***

## 14. Troubleshooting and command reference

### Before attempting a fix

Save the file, read the error and check the folder, Python, branch and browser:

```bat
python -c "from pathlib import Path; import sys; print('Folder:', Path.cwd()); print('Python:', sys.executable)"
git status
echo %TEST_BROWSER%
```

The folder should be your cloned project folder. Python should come from its `.venv`.

### Common problems

| Problem | What to try |
| --- | --- |
| Python is not recognised | Reopen VS Code. Try `py -3 --version`. Review installation if neither works. |
| Packages cannot be imported | Activate `.venv`, check Python's path and repeat `python -m pip install -r requirements.txt`. |
| Activation fails | Use Command Prompt and `.venv\Scripts\activate.bat`. Alternatively replace `python` with `.venv\Scripts\python.exe` in later commands. |
| Browser variable is empty or prints `%TEST_BROWSER%` | Set it again in this Command Prompt terminal. |
| Chrome or Edge cannot be found | Check it opens from Start. Use the other installed, approved browser if needed. |
| `invalid choice: 'chrome'` | Use `--browser chromium` in `pytest.ini` and `--browser-channel chrome` in pytest commands. |
| Playwright Chromium executable is missing | For main tests include `--browser-channel %TEST_BROWSER%`; for recording include `--channel %TEST_BROWSER%`. |
| No tests are found | Save the file. Check its `.py` extension, `test_` filename and `test_` function names. |
| File cannot be found | Check spelling, member number and project folder. |
| `IndentationError` | Match leading spaces. Use four spaces inside a function. |
| `SyntaxError` | Check quotes, brackets and colons. Do not paste Markdown backticks into code. |
| Browser is not visible | Add `--headed`. |
| Browser closes quickly | Normal after a run. Use `--headed --slowmo 300` and read the terminal result. |
| Expected text differs | Compare spelling, capital letters and spaces in input and assertion. |
| Website cannot load | Try the URL manually. Check the connection. Save and retry later if unavailable. |
| Locator times out | Check the page loaded and the locator matches. Use Inspect or Codegen. |
| Report has no screenshot | Open screenshots separately under `test-results`. |
| Generated output disappeared | Later runs may replace it. Copy it locally first if needed. |
| Browser or download blocked by policy | Use approved processes. Do not disable security controls. |
| Repository not found | Check URL, sign-in and accepted invitation. |
| Push rejected | Check authentication, access, branch and remote. Do not force-push. |
| Nothing to commit | The file may be unchanged, already committed, unsaved or ignored. Use `git status` and `git diff`. |
| Local main lacks merged files | Run `git pull --ff-only origin main` from clean local `main`. |
| Git warns about overwriting changes | Stop and inspect `git status`. Commit intended source changes on your branch before switching. |
| Many generated files appear in Git | Check `.gitignore` exists in the project root with the correct name. See below. |

### If `.gitignore` does not appear to work

```bat
git check-ignore -v .venv/
```

If no rule is displayed, check the name, location and contents of `.gitignore`.

If a folder was selected with `git add` but not committed, remove that selection without deleting it:

```bat
git restore --staged .venv/
```

If a non-sensitive local-only folder was already committed, stop tracking it while keeping your local copy:

```bat
git rm -r --cached .venv/
git status
git diff --staged
```

Use the actual unwanted path, not a source folder. Review the removal, then commit it with the ignore rules on your branch:

```bat
git add .gitignore
git commit -m "Stop tracking local Python environment"
git push
```

Combine through a PR. This does not remove the folder from earlier history.

> [!WARNING]
> If credentials or private information were committed, ignore rules and later deletion are not a complete fix. Stop sharing the affected content and use the relevant account or organisation process to revoke credentials and handle the disclosure.

### If a merge conflict appears

Do not delete the repository or run destructive reset commands. Use `git status` to identify the current state.

If a local merge is in progress, open conflicting files in VS Code and compare the versions with the file's owner. Keep the intended content and remove markers such as `<<<<<<<`, `=======` and `>>>>>>>`. Save and test before completing the merge.

If you need to return to the state before that local merge, use `git merge --abort` only when `git status` confirms a merge is in progress.

If `git pull --ff-only` refuses because histories have diverged, it has not started a merge. Preserve commits and inspect:

```bat
git fetch origin
git log --oneline --graph --decorate --all -15
```

### Main command reference

Use your own member number.

| Goal | Command |
| --- | --- |
| Choose Edge | `set "TEST_BROWSER=msedge"` |
| Choose Chrome | `set "TEST_BROWSER=chrome"` |
| Watch your tests | `python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed --slowmo 300` |
| Run without a visible browser | `python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER%` |
| Inspect changes | `git diff` |
| Select your source | `git add tests/test_member_1.py` |
| Inspect selected changes | `git diff --staged` |
| Check an ignore rule | `git check-ignore -v .venv/` |
| Save selected changes | `git commit -m "Describe the change"` |
| Upload commits | `git push` |

***

## Closing reminder

A passing test means its particular checks succeeded in that run. It does not prove the whole website is error-free.

Keep examples small and understandable. Use failures to understand what happened. Share working source without uploading private data or local browser outputs.

```text
Choose a behaviour → Define the expectation → Automate → Run
                   → Investigate → Improve → Commit → Push → Merge
```
