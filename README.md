# Automated Testing Tools Group Practical

> A two-hour, hands-on introduction to browser automation using Windows and Google Chrome or Microsoft Edge.

> [!NOTE]
> ## Educational Practice Materials
>
> Use fictional task names and the published demonstration login details only. Do not enter or share personal passwords, API keys, identification numbers, personal contact details or confidential information. Screenshots and traces may contain page content.

Learn automated testing by opening demonstration websites, automating browser actions and checking results.

No previous automated testing experience is needed. You have already completed a basic Python module. This practical builds on that knowledge. Complete Python examples and explanations are provided. You do not need to build a website, learn JavaScript or create an application server.

Work in a group of 3–5. Every member completes the guided testing activities on their own computer and creates their own test file. Do not divide the guided tests among members. Help one another solve problems, but run your own tests before committing your file. The coordinator prepares only the shared repository and starting files.

### Practical overview

| Item | Details |
| --- | --- |
| Main lesson | 2 hours: 120 minutes. |
| Before the lesson | Complete software and account preparation in Section 1. |
| Operating system | Windows. |
| Python knowledge | Basic Python, from the module completed earlier. |
| Main browser | Installed stable Google Chrome or Microsoft Edge. |
| Terminal | Windows Command Prompt inside VS Code. |
| Project location | A folder of your choice where you can save files. |
| Task-list website | [Playwright TodoMVC](https://demo.playwright.dev/todomvc/) |
| Login website | [The Internet login demonstration](https://the-internet.herokuapp.com/login) |
| Shared project | One repository with a separate test file for each member. |
| Guided cases per member | Seven: five task-list cases and two login cases. |
| After the lesson | Optional activities in Section 14. |

### Tools used

| Tool | What it does |
| --- | --- |
| Python | Runs the test code. |
| VS Code and its Microsoft Python extension | Help you create and edit Python files. |
| Google Chrome or Microsoft Edge | Runs the main browser activities. Choose either one. |
| Playwright | Controls the browser and checks page behaviour. |
| Playwright Codegen | Records actions and creates starting code. |
| pytest | Finds and runs tests. |
| pytest-html | Creates an HTML results report. |
| Git and GitHub | Save, share and combine changes. |
| Trace Viewer, used after the lesson | Helps you look back through a run. |

Codegen and Trace Viewer are included with Playwright.

### Browser choices

| Browser | When to use it | Selection |
| --- | --- | --- |
| Microsoft Edge | Main option. | `--browser chromium --browser-channel msedge` |
| Google Chrome | Equally suitable main option. | `--browser chromium --browser-channel chrome` |
| Playwright Chromium | Optional post-lesson practice. | `--browser chromium` without a channel |
| Playwright Firefox | Optional post-lesson practice. | `--browser firefox` |
| Playwright WebKit | Optional post-lesson practice. | `--browser webkit` |

> [!IMPORTANT]
> Chrome and Edge are Chromium-based browsers. In pytest, `--browser chromium` selects the browser family. The channel selects installed Chrome or Edge.
>
> Do not use `--browser chrome` or `--browser edge`. Use `--browser-channel chrome` or `--browser-channel msedge`.
>
> No Playwright Chromium download is needed for the main Chrome or Edge activities.

## Contents

1. [Before the lesson: prepare your software](#1-before-the-lesson-prepare-your-software)
2. [The two-hour lesson plan](#2-the-two-hour-lesson-plan)
3. [Understand the workflow](#3-understand-the-workflow)
4. [Create and clone the group repository](#4-create-and-clone-the-group-repository)
5. [Create the shared starting files](#5-create-the-shared-starting-files)
6. [Prepare your branch and Python environment](#6-prepare-your-branch-and-python-environment)
7. [Explore and run your first test](#7-explore-and-run-your-first-test)
8. [Check task completion](#8-check-task-completion)
9. [Run one test with different inputs](#9-run-one-test-with-different-inputs)
10. [Record and replay browser actions](#10-record-and-replay-browser-actions)
11. [Try a simple login](#11-try-a-simple-login)
12. [Create a results report](#12-create-a-results-report)
13. [Combine the group files](#13-combine-the-group-files)
14. [Optional post-lesson practice](#14-optional-post-lesson-practice)
15. [Simple syntax reference](#15-simple-syntax-reference)
16. [Troubleshooting and command reference](#16-troubleshooting-and-command-reference)

***

## 1. Before the lesson: prepare your software

Complete these steps before starting the two-hour practical. Downloads, account creation and software installation are not included in the lesson timing.

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

Use Command Prompt throughout. If you see Python's `>>>` prompt, enter `exit()` first.

```bat
python --version
```

If unavailable:

```bat
py -3 --version
```

You should see a Python version.

### 1.3 Check Chrome or Edge

Open your chosen stable Chrome or Edge from Start. Check that both demonstration websites in the overview load. No personal browser sign-in is needed.

If needed, use an approved installer for [Chrome](https://www.google.com/chrome/) or [Edge](https://www.microsoft.com/edge/download).

### 1.4 Check Git and GitHub

```bat
git --version
```

If missing, install Git for Windows from [Git Downloads](https://git-scm.com/downloads), then reopen VS Code.

Replace these example values before running:

```bat
git config --global user.name "Your Name"
git config --global user.email "YOUR_GITHUB_COMMIT_EMAIL"
```

Use an email linked to GitHub or your GitHub no-reply email. These identify commits; they do not sign you in.

Sign in to GitHub in your browser. When Git asks for authentication later, follow its browser sign-in instructions. Never put passwords or tokens in project files.

### 1.5 Agree group details

Agree the coordinator, group identifier, member numbers starting at 1, and GitHub usernames.

> [!NOTE]
> Use approved installation methods on managed computers. Ask IT support when administrator access is required. Do not bypass restrictions. If one browser is unavailable, use the other approved browser.

***

## 2. The two-hour lesson plan

| Time | Activity | Sections |
| --- | --- | --- |
| 0–15 minutes | Create and clone the repository; share starting files. | 3–5 |
| 15–30 minutes | Prepare branches, Python environments and browser selection. | 6 |
| 30–45 minutes | Explore the website and run the first test. | 7 |
| 45–55 minutes | Add the completion test. | 8 |
| 55–65 minutes | Run blank-input cases. | 9 |
| 65–80 minutes | Record actions, add a check and replay. | 10 |
| 80–100 minutes | Add and run two login tests. | 11 |
| 100–105 minutes | Generate and open a report. | 12 |
| 105–120 minutes | Combine group files and update local main. | 13 |
| Total | 120 minutes | |

Timing assumes Section 1 is complete and the network is working. If setup or debugging takes longer, save your progress and finish the remaining guided steps afterwards, before starting optional extensions. Do not hide errors or skip checks to keep to the timing.

Follow the numbered steps. Use the explanation tables and Section 15 when unfamiliar syntax appears. Failure investigation and additional browsers are optional post-lesson work.

***

## 3. Understand the workflow

Playwright performs browser actions. pytest runs test functions. Assertions check results.

```text
Open a page → Perform an action → Check the result
```

### Key terms

| Term | Simple meaning |
| --- | --- |
| Locator | An instruction that finds part of a page. |
| Action | Something the browser does, such as typing or clicking. |
| Assertion | A check of an expected result. |
| Negative test | A test using invalid input or an invalid action. |
| Parametrization | Running one test with different inputs. |
| Virtual environment | A separate set of Python packages for the project. |
| Browser channel | Installed Chrome or Edge selected for a run. |
| Repository | A project whose changes are tracked by Git. |
| Branch | A separate line of work in a repository. |
| Commit | A saved record of selected changes on your computer. |
| Push | Upload commits to GitHub. |
| Pull request, or PR | A request to combine a branch with another branch. |
| Merge | Combine changes from branches. |
| `.gitignore` | A file listing local files and folders to leave out when adding new files to Git. |

Actions:

```python
task_input.fill("Read testing notes")
task_input.press("Enter")
```

Assertion:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

These are explanatory snippets, not complete tests. Complete examples follow.

A script that only clicks and types may finish without checking the intended result. A negative test can pass: submitting an empty task should leave the list empty. The test passes when that expected behaviour occurs.

### Group workflow

```text
Update main → Create a branch → Edit and run
            → Save → Commit → Push → Open a PR → Merge
            → Everyone updates main
```

Saving does not commit. Committing does not upload. Pushing does not merge.

> [!IMPORTANT]
> Commands go in the terminal. Python code goes in the named `.py` file. Save before running. Copy only code inside a code block, not the surrounding backticks.

> [!WARNING]
> Use small, deliberate runs on the named demonstration websites. Do not run load tests, security scans or continuous loops. Do not force-push or use destructive Git commands to bypass a problem.

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
6. Invite members using their GitHub usernames.
7. Members accept the invitations.

### 4.3 Everyone: clone the repository

1. Open Windows File Explorer.
2. Open a folder of your choice where you can save files.
3. Click the address bar and copy its full path.
4. Replace the placeholder below with that path. Keep the quotation marks.

```bat
cd /d "PASTE_YOUR_CHOSEN_FOLDER_PATH_HERE"
```

On GitHub, select Code → HTTPS and copy the repository URL. Replace the placeholder:

```bat
git clone PASTE_THE_COPIED_HTTPS_URL_HERE
```

Git creates a folder inside your chosen folder. Enter it using its actual name, for example:

```bat
cd automated-testing-group-01
```

Use VS Code's File → Open Folder to open the cloned project. Open a new Command Prompt terminal.

```bat
git status
git remote -v
```

You should be on `main`. `origin`, Git's short name for the shared remote location, should point to the group repository.

> [!TIP]
> Members may choose different locations. Run remaining commands inside the cloned project folder, not its parent folder.

***

## 5. Create the shared starting files

> [!IMPORTANT]
> The coordinator completes this section first. Others continue with Section 6 after the setup changes have been merged.

### 5.1 Create a setup branch

```bat
git switch main
git pull --ff-only origin main
git switch -c setup/testing-files
```

`switch -c` creates a branch. `pull --ff-only` updates only when Git can move the branch directly forward.

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

Listed files and folders stay on your computer but are normally left out when adding new files to Git.

| Entry | What stays local |
| --- | --- |
| `.venv/` | Python environment and installed packages. |
| `__pycache__/` | Temporary Python files. |
| `.pytest_cache/` | Temporary pytest information. |
| `reports/` | Generated HTML reports. |
| `recordings/` | Individual recording experiments. |
| `test-results/` | Screenshots, traces and browser output. |
| `.env` | A possible local settings file. This guide does not require one. |

Commit `.gitignore` itself so everyone uses the same rules. Create it before adding environments and outputs.

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

Keep `--browser chromium`. Members select installed Chrome or Edge through their commands.

### 5.5 Commit, push and merge

Save the files:

```bat
git add .gitignore requirements.txt pytest.ini
git diff --staged
git commit -m "Add testing configuration and ignore rules"
git push -u origin setup/testing-files
```

`git add` selects changes. `git diff --staged` displays them. `-u` links your local and remote branches for later `git push` commands.

On GitHub:

1. Open a PR from `setup/testing-files` to `main`.
2. Check base is `main` and compare is `setup/testing-files`.
3. Inspect Files changed.
4. Confirm only intended files appear, then merge.

The base is the destination. The compare branch contains proposed changes.

***

## 6. Prepare your branch and Python environment

### 6.1 Update and create your branch

Everyone runs, using their own number:

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

In VS Code, press Ctrl+Shift+P, find `Python: Select Interpreter` and select the Python inside `.venv`.

### 6.3 Install packages

```bat
python -m pip install -r requirements.txt
python -m pytest --version
python -m playwright --version
```

Wait for installation before running the version commands. No Playwright browser download is needed for installed Chrome or Edge.

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

Git does not store empty folders. Members may need to create them locally.

```bat
git status
git check-ignore .venv/
```

The second command should print `.venv/`. Environment files should not appear as new files to commit.

> [!TIP]
> On another day, reopen this folder, activate `.venv` and set `TEST_BROWSER` again. Continue your existing branch; do not recreate it.

***

## 7. Explore and run your first test

### 7.1 Try the task list manually

Open [Playwright TodoMVC](https://demo.playwright.dev/todomvc/) in your usual browser.

1. Enter `Read testing notes` in `What needs to be done?`.
2. Press Enter and find the task.
3. Select its checkbox.
4. Try All, Active and Completed.

The automated browser uses a separate session. You do not need to clear your usual browser's tasks before testing.

### 7.2 Create your personal test file

Member 1 creates `tests/test_member_1.py`. Use your number.

Paste all of this code and save. Keep the spaces at the start of lines inside the function.

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

The browser opens, adds the task and closes. If checks succeed, the terminal reports `1 passed`.

| Code or option | Meaning |
| --- | --- |
| `def test_add_task(...)` | Defines a test; pytest recognises `test_` function names. |
| `page` | A browser page supplied by the Playwright pytest package. |
| `page: Page` | A type hint that helps the editor understand `page`. |
| `page.goto(URL)` | Opens the website. |
| `get_by_placeholder(...)` | Finds an input using its hint text. |
| `exact=True` | Requires the whole hint text to match. |
| `locator(".todo-list li")` | Finds task rows using a CSS selector. |
| `task_items.locator("label")` | Finds their text labels. |
| `fill(...)` / `press("Enter")` | Enter text / submit it. |
| `to_have_count(...)` | Checks the number of rows. |
| `to_have_text([...])` | Checks expected labels. |
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

Use your filename and branch. It is on your branch, not `main`, until merged.

***

## 8. Check task completion

### 8.1 Append another test

Add below the first test. Keep the existing code.

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

If both succeed, the terminal reports `2 passed`.

`first` selects the first row. `get_by_role("checkbox")` finds its checkbox. `check()` selects it; `to_be_checked()` checks its state.

Each test gets a fresh browser session and creates its own task. Tests do not rely on tasks from another test.

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

The two earlier tests and three input cases produce five runs. If all succeed, the terminal reports `5 passed`.

```bat
git add tests/test_member_1.py
git diff --staged
git commit -m "Add completion and blank input checks"
git push
```

These examples do not cover every possible invalid input.

***

## 10. Record and replay browser actions

You previously entered Python code yourself. Codegen can create starting code by watching your actions in a browser.

### 10.1 Understand recording and replay

```text
Recording: You type and click → Codegen creates code
Replaying: You run the test → Playwright types and clicks
```

Use one scenario:

```text
Open the website → Add “Try the recorder” → Check its text
```

Recording actions is only the start. An assertion checks that the expected task appeared.

### 10.2 Prepare the terminal

Use your cloned project folder and Command Prompt. Activate `.venv` if needed:

```bat
.venv\Scripts\activate.bat
echo %TEST_BROWSER%
```

You should see `msedge` or `chrome`. If needed, set Edge with `set "TEST_BROWSER=msedge"` or Chrome with `set "TEST_BROWSER=chrome"`. Check `recordings` exists.

### 10.3 Start Codegen

```bat
python -m playwright codegen --channel %TEST_BROWSER% --target python-pytest -o recordings/member_1.py https://demo.playwright.dev/todomvc/
```

Use your number.

| Part | Meaning |
| --- | --- |
| `codegen` | Start the recorder. |
| `--channel %TEST_BROWSER%` | Use your selected installed browser. |
| `--target python-pytest` | Create Python code for pytest. |
| `-o recordings/member_1.py` | Save code in this file. |
| Website address | Open this page. |

> [!IMPORTANT]
> Codegen uses `--channel`; pytest uses `--browser-channel`. These option names are different.

### 10.4 Find the windows

| Window | What to do |
| --- | --- |
| Recording browser | Perform your typing and clicks. |
| Playwright Inspector | Watch the generated code. |

Move them so you can see both. Use the browser opened by Codegen, not another browser window.

### 10.5 Record adding one task

1. Confirm the recording browser's task list is empty.
2. Click `What needs to be done?`.
3. Type `Try the recorder`.
4. Press Enter.
5. Confirm the task appears. Do not add more tasks.

Look at Inspector. Code should appear for opening the page, entering text and pressing Enter. An extra recorded click is fine.

### 10.6 Try recording a check

1. Hover over toolbar buttons to read their labels.
2. Find the text assertion control, usually labelled `Assert text`.
3. Select it, then select `Try the recorder` in the page.
4. Confirm the text if prompted.
5. Look for an `expect(...)` line in the code.

> [!TIP]
> If you cannot find the control, continue. You can add the check manually below.

### 10.7 Finish recording

Close the recording browser and Inspector. Wait for the terminal to be ready. Open `recordings/member_1.py` in VS Code, using your number.

### 10.8 Read the actions

They may look like:

```python
page.get_by_placeholder("What needs to be done?").fill(
    "Try the recorder"
)
page.get_by_placeholder("What needs to be done?").press("Enter")
```

`get_by_placeholder(...)` finds the input, `fill(...)` enters text and `press("Enter")` submits it.

Your code may differ because the recorder can find an element in different ways. Start by finding the website address, task text and Enter action.

### 10.9 Make sure there is a check

If no assertion checks the task text, add this after the Enter action inside the test function:

```python
expect(page.locator(".todo-list li label")).to_have_text(
    ["Try the recorder"]
)
```

Match indentation and make sure `expect` is imported at the top. If unsure, compare with this complete example. You can replace your recording file with it if needed:

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

The locator finds task labels. The assertion checks that they match the expected list containing one label. Save the file.

### 10.10 Replay

```bat
python -m pytest recordings/member_1.py --browser-channel %TEST_BROWSER% --headed --slowmo 300
```

Playwright opens the page, enters the task, submits it and checks the text. The browser closes. If this one test succeeds, the terminal reports `1 passed`.

The shared `pytest.ini` already selects `chromium`. To choose installed Chrome, use `--browser-channel chrome`, not `--browser chrome`.

### 10.11 Understand the result

```text
Actions → Do something
Assertions → Check what happened
```

A successful run with only actions does not explicitly check task text. With the assertion, a successful run confirms the text matched.

Keep experiments in `recordings/`, which stays local through `.gitignore`. This recording is separate from the guided cases in your personal file under `tests/`.

If replay fails, check input and expected text, ensure only one task was added, and read the error. The optional failure activity in Section 14.1 provides more practice.

***

## 11. Try a simple login

TodoMVC has no login activity. For these two tests, use [The Internet login demonstration](https://the-internet.herokuapp.com/login).

### 11.1 Understand the two cases

| Case | Input | Expected result |
| --- | --- | --- |
| Correct details | Published practice username and password. | Secure Area heading appears. |
| Incorrect password | Practice username with a deliberately wrong password. | Password error appears; Login button remains visible. |

The page publishes these practice details:

| Field | Value |
| --- | --- |
| Username | `tomsmith` |
| Password | `SuperSecretPassword!` |

> [!IMPORTANT]
> These are public demonstration details, not personal credentials. Do not use your own passwords or run these tests against other login websites. Copy the capital letters and final exclamation mark carefully.

### 11.2 Try the correct login manually

1. Open the demonstration login page in Chrome or Edge.
2. Enter `tomsmith` in Username.
3. Enter `SuperSecretPassword!` in Password.
4. Click Login.
5. Find the Secure Area heading.

Your automated test will repeat these actions in its own session.

### 11.3 Append the correct-login test

Add below the existing tests in your personal file. Keep the imports, task-list URL and earlier tests.

```python
def test_login_with_correct_details(page: Page):
    page.goto("https://the-internet.herokuapp.com/login")

    page.get_by_label("Username").fill("tomsmith")
    page.get_by_label("Password").fill(
        "SuperSecretPassword!"
    )

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
| `.click()` | Click it. |
| `get_by_role("heading", name="Secure Area", exact=True)` | Find that exact heading. |
| `.to_be_visible()` | Check it appears. |

The actions enter details and click Login. The assertion checks the expected page heading.

### 11.4 Run only this test

```bat
python -m pytest tests/test_member_1.py::test_login_with_correct_details --browser-channel %TEST_BROWSER% --headed --slowmo 300
```

Use your number. The part after `::` selects one test function. If it succeeds, the summary reports `1 passed`.

### 11.5 Append the incorrect-password test

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

This enters a wrong password and checks for the error and the Login button.

> [!NOTE]
> The login attempt should be rejected. The test passes when that rejection happens as expected. An unsuccessful login can therefore be a successful test.

### 11.6 Run all your cases

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed
```

| Guided case | Runs |
| --- | ---: |
| Add a task | 1 |
| Complete a task | 1 |
| Reject blank task inputs | 3 |
| Login with correct details | 1 |
| Login with incorrect password | 1 |
| Total | 7 |

If all succeed, the terminal reports `7 passed`. Read the actual result. Optional additions change the total.

Each login test opens its own page and enters its own details. It does not rely on the other login test.

### 11.7 Commit and push

```bat
git add tests/test_member_1.py
git diff --staged
git commit -m "Add correct and incorrect password login tests"
git push
```

If a login test fails, check the page loads manually, compare the credentials, and read the assertion error. Do not use personal accounts as a substitute.

***

## 12. Create a results report

Check `reports` exists:

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --html=reports/member-1.html --self-contained-html
```

The browser runs without a visible window because `--headed` is omitted.

In Windows File Explorer, open the project folder, then `reports`, then `member-1.html`.

Find test names, results and durations. Expand errors if present. The report remains local through `.gitignore`.

***

## 13. Combine the group files

### 13.1 Check and push

```bat
git status
git push
```

If source changes remain, run your file, add that file, inspect `git diff --staged`, commit and push. Do not add environments, reports, recordings or traces.

### 13.2 Merge one PR at a time

On GitHub:

1. Open a PR from `testing/member-1` to `main`, using your number.
2. Use a title such as `Add Member 1 browser tests`.
3. Ask another member to look through Files changed with you.
4. Check changes belong to your file, assertions are meaningful and no private data or local outputs appear.
5. Merge one member's PR at a time.

Do not edit another member's file in this activity. Separate filenames allow files to sit beside one another without replacing work.

### 13.3 Everyone: update local main

Start with a clean working directory. Commit intended source changes on your branch before switching.

```bat
git switch main
git pull --ff-only origin main
git status
```

You should see the merged files. A GitHub merge does not update your computer automatically.

### 13.4 Run the group project once

Choose one member to run:

```bat
python -m pytest --browser-channel %TEST_BROWSER% --html=reports/group-results.html --self-contained-html
```

With only guided cases, there are seven runs per member file. Optional additions increase this. Repeated guided cases do not represent additional unique functional coverage.

If the run needs more time, preserve the result and investigate afterwards. Avoid repeated full-group runs without a reason.

### End of the main lesson

Every member should have their own guided source file and have run it on their own computer. Keep source in the shared repository and generated outputs locally. Continue any unfinished guided steps before optional extensions.

***

## 14. Optional post-lesson practice

Choose activities that help you revisit an unfamiliar step or explore further. Times are planning guides, not limits.

| Activity | Suggested time | Focus |
| --- | --- | --- |
| 14.1 Investigate a deliberate failure | 15–20 minutes | Errors, screenshots and traces. |
| 14.2 Inspect page elements | 5–10 minutes | Match locators to the page. |
| 14.3 Try another browser | 10–15 minutes plus downloads | Reuse tests. |
| 14.4 Expand inputs | 10–15 minutes | Parametrization. |
| 14.5 Add a reusable helper | 15–20 minutes | Reduce repeated actions. |
| 14.6 Improve a recording | 15–20 minutes | Create a useful shared test. |
| 14.7 Inspect Git history | 5–10 minutes | Find saved changes. |

Before changing shared source again, update clean local `main` and create a new branch:

```bat
git switch main
git pull --ff-only origin main
git switch -c practice/member-1-follow-up
```

Use your number. On a later session, continue that branch rather than recreating it. Run your personal file after changes, then commit, push and combine through a PR.

### 14.1 Investigate a deliberate failure

A failed test does not automatically mean the website is broken. Here, the expected task text is deliberately wrong.

In `test_add_task()`, temporarily replace:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

with:

```python
expect(task_labels).to_have_text(["A different task"])
```

Do not change the entered text.

```bat
python -m pytest tests/test_member_1.py::test_add_task --browser-channel %TEST_BROWSER% --headed --screenshot only-on-failure --tracing retain-on-failure --output test-results/member-1-failure
```

| Option | Purpose |
| --- | --- |
| `::test_add_task` | Select only this function. |
| `--screenshot only-on-failure` | Save a screenshot if it fails. |
| `--tracing retain-on-failure` | Keep the failed run's trace. |
| `--output ...` | Choose the output folder. |

Find expected and actual text in the error. Open `test-results/member-1-failure`, its generated test subfolder and the screenshot.

Find `trace.zip`, right-click it and select Copy Relative Path. Replace this placeholder, keeping the quotes:

```bat
python -m playwright show-trace "PASTE_RELATIVE_PATH_HERE" --browser-channel %TEST_BROWSER%
```

Select actions in order to examine page loading, input, Enter and the failed check.

Restore the original assertion, save and rerun:

```bat
python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER%
git diff
```

With only guided cases, a successful run reports `7 passed`. If restored exactly, Git may show no change and no extra commit is needed.

> [!IMPORTANT]
> Do not commit the deliberate mistake or delete the assertion to hide failure. Restore the meaningful check. Later runs may replace generated output; copy it locally first only if you want to keep it.

### 14.2 Inspect page elements

On the task-list page, right-click the input and select Inspect. Find `placeholder="What needs to be done?"` and compare it with `get_by_placeholder(...)`.

On the login page, look at the visible Username and Password labels. Compare them with the `get_by_label(...)` lines. An attribute is extra information attached to a page element; labels and attributes help identify controls.

### 14.3 Try another browser

To use the other installed main browser, change `TEST_BROWSER` and rerun your personal file. Python source and shared configuration stay unchanged.

For Playwright-managed browsers, these commands override shared `addopts` for that run. Do not add a Chrome or Edge channel to Firefox or WebKit.

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

Ordinary Firefox does not replace Playwright Firefox. Playwright WebKit is not installed Safari. Skip unsupported or blocked options. Compare functional outcomes, not browser speed; these are not performance benchmarks.

After upgrading Playwright, reinstall managed browsers you use. This does not mean reinstalling ordinary Chrome or Edge.

### 14.4 Expand input examples

Replace the parametrization block above the blank-input function with:

```python
@pytest.mark.parametrize(
    "task_text",
    ["", " ", "   ", "    "],
    ids=["empty", "one-space", "three-spaces", "four-spaces"],
)
```

Keep the function unchanged. There is one ID per input. If this is your only addition, your file now runs eight cases.

You can also change a valid task name in both its input action and assertion. Changing only one may cause a mismatch.

### 14.5 Add a reusable helper

A helper performs reusable steps. Append both functions below to your personal file, keeping imports and URL:

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

Run your file. This adds one test. The helper performs actions; the test contains the checks.

### 14.6 Improve a recording

1. Try editing or deleting a task manually.
2. Record it using Section 10.
3. Read the generated code and remove unnecessary actions.
4. Add a useful assertion for task text or count.
5. Add the working test to your personal file under `tests/` to share it.
6. Give its function a name different from existing tests.
7. Run, commit and push, then combine through a PR.

Keep experiments in ignored `recordings/`. If expected behaviour is unclear, treat it as an observation rather than a confirmed defect.

### 14.7 Inspect Git history

```bat
git log --oneline --graph --decorate --all -15
```

Use an actual commit ID:

```bat
git show COMMIT_ID
```

This displays what changed. Press `q` if Git opens a scrolling view.

***

## 15. Simple syntax reference

Use this as a reference while working. You do not need to memorise it. These are small examples, not a separate complete program.

### 15.1 Start a test and open a page

| Syntax | Meaning |
| --- | --- |
| `from playwright.sync_api import Page, expect` | Import the page type and checking tool. |
| `def test_example(page: Page):` | Define a test using a browser page. |
| `page.goto("https://example.com")` | Open a website address. Use the practice websites in your actual tests. |

### 15.2 Find something on the page

| Syntax | Meaning |
| --- | --- |
| `page.get_by_label("Username")` | Find a field using its label. |
| `page.get_by_placeholder("What needs to be done?")` | Find an input using hint text. |
| `page.get_by_role("button", name="Login")` | Find a button by name. |
| `page.get_by_role("link", name="Completed")` | Find a link by name. |
| `page.get_by_role("heading", name="Secure Area")` | Find a heading by name. |
| `page.get_by_text("Your password is invalid!")` | Find an element with this text. |
| `page.locator(".todo-list li")` | Find task rows using the supplied CSS selector. |

### 15.3 Perform an action

| Syntax | Meaning |
| --- | --- |
| `field.fill("Some text")` | Replace a field's contents with this text. |
| `field.press("Enter")` | Press Enter in the field. |
| `button.click()` | Click the selected button. |
| `checkbox.check()` | Select a checkbox. |

`field`, `button` and `checkbox` are example variable names. First assign them a locator. For example:

```python
username_field = page.get_by_label("Username")
username_field.fill("tomsmith")
```

The same action on one line:

```python
page.get_by_label("Username").fill("tomsmith")
```

### 15.4 Check a result

| Syntax | Meaning |
| --- | --- |
| `expect(item).to_be_visible()` | Check the item is visible. |
| `expect(checkbox).to_be_checked()` | Check a checkbox is selected. |
| `expect(items).to_have_count(1)` | Check exactly one item matches. |
| `expect(labels).to_have_text(["Read testing notes"])` | Check labels match the expected list. |
| `expect(field).to_have_value("")` | Check an input is empty. |

Read assertions as: “Expect this item to have this result.” The variable names must refer to locators defined in your test.

### 15.5 Recognise common Python symbols

| Syntax | Meaning here |
| --- | --- |
| `"text"` | A string: a text value. |
| `""` | An empty string. |
| `["A", "B"]` | A list containing two values. |
| `name = value` | Store a value under a variable name. |
| `object.method(...)` | Call an operation on an object. |
| `:` after `def ...` | Starts a function's indented body. |
| Four spaces inside a function | Keep instructions inside that function. |

***

## 16. Troubleshooting and command reference

### Before attempting a fix

Save the file, read the error and check folder, Python, branch and browser:

```bat
python -c "from pathlib import Path; import sys; print('Folder:', Path.cwd()); print('Python:', sys.executable)"
git status
echo %TEST_BROWSER%
```

Use the cloned project folder and its `.venv` Python.

### Common problems

| Problem | What to try |
| --- | --- |
| Python not recognised | Reopen VS Code. Try `py -3 --version`. Review installation if neither works. |
| Packages cannot be imported | Activate `.venv`, check Python and repeat `python -m pip install -r requirements.txt`. |
| Activation fails | Use Command Prompt and `.venv\Scripts\activate.bat`. Alternatively replace `python` with `.venv\Scripts\python.exe` in commands. |
| Browser variable is empty or prints `%TEST_BROWSER%` | Set it again in this terminal. |
| Chrome or Edge cannot be found | Check it opens from Start. Use the other approved installed browser if needed. |
| `invalid choice: 'chrome'` | Use `--browser chromium` in `pytest.ini` and `--browser-channel chrome` in pytest commands. |
| Playwright Chromium executable missing | Main tests need `--browser-channel %TEST_BROWSER%`; Codegen needs `--channel %TEST_BROWSER%`. |
| No tests found | Save. Check `.py` extension, `test_` filename and `test_` function names. |
| File not found | Check spelling, member number and project folder. |
| `IndentationError` | Match spaces. Use four spaces inside a function. |
| `SyntaxError` | Check quotes, brackets and colons. Do not paste Markdown backticks into code. |
| Browser not visible | Add `--headed`. |
| Browser closes quickly | Normal after running. Use `--headed --slowmo 300` and read results. |
| Expected text differs | Compare spelling, capital letters and spaces. |
| Login test fails | Check demonstration page availability, username and password. Do not use personal accounts. |
| Website cannot load | Try manually. Check connection. Save and retry later if unavailable. |
| Locator times out | Check page loaded and locator matches. Use Inspect or Codegen. |
| Report has no screenshot | Open screenshots separately under `test-results`. |
| Generated output disappears | Later runs may replace it. Copy locally first if needed. |
| Browser/download blocked | Use approved processes. Do not disable security controls. |
| Repository not found | Check URL, sign-in and accepted invitation. |
| Push rejected | Check authentication, access, branch and remote. Do not force-push. |
| Nothing to commit | Files may be unchanged, already committed, unsaved or ignored. Use `git status` and `git diff`. |
| Local main lacks merged files | Pull from clean local main. |
| Git warns about overwriting changes | Inspect `git status`. Commit intended source on your branch before switching. |
| Many generated files appear in Git | Check `.gitignore` in the project root. See below. |

### If `.gitignore` does not appear to work

```bat
git check-ignore -v .venv/
```

If no rule appears, check `.gitignore` name, location and contents.

To unselect a folder added but not committed, keeping its files:

```bat
git restore --staged .venv/
```

For a non-sensitive local-only folder already committed, stop tracking it while keeping the local copy:

```bat
git rm -r --cached .venv/
git status
git diff --staged
```

Use the actual unwanted path, not a source folder. Review, then commit on your branch:

```bat
git add .gitignore
git commit -m "Stop tracking local Python environment"
git push
```

Combine through a PR. This does not remove earlier history.

> [!WARNING]
> If private information or credentials were committed, ignoring or later deleting them is not a complete fix. Stop sharing affected content and follow the relevant account or organisation process to revoke credentials and handle disclosure. The published demo login details in Section 11 are not personal credentials.

### If a merge conflict appears

Do not delete the repository or run destructive resets. Use `git status` first.

If a local merge is in progress, compare conflicting files in VS Code with their owner. Keep intended content, remove conflict markers such as `<<<<<<<`, `=======` and `>>>>>>>`, save and test before completing the merge.

To return to the state before a local merge, use `git merge --abort` only when `git status` confirms a merge is in progress.

If `git pull --ff-only` refuses because histories diverged, no merge started. Preserve commits and inspect:

```bat
git fetch origin
git log --oneline --graph --decorate --all -15
```

### Main command reference

Use your number.

| Goal | Command |
| --- | --- |
| Choose Edge | `set "TEST_BROWSER=msedge"` |
| Choose Chrome | `set "TEST_BROWSER=chrome"` |
| Watch your tests | `python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER% --headed --slowmo 300` |
| Run without visible browser | `python -m pytest tests/test_member_1.py --browser-channel %TEST_BROWSER%` |
| Run one login test | `python -m pytest tests/test_member_1.py::test_login_with_correct_details --browser-channel %TEST_BROWSER% --headed` |
| Inspect changes | `git diff` |
| Select source | `git add tests/test_member_1.py` |
| Inspect selected changes | `git diff --staged` |
| Check ignore rule | `git check-ignore -v .venv/` |
| Save changes | `git commit -m "Describe the change"` |
| Upload commits | `git push` |

***

## Closing reminder

A passing test means its particular checks succeeded in that run. It does not prove the whole website is error-free.

Keep examples small and understandable. Use failures to understand what happened. Share working source without private data or local browser outputs.

```text
Choose a behaviour → Define the expectation → Automate → Run
                   → Investigate → Improve → Commit → Push → Merge
```
