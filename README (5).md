# Automated Testing Tools Team Practical

> A guided, hands-on introduction to browser automation and testing tools for students with no prior automated testing experience.

> [!NOTE]
> ## Educational Practice Repository
>
> This public repository has been created solely for an introductory automated testing tools practical. Its purpose is to help students explore browser inspection, recording, replay, assertions, data-driven testing, browser comparisons, reports and diagnostic evidence.
>
> All task names, examples, scenarios and other student-created content are fictional and prepared for educational purposes only. Any resemblance to actual persons, organisations, events or circumstances is purely coincidental.
>
> Do not include confidential, personal, sensitive, commercially sensitive or copyrighted material in this repository. This includes passwords, access tokens, API keys, identification numbers, personal contact details and private photographs.

This in-class practical helps you learn automated testing tools by using them. You will work in a small group to test a live demonstration task-list website.

The focus is on understanding what the tools offer: recording interactions, replaying actions, checking results, varying inputs, comparing browsers, reading reports and investigating failures.

No previous automated testing experience is required. The guided activities use Python, which you already know. You do not need to learn JavaScript, build a website or create an application server.

All tests are started manually on your computer. Git and GitHub are used to record and share your work.

### Tools used in this practical

| Tool | What you will use it for |
| --- | --- |
| Python | Write and execute test code. |
| Visual Studio Code | Edit scripts and practical records. |
| Microsoft Python extension for VS Code | Select the Python environment and support Python editing. |
| Browser Developer Tools | Examine page elements and their attributes. |
| Playwright | Control browsers and check website behaviour. |
| Playwright Codegen | Record interactions and generate Python test code. |
| pytest | Discover and execute tests. |
| pytest-html | Generate a readable HTML report. |
| Playwright Trace Viewer | Inspect actions, page snapshots and errors. |
| Git and GitHub | Preserve and combine contributions. |

Codegen and Trace Viewer are included with Playwright. Developer Tools is included with desktop browsers such as Chrome and Edge.

### Browser options included

| Browser option | Installation method | Test selection |
| --- | --- | --- |
| Chromium | Install through Playwright. | `--browser chromium` |
| Firefox | Install Playwright's Firefox build. | `--browser firefox` |
| WebKit | Install Playwright's WebKit build. | `--browser webkit` |
| Google Chrome | Use installed stable Google Chrome. | `--browser chromium --browser-channel chrome` |
| Microsoft Edge | Use installed stable Microsoft Edge. | `--browser chromium --browser-channel msedge` |

> [!IMPORTANT]
> Playwright's Firefox is a specially supported build. Installing ordinary Firefox alone does not replace it.
>
> Playwright WebKit is not the installed Safari application. Do not report a WebKit run as a test performed in Safari.

| Item | Details |
| --- | --- |
| Group size | 4–5 students |
| Guided in-class duration | Approximately 2.5 hours |
| Required knowledge | Python, basic terminal use and the earlier Git practical |
| Test website | [Playwright TodoMVC demonstration](https://demo.playwright.dev/todomvc/) |
| Practical outcome | Test scripts, execution records, browser comparisons, selected evidence, reflections and Git history |
| Focus | Exploring automated testing tools, not developing an application |

## Contents

1. [Learning outcomes](#1-learning-outcomes)
2. [Understand the workflow](#2-understand-the-workflow)
3. [Prepare your group and computers](#3-prepare-your-group-and-computers)
4. [Create and clone the repository](#4-create-and-clone-the-repository)
5. [Create the starting files](#5-create-the-starting-files)
6. [Prepare your individual environment](#6-prepare-your-individual-environment)
7. [Explore, record and replay](#7-explore-record-and-replay)
8. [Create automated checks](#8-create-automated-checks)
9. [Run data-driven tests and compare browsers](#9-run-data-driven-tests-and-compare-browsers)
10. [Investigate a failed test](#10-investigate-a-failed-test)
11. [Create your own tests](#11-create-your-own-tests)
12. [Combine contributions and reflect](#12-combine-contributions-and-reflect)
13. [Troubleshooting and command reference](#13-troubleshooting-and-command-reference)
14. [Individual completion checklist](#14-individual-completion-checklist)
15. [Optional extension activities — outside the in-class practical](#15-optional-extension-activities--outside-the-in-class-practical)

***

## 1. Learning outcomes

By the end of this practical, you should be able to:

- Explain the role of each selected tool.
- Inspect a page element using browser Developer Tools.
- Record and replay browser interactions.
- Distinguish an action from an assertion.
- Execute positive and negative tests.
- Run the same test with different data.
- Select different browsers without rewriting a test.
- Launch Chrome and Edge explicitly from Python.
- Generate an HTML report.
- Investigate a failure using a screenshot and trace.
- Create additional tests of your own.
- Explain your contributions using Git history.

### Working through this practical

1. Complete the activities in sequence.
2. Enter commands in the terminal, not in your documents.
3. Enter Python code in the indicated `.py` files.
4. Replace member numbers, addresses and filenames with your own.
5. Read explanations before running commands.
6. Wait for all members at group checkpoints.
7. Record actual results only after execution.

Use Git Bash on Windows, or Terminal on macOS or Linux. Alternative Windows activation commands are also provided.

> [!IMPORTANT]
> Run commands from inside your cloned repository unless instructed otherwise. Check your branch and working directory before making changes. Activate the Python environment before running testing commands.

### Suggested timing

Install base software and browser binaries before class where possible.

| Activity | Time |
| --- | ---: |
| Group setup, starting files and environment checks | 25 minutes |
| Explore the website | 10 minutes |
| Record and replay | 20 minutes |
| Create automated checks | 25 minutes |
| Data-driven tests and allocated browser comparisons | 20 minutes |
| Failure investigation | 20 minutes |
| Self-designed tests | 20 minutes |
| Integration and reflection | 10 minutes |
| Total | 150 minutes |

The Chrome and Edge standalone examples are additional demonstrations. Divide them between members or complete the remaining examples outside class if needed.

### Related lesson materials

- `03-3-Testing-Tools-1.pptx`
- `OAL-03-2-Manual-vs-Automated-1.pptx`

***

## 2. Understand the workflow

### A simple mental model

The website is the application you want to check.

Playwright follows your browser instructions. pytest finds and executes your tests. Assertions compare observed behaviour with your expectations.

### Key terms

| Term | Meaning |
| --- | --- |
| Test case | A scenario with steps and an expected result. |
| Locator | An instruction identifying an element on a page. |
| Action | An operation such as typing, clicking or pressing a key. |
| Assertion | A check comparing behaviour with an expectation. |
| Positive test | A test using valid inputs or an expected action. |
| Negative test | A test checking invalid inputs or actions. |
| Parameterized test | One definition executed with several input values. |
| Fixture | A reusable setup resource, such as Playwright's `page`. |
| Browser channel | A selection such as installed Google Chrome or Microsoft Edge. |
| Headed execution | Running with the browser window visible. |
| Headless execution | Running without displaying a browser window. |
| Report | A summary of execution and outcomes. |
| Trace | A record of actions and diagnostic information. |
| Virtual environment | A project-specific Python environment. |
| Personal work branch | Your own Git branch for developing a contribution. |
| Pull request, or PR | A request to combine your branch with shared `main`. |

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

A script that clicks and types has not necessarily checked the result.

### Positive and negative do not mean pass and fail

| Scenario | Expected behaviour | Passing outcome |
| --- | --- | --- |
| Add a normal task. | A task appears with the entered text. | The task appears correctly. |
| Submit an empty task. | No task is added. | The task list remains unchanged. |

A negative test passes when invalid input is handled as expected.

### One test, different browsers

```text
Same test instructions
        ↓
Chromium / Firefox / WebKit / Chrome / Edge
        ↓
Compare observed outcomes
```

For the guided pytest tests, select browsers through command-line arguments. Do not create five copies of the same test merely to change the browser.

### Saving, committing and sharing

```text
Save   → Write changes to a file.
Commit → Record selected changes locally.
Push   → Send local commits to GitHub.
PR     → Propose combining your branch with main.
```

Saving does not commit. Committing does not upload. Pushing a branch does not merge it into `main`.

### Group working rules

- Use your own branch, test file, results file and evidence folder.
- Every member completes the guided exercises.
- Keep commits focused and messages meaningful.
- Keep these instructions in `README.md`.
- Do not claim another member's execution as your own.
- Do not change expectations merely to obtain a pass.
- Use fictional data and small, deliberate test runs.

A formal findings report, assigned review rotation and peer-reproduction exercise are not required.

> [!WARNING]
> Do not perform load testing, security scanning or high-frequency repeated runs against the public website. Do not force-push, use `git reset --hard` or delete the repository to bypass a problem. Preserve your work and ask your Tutor if needed.

***

## 3. Prepare your group and computers

### 3.1 Assign responsibilities

| Member | Initial coordination responsibility | Individual test file |
| --- | --- | --- |
| 1 | Timing and activity progress | `tests/test_member_1.py` |
| 2 | Environment setup notes | `tests/test_member_2.py` |
| 3 | Open-ended task allocation | `tests/test_member_3.py` |
| 4 | Evidence organisation | `tests/test_member_4.py` |
| 5, if any | Repository integration and summary | `tests/test_member_5.py` |

For four members, Members 1 and 4 share integration and summary coordination.

These responsibilities do not replace individual testing. Each member uses their own computer and GitHub account.

### 3.2 Install or verify Python

Use Python 3.12 or 3.13.

#### Windows

1. Open [Python Downloads](https://www.python.org/downloads/).
2. Download a stable installer appropriate for your computer.
3. Run it.
4. If `Add Python to PATH` is shown, select it.
5. Complete installation and reopen your terminal.
6. Check:

```powershell
python --version
```

If unavailable:

```powershell
py -3 --version
```

If the launcher works, use `py -3` to create the virtual environment later.

#### macOS

Check:

```bash
python3 --version
```

If necessary, install a stable version from [Python Downloads for macOS](https://www.python.org/downloads/macos/), reopen Terminal and check again.

#### Linux

```bash
python3 --version
python3 -m pip --version
```

Ask your Tutor or system administrator to install missing Python, pip or virtual-environment support. Do not alter system-managed Python or bypass restrictions.

### 3.3 Install or verify Git

```bash
git --version
```

If unavailable, install the appropriate version from [Git Downloads](https://git-scm.com/downloads), reopen your terminal and check again.

Set your identity if needed:

```bash
git config --global user.name "Your Name"
git config --global user.email "YOUR_COMMIT_EMAIL"
```

Use an email associated with GitHub or your GitHub-provided no-reply email. These settings identify commits; they do not sign you in. Complete authentication before continuing.

### 3.4 Install Visual Studio Code and its Python extension

1. Install [Visual Studio Code](https://code.visualstudio.com/) for your operating system.
2. Open VS Code.
3. Open Extensions.
4. Search for `Python`.
5. Install the extension published by Microsoft.

The extension does not install Python itself. Another Python editor may be used with your Tutor's approval.

### 3.5 Install or verify Google Chrome

If already installed, do not reinstall it.

Otherwise:

1. Open [Google Chrome](https://www.google.com/chrome/).
2. Download stable Chrome for your operating system.
3. Complete installation.
4. Open it once to finish any first-run setup.
5. Close it before the automation activity.

Do not connect a personal profile for this practical.

### 3.6 Install or verify Microsoft Edge

If already installed, do not reinstall it.

Otherwise:

1. Open [Microsoft Edge](https://www.microsoft.com/edge/download).
2. Download stable Edge for your operating system.
3. Complete installation.
4. Open it once to finish any first-run setup.
5. Close it before the automation activity.

> [!IMPORTANT]
> Use approved installation methods on managed computers. Browser policies may prevent automation. Record the restriction and consult your Tutor; do not bypass it.

### Checkpoint

- [ ] Everyone has Python, Git, an editor and a GitHub account.
- [ ] GitHub authentication is ready.
- [ ] Chrome and Edge availability has been checked.
- [ ] Everyone knows their member number and responsibility.
- [ ] Everyone understands the data-handling rules.

***

## 4. Create and clone the repository

### 4.1 Coordinator only: create the shared repository

On GitHub:

1. Create `automated-testing-tools-team-XX`, replacing `XX` with your group identifier.
2. Set visibility to Public.
3. Add a README and confirm the default branch is `main`.
4. Place these instructions in `README.md`, including the disclaimer.
5. Invite all group members.
6. Invite your Tutor using the username provided.
7. Confirm invitations are accepted.

> [!NOTE]
> If your Tutor provides a repository, use it instead. Follow institutional visibility requirements if they differ. Public repositories may be viewed by anyone; include fictional, non-sensitive content only.

### 4.2 Everyone: clone the repository

On GitHub, open the repository, select Code → HTTPS and copy the URL.

Type `git clone`, add one space and paste that URL:

```bash
git clone PASTE_THE_HTTPS_URL_COPIED_FROM_GITHUB_HERE
```

Do not type the placeholder literally or use Markdown link syntax in the command.

Enter the folder created, using its actual name:

```bash
cd automated-testing-tools-team-XX
```

Open it in VS Code through `File → Open Folder`.

### 4.3 Inspect your local repository

```bash
git status
git branch
git remote -v
git log --oneline -5
```

| Command | What to check |
| --- | --- |
| `git status` | Current branch and uncommitted changes. |
| `git branch` | The `*` identifies the current branch. |
| `git remote -v` | `origin` points to the group repository. |
| `git log --oneline -5` | Up to five recent commits. |

Press `q` if a scrolling view opens.

### Checkpoint

- [ ] Members and the Tutor have access.
- [ ] The disclaimer appears in `README.md`.
- [ ] I am inside the cloned repository on `main`.
- [ ] My working directory is clean.
- [ ] `origin` points to the correct repository.

***

## 5. Create the starting files

> [!IMPORTANT]
> The coordinator completes this section first. Others wait until the setup PR has merged.

### 5.1 Create a setup branch

```bash
git switch main
git pull --ff-only origin main
git switch -c setup/testing-files
```

The first command selects local `main`. The second updates it only if Git can move it directly forward. The third creates and selects the setup branch.

### 5.2 Prepare the structure

```text
README.md
.gitignore
requirements.txt
pytest.ini
tests/
examples/
docs/
├── team-plan.md
├── summary.md
├── results/
│   ├── member-1.md
│   ├── member-2.md
│   ├── member-3.md
│   ├── member-4.md
│   └── member-5.md
├── reflections/
│   ├── member-1.md
│   ├── member-2.md
│   ├── member-3.md
│   ├── member-4.md
│   └── member-5.md
└── evidence/
```

Omit Member 5's files for four members. Initial documents may contain a heading only. Git does not track empty folders.

The `tests/` folder holds pytest tests. The `examples/` folder holds standalone browser-launch demonstrations.

### 5.3 Create `.gitignore`

```gitignore
.venv/
__pycache__/
.pytest_cache/
test-results/
reports/
recordings/
.env
```

Selected evidence will be copied into `docs/evidence/` before committing.

### 5.4 Create `requirements.txt`

```text
pytest-playwright
pytest-html
```

### 5.5 Create `pytest.ini`

```ini
[pytest]
testpaths = tests
addopts = -v
```

Keep browser selection in commands so each run is explicit.

### 5.6 Create `docs/team-plan.md`

```markdown
# Team plan

## Group identifier

## Members

| Member | Non-sensitive identifier | GitHub username | Responsibility |
| --- | --- | --- | --- |
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |

## Environment setup notes

## Browser availability

## Browser comparison allocation

## Open-ended testing allocation

## Repository integration arrangements
```

Add Member 5 if needed.

### 5.7 Stage, commit and push

```bash
git status
git add .gitignore requirements.txt pytest.ini docs/
git diff --staged
git commit -m "Add testing configuration and group records"
git push -u origin setup/testing-files
```

### 5.8 Create and merge the setup PR

1. Create a PR on GitHub.
2. Set base to `main`.
3. Set compare to `setup/testing-files`.
4. Inspect Files changed and confirm the intended files.
5. Merge the setup PR.

Base is the destination; compare contains the proposal. A formal review exercise is not required.

### 5.9 Everyone: update local `main`

```bash
git switch main
git pull --ff-only origin main
git status
```

Merging on GitHub does not update anyone's computer automatically.

### Checkpoint

- [ ] The setup PR is merged.
- [ ] Everyone has updated local `main`.
- [ ] Everyone can open the starting configuration and records.
- [ ] Everyone's working directory is clean.

***

## 6. Prepare your individual environment

### 6.1 Create your personal branch

Use your member number:

```bash
git switch -c testing/member-1
git branch --show-current
git status
```

### 6.2 Create a virtual environment

Windows:

```powershell
python -m venv .venv
```

If only the launcher works:

```powershell
py -3 -m venv .venv
```

macOS/Linux:

```bash
python3 -m venv .venv
```

### 6.3 Activate the environment

Run only the command for your terminal.

Git Bash on Windows:

```bash
source .venv/Scripts/activate
```

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Windows Command Prompt:

```bat
.venv\Scripts\activate.bat
```

macOS/Linux:

```bash
source .venv/bin/activate
```

Verify:

```bash
python -c "import sys; print(sys.executable)"
```

The path should point inside this repository's `.venv`.

> [!TIP]
> If activation is blocked, use an approved alternative terminal or ask your Tutor. You can invoke the interpreter directly: `.\.venv\Scripts\python.exe` on Windows or `./.venv/bin/python` on macOS/Linux. Replace `python` in later commands with that path.

### 6.4 Select the VS Code interpreter

1. Open the Command Palette: `Ctrl+Shift+P` on Windows/Linux or `Cmd+Shift+P` on macOS.
2. Search for `Python: Select Interpreter`.
3. Select the interpreter inside `.venv`.

### 6.5 Install testing packages

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### 6.6 Install Chromium, Firefox and WebKit

```bash
python -m playwright install chromium firefox webkit
```

Or install separately:

```bash
python -m playwright install chromium
python -m playwright install firefox
python -m playwright install webkit
```

These commands install Playwright-managed builds. They do not install Chrome or Edge.

> [!NOTE]
> Browser downloads require time and disk space. If operating-system support or required system libraries are missing, record the limitation and consult your Tutor. Do not install system packages without authorisation.

### 6.7 Verify the tools

```bash
python --version
python -m pytest --version
python -m playwright --version
python -m pip show pytest-html
```

### 6.8 Create local output folders

Using your editor, create:

```text
recordings/
reports/
```

These are ignored by Git.

### 6.9 Prepare your results document

In `docs/results/member-1.md`:

```markdown
# Automated tools results — Member 1

## Environment

- Date and time:
- Operating system:
- Python version:
- Playwright version:
- pytest version:

## Browser availability

| Browser | Available? | Installation or restriction notes |
| --- | --- | --- |
| Chromium | | |
| Playwright Firefox | | |
| Playwright WebKit | | |
| Google Chrome | | |
| Microsoft Edge | | |

## Website exploration

## Recording and replay

## Positive tests

## Data-driven negative tests

## Browser comparison

## Chrome and Edge examples

## Failure investigation

## Self-designed tests
```

### 6.10 Commit and push

```bash
git add docs/results/member-1.md
git diff --staged
git commit -m "Record testing environment and browser availability"
git push -u origin testing/member-1
```

### Checkpoint

- [ ] Everyone is on their own branch.
- [ ] Everyone's interpreter points to `.venv`.
- [ ] Packages and managed browser installations have been checked.
- [ ] Chrome and Edge availability is recorded.
- [ ] Restrictions are documented honestly.
- [ ] Everyone pushed an environment record.

***

## 7. Explore, record and replay

### 7.1 Open the live website

Open [Playwright TodoMVC](https://demo.playwright.dev/todomvc/).

1. Find the input with the placeholder `What needs to be done?`.
2. Enter `Read testing notes`.
3. Press Enter.
4. Confirm that a task appears.
5. Select its checkbox.
6. Observe its completed appearance.
7. Explore All, Active and Completed filters.

### 7.2 Inspect the input

In Chrome or Edge:

1. Right-click the input and select Inspect.
2. Find the selected input element.
3. Locate its `placeholder` attribute.
4. Record its value.

Also record one usability observation, such as whether completing a task is obvious.

### 7.3 Start Codegen

Use Chromium for recording:

```bash
python -m playwright codegen --target python-pytest -o recordings/member_1.py https://demo.playwright.dev/todomvc/
```

Use your own number. You only need to record once; the test can later run in other browsers.

### 7.4 Record a scenario

1. Confirm that the recording browser's task list is empty.
2. Enter `Prepare a testing checklist`.
3. Press Enter.
4. Use the text-assertion control to check the new task label.
5. Stop recording.
6. Inspect the generated code.
7. Close the recording windows.

Start a fresh session if needed. Identify the generated navigation, locator, input action, Enter action and assertion.

### 7.5 Replay

```bash
python -m pytest recordings/member_1.py --browser chromium --headed --slowmo 300
```

| Option | Purpose |
| --- | --- |
| `--browser chromium` | Select Chromium. |
| `--headed` | Display the browser. |
| `--slowmo 300` | Slow operations so you can observe them. |

### 7.6 Record what happened

- Which actions were generated?
- Which locator was selected?
- Was an assertion included?
- Did replay behave as expected?
- What would be missing if the script only clicked and typed?

Commit your observations:

```bash
git add docs/results/member-1.md
git diff --staged
git commit -m "Record browser inspection and recording observations"
git push
```

### Checkpoint

- [ ] Everyone inspected the input.
- [ ] Everyone recorded and replayed a scenario.
- [ ] Everyone recorded actual outcomes and pushed observations.

***

## 8. Create automated checks

### 8.1 Create your test file

Member 1 creates `tests/test_member_1.py`:

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

    task_input.fill("Prepare a testing checklist")
    task_input.press("Enter")

    expect(task_items).to_have_count(1)

    expect(task_labels).to_have_text(
        ["Prepare a testing checklist"]
    )

    expect(task_input).to_have_value("")
```

Use your own filename.

### 8.2 Understand the checks

| Code or concept | Purpose |
| --- | --- |
| `page.goto(URL)` | Open the website. |
| `get_by_placeholder(...)` | Identify the input. |
| `locator(".todo-list li")` | Identify task items. |
| `.fill(...)` and `.press(...)` | Perform actions. |
| `to_have_count(...)` | Check the number of tasks. |
| `to_have_text(...)` | Check task text. |
| `to_have_value("")` | Check that the input is cleared. |

### 8.3 Run in Chromium

```bash
python -m pytest tests/test_member_1.py --browser chromium --headed --slowmo 300
```

Record the actual result.

### 8.4 Add a completion test

Append:

```python
def test_complete_task(page: Page):
    page.goto(URL)

    task_input = page.get_by_placeholder(
        "What needs to be done?",
        exact=True,
    )

    task_items = page.locator(".todo-list li")

    expect(task_items).to_have_count(0)

    task_input.fill("Review practical instructions")
    task_input.press("Enter")

    expect(task_items).to_have_count(1)

    task = task_items.first
    checkbox = task.get_by_role("checkbox")

    checkbox.check()

    expect(checkbox).to_be_checked()

    page.get_by_role(
        "link",
        name="Completed",
        exact=True,
    ).click()

    expect(task_items).to_have_count(1)

    expect(task_items.locator("label")).to_have_text(
        ["Review practical instructions"]
    )
```

Each test creates its own task. The plugin provides a fresh browser context and page for each test using `page`.

### 8.5 Run both tests

```bash
python -m pytest tests/test_member_1.py --browser chromium --headed
```

Expected number in your file: two tests. Record the actual result.

### 8.6 Generate an HTML report

```bash
python -m pytest tests/test_member_1.py --browser chromium --html=reports/member-1-chromium-positive.html --self-contained-html
```

Open the report. Find test names, outcomes, durations and any errors.

### 8.7 Use a readable results block

```markdown
### Test ID: AUTO-1-01

| Item | Details |
| --- | --- |
| Type | Positive |
| Source | `tests/test_member_1.py` |
| Browser | Chromium |
| Status | Not run |

#### Purpose

Check that adding a task displays the correct text.

#### Expected result

One task appears, its text matches and the input is cleared.

#### Execution command

Record the command used.

#### Actual result

Not recorded — test has not been executed.

#### Evidence

Not captured.

---
```

Update after execution. Use Pass, Fail, Blocked or Not run.

### 8.8 Commit and push

```bash
git add tests/test_member_1.py docs/results/member-1.md
git diff --staged
git commit -m "Add and run task creation and completion checks"
git push
```

### Checkpoint

- [ ] Everyone has two guided tests.
- [ ] Actual outcomes are recorded.
- [ ] Everyone inspected an HTML report.
- [ ] Source and records are committed and pushed.

***

## 9. Run data-driven tests and compare browsers

### 9.1 State the expected behaviour

For this exercise:

> Submitting an empty or whitespace-only task should not create a task.

These negative tests pass when the invalid task is not added.

### 9.2 Add the import

At the top of your test file:

```python
import pytest
```

Keep existing imports and tests.

### 9.3 Add the parameterized test

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

### 9.4 Predict the count

Your file contains one add-task test, one completion test and three blank-input cases.

Expected total per browser: five tests.

### 9.5 Run in Chromium

```bash
python -m pytest tests/test_member_1.py --browser chromium --headed --html=reports/member-1-chromium.html --self-contained-html
```

### 9.6 Run in Firefox

```bash
python -m pytest tests/test_member_1.py --browser firefox --headed --html=reports/member-1-firefox.html --self-contained-html
```

This selects Playwright's Firefox build.

### 9.7 Run in WebKit

```bash
python -m pytest tests/test_member_1.py --browser webkit --headed --html=reports/member-1-webkit.html --self-contained-html
```

Record this as Playwright WebKit, not Safari.

### 9.8 Run in Google Chrome

#### Run the existing pytest tests

Ensure stable Chrome is installed:

```bash
python -m pytest tests/test_member_1.py --browser chromium --browser-channel chrome --headed --html=reports/member-1-chrome.html --self-contained-html
```

The test file is unchanged. The channel selects the installed browser.

#### See Chrome selection directly in Python

Create `examples/member_1_chrome.py`:

```python
from playwright.sync_api import sync_playwright, expect

URL = "https://demo.playwright.dev/todomvc/"


def main():
    with sync_playwright() as playwright:
        browser = playwright.chromium.launch(
            channel="chrome",
            headless=False,
            slow_mo=300,
        )

        try:
            context = browser.new_context()

            try:
                page = context.new_page()
                page.goto(URL)

                task_input = page.get_by_placeholder(
                    "What needs to be done?",
                    exact=True,
                )

                task_items = page.locator(".todo-list li")

                expect(task_items).to_have_count(0)

                task_input.fill("Test a task in Google Chrome")
                task_input.press("Enter")

                expect(task_items).to_have_count(1)

                expect(task_items.locator("label")).to_have_text(
                    ["Test a task in Google Chrome"]
                )

                expect(task_input).to_have_value("")

                print("PASS: Google Chrome displayed the expected task.")

            finally:
                context.close()

        finally:
            browser.close()


if __name__ == "__main__":
    main()
```

Run:

```bash
python examples/member_1_chrome.py
```

Expected behaviour:

1. Chrome opens in a separate browser session.
2. The website loads.
3. A task is entered.
4. Assertions check the task count, task text and cleared input.
5. A passing message appears if all assertions succeed.
6. The browser closes.

If a check fails, Python displays an error instead of the passing message. Record the actual result.

### 9.9 Run in Microsoft Edge

#### Run the existing pytest tests

Ensure stable Edge is installed:

```bash
python -m pytest tests/test_member_1.py --browser chromium --browser-channel msedge --headed --html=reports/member-1-edge.html --self-contained-html
```

#### See Edge selection directly in Python

Create `examples/member_1_edge.py`:

```python
from playwright.sync_api import sync_playwright, expect

URL = "https://demo.playwright.dev/todomvc/"


def main():
    with sync_playwright() as playwright:
        browser = playwright.chromium.launch(
            channel="msedge",
            headless=False,
            slow_mo=300,
        )

        try:
            context = browser.new_context()

            try:
                page = context.new_page()
                page.goto(URL)

                task_input = page.get_by_placeholder(
                    "What needs to be done?",
                    exact=True,
                )

                task_items = page.locator(".todo-list li")

                expect(task_items).to_have_count(0)

                task_input.fill("Test a task in Microsoft Edge")
                task_input.press("Enter")

                expect(task_items).to_have_count(1)

                expect(task_items.locator("label")).to_have_text(
                    ["Test a task in Microsoft Edge"]
                )

                expect(task_input).to_have_value("")

                print("PASS: Microsoft Edge displayed the expected task.")

            finally:
                context.close()

        finally:
            browser.close()


if __name__ == "__main__":
    main()
```

Run:

```bash
python examples/member_1_edge.py
```

Expected behaviour matches the Chrome demonstration, but Microsoft Edge is selected. Record what actually happened.

#### Understand the launch code

| Code | Meaning |
| --- | --- |
| `sync_playwright()` | Start Playwright's synchronous Python interface. |
| `playwright.chromium.launch(...)` | Launch a Chromium-family browser. |
| `channel="chrome"` | Select installed Google Chrome. |
| `channel="msedge"` | Select installed Microsoft Edge. |
| `headless=False` | Make the browser visible. |
| `slow_mo=300` | Slow operations so you can observe them. |
| `browser.new_context()` | Create an isolated browser session. |
| `context.new_page()` | Open a page in that session. |
| `finally` | Close resources even if a check fails. |

> [!IMPORTANT]
> These standalone scripts demonstrate explicit browser launching. They do not connect to your everyday signed-in browser profile.
>
> Continue using pytest for the guided reports, screenshots and traces. Plugin options do not automatically configure browsers launched manually by standalone scripts.
>
> The scripts in `examples/` do not change the five-test count in your guided pytest file.

Record standalone executions using:

```markdown
### Chrome or Edge standalone example

#### Source

Record the file used.

#### Command

Record the command used.

#### Expected result

One task appears with the expected text and the input is cleared.

#### Actual result

Record what happened.

#### Status

Pass / Fail / Blocked / Not run

#### Notes

Record installation, policy or execution issues.
```

Stage only the example files you created:

```bash
git add examples/member_1_chrome.py examples/member_1_edge.py
git add docs/results/member-1.md
git diff --staged
git commit -m "Add Chrome and Edge browser automation examples"
git push
```

If you created one example only, stage that file only. Use your actual member number.

### 9.10 Run three managed browsers together

After understanding individual commands:

```bash
python -m pytest tests/test_member_1.py --browser chromium --browser firefox --browser webkit --html=reports/member-1-three-browsers.html --self-contained-html
```

For the five guided cases:

```text
5 cases × 3 browsers = 15 executions
```

Run Chrome and Edge separately using their channel commands.

> [!IMPORTANT]
> Do not combine Chrome or Edge channels with Firefox or WebKit selections. Use channel options only with Chromium in this practical.

### 9.11 Allocate browser comparisons

Everyone runs the guided tests in Chromium. Divide additional comparison work:

| Member | Suggested browser |
| --- | --- |
| 1 | Chromium |
| 2 | Firefox |
| 3 | WebKit |
| 4 | Google Chrome |
| 5 | Microsoft Edge |

For four members, Member 4 also checks Edge if available. Members may try every available browser, but do not repeat full runs unnecessarily.

Document unavailable browsers rather than reporting them as tested.

### 9.12 Record comparisons

Use a block for each browser you personally executed:

```markdown
### Browser comparison — Firefox

- Command:
- Executed by:
- Actual outcome:
- Observations:
- Report filename:
```

For another member's result, link to their record and identify them. Do not claim the execution.

Compare final task behaviour, displayed text, checkbox state, filters and errors. Do not use these small functional runs as a browser-speed benchmark.

### 9.13 Commit and push

Suggested message:

```text
Add data-driven tests and browser comparison results
```

### Checkpoint

- [ ] Everyone ran the five guided cases in Chromium.
- [ ] The group attempted all browser options where available.
- [ ] Chrome and Edge examples were explored by assigned members or recorded for later practice.
- [ ] Browsers and restrictions are identified accurately.
- [ ] Results and observations are committed.

***

## 10. Investigate a failed test

You will deliberately introduce an incorrect expectation. This demonstrates diagnostics, not a website defect.

### 10.1 Change one expectation

In `test_add_task()`, temporarily replace:

```python
expect(task_labels).to_have_text(
    ["Prepare a testing checklist"]
)
```

with:

```python
expect(task_labels).to_have_text(
    ["A different task"]
)
```

Do not change the input text.

### 10.2 Predict the failure

Record the entered text, expected text and why the comparison should fail.

### 10.3 Run with diagnostic options

```bash
python -m pytest tests/test_member_1.py -k test_add_task --browser chromium --headed --screenshot only-on-failure --tracing retain-on-failure --output test-results/member-1-chromium-failure --html=reports/member-1-chromium-failure.html --self-contained-html
```

| Option | Purpose |
| --- | --- |
| `-k test_add_task` | Select tests matching that name. |
| `--screenshot only-on-failure` | Save a failure screenshot. |
| `--tracing retain-on-failure` | Retain a failed test's trace. |
| `--output ...` | Choose the artifact directory. |
| `--html=...` | Generate the report. |

### 10.4 Inspect report and screenshot

Open `reports/member-1-chromium-failure.html`. Find the failed test, assertion line, expected text and actual text.

Open the generated test subfolder under `test-results/member-1-chromium-failure/` and inspect its screenshot.

Does the page show the task the script actually entered?

### 10.5 Open the trace

Find `trace.zip`. Replace the placeholder with its actual path:

```bash
python -m playwright show-trace "PATH_TO_TRACE_ZIP"
```

Inspect navigation, the input action, Enter, page snapshots and the failed assertion.

### 10.6 Preserve selected evidence

Copy useful screenshots into `docs/evidence/member-1/`, for example:

```text
chromium-failure-report.png
chromium-failure-page.png
```

From the results file:

```markdown
[View failure page](../evidence/member-1/chromium-failure-page.png)
```

Copy selected evidence before rerunning because generated output can be replaced. Do not commit the entire artifact directory.

### 10.7 Record the investigation

```markdown
## Failure investigation

### Browser used

### Deliberate change

### Predicted outcome

### Actual outcome

### Screenshot observation

### Trace observation

### Cause

### Correction and rerun
```

Explain why this is a test expectation error rather than a website defect.

### 10.8 Restore and rerun

Restore the original expected text:

```bash
python -m pytest tests/test_member_1.py --browser chromium --html=reports/member-1-chromium-corrected.html --self-contained-html
```

Record the actual outcome.

> [!IMPORTANT]
> Do not remove the assertion or skip the test to obtain a pass. Restore the meaningful expectation. Do not leave the deliberately incorrect assertion in the shared suite.

### 10.9 Commit and push

```bash
git add tests/test_member_1.py docs/results/member-1.md docs/evidence/member-1/
git diff --staged
git commit -m "Document browser failure investigation"
git push
```

Review images directly; a text diff does not display their visual contents.

### Checkpoint

- [ ] Everyone observed the deliberate failure.
- [ ] Everyone inspected the report, screenshot and trace.
- [ ] Everyone restored the correct assertion and recorded the rerun.
- [ ] Records and selected evidence are pushed.

***

## 11. Create your own tests

Each member chooses additional behaviour. There is no prescribed scenario list or fixed test count.

### 11.1 Choose a question

Possible starting points:

- Can a task be edited or deleted?
- Does Active exclude completed tasks?
- Does All show active and completed tasks?
- What happens with duplicate task names?
- Does refreshing preserve tasks within the same context?
- What happens to leading or trailing spaces?

These are prompts, not compulsory tasks.

### 11.2 Agree the allocation

In `docs/team-plan.md`:

```markdown
### Member 1 — Open-ended testing

- Chosen area:
- Question:
- Browser or browsers:
```

### 11.3 Plan before coding

In your own results file:

```markdown
## Self-designed tests

### Testing idea

### Reason

### Test basis

### Starting state

### Planned actions

1.
2.
3.

### Assertions

### Browser selection
```

### 11.4 Use the tools

Explore manually, inspect elements, use Codegen's locator picker, adapt earlier patterns and inspect diagnostic artifacts.

Start each test from a known state. Include setup within the test; do not rely on another test's tasks.

Commit the plan and initial code:

```text
Add self-designed browser test
```

### 11.5 Execute and adapt

1. Run your file.
2. Compare actual and expected behaviour.
3. Investigate unexpected outcomes.
4. Try a second browser if useful.
5. Add follow-up cases if appropriate.
6. Record what you learned.

If the expectation is unclear, state the assumption or question. Do not claim a confirmed defect based only on preference. Use `Observation only` when no clear pass/fail basis exists. Leave unexecuted work marked Not run.

### 11.6 Commit the results

Suggested message:

```text
Record self-designed browser testing results
```

### Checkpoint

- [ ] Every member chose a question and executed additional tests.
- [ ] Browser selection is recorded.
- [ ] Assumptions, actual outcomes and remaining questions are documented.
- [ ] Contributions are committed and pushed.

***

## 12. Combine contributions and reflect

### 12.1 Complete your reflection

In your own file under `docs/reflections/`, answer:

- What did Codegen do, and what did you still decide?
- How do actions differ from assertions?
- Why can a negative test pass?
- How did parametrization reduce repetition?
- What changed when you selected another browser?
- Why is Playwright WebKit not installed Safari?
- How do standalone scripts differ from pytest execution?
- How did screenshots and traces help?
- What can these checks not determine?
- How does your Git history show your progress?

Commit and push the reflection.

### 12.2 Create your PR

```text
base: main
compare: your personal work branch
```

Suggested title:

```text
Add Member 1 automated testing tools practical
```

Description:

```markdown
## What changed?

- Recording and replay:
- Guided checks:
- Data-driven tests:
- Browser comparisons:
- Chrome or Edge examples:
- Failure investigation:
- Self-designed tests:

## What did I execute?

- Commands:
- Browsers:
- Actual outcomes:
- Known limitations:

## Supporting records

- Results:
- Reflection:
- Selected evidence:
```

### 12.3 Merge one contribution at a time

Formal peer approval and reproduction are not required. Before merging, inspect Files changed and confirm:

- Files are in intended locations.
- No other member's work is overwritten.
- No deliberately incorrect assertion remains.
- Evidence links work.
- No sensitive information is included.
- Environments and generated reports are not committed.

Use Create a merge commit if available to preserve individual commits.

### 12.4 Everyone: update local `main`

Start with no uncommitted changes:

```bash
git switch main
git pull --ff-only origin main
git status
```

### 12.5 Coordinator: prepare the summary

```bash
git switch -c docs/group-summary
```

Complete `docs/summary.md`:

```markdown
# Group summary

## Tools experienced

- Browser Developer Tools:
- Codegen:
- Playwright:
- pytest:
- HTML report:
- Trace Viewer:

## Browser coverage

### Chromium
- Tester:
- Result record:
- Main observation:

### Firefox
- Tester:
- Result record:
- Main observation:

### WebKit
- Tester:
- Result record:
- Main observation:

### Google Chrome
- Tester:
- Result record:
- Main observation:

### Microsoft Edge
- Tester:
- Result record:
- Main observation:

## Member 1

- Tests: [View source](../tests/test_member_1.py)
- Results: [View record](results/member-1.md)
- Reflection: [View reflection](reflections/member-1.md)
- Standalone examples, if completed:
- Self-designed investigation:
- Main observation:
- Pull request:

## Member 2

Repeat for every member.

## Group conclusion

- What did automation make easier?
- What setup or maintenance was needed?
- Which browser differences were observed?
- Which observations required human judgement?
- What would the group explore next?
```

Run the integrated pytest suite once in Chromium:

```bash
python -m pytest --browser chromium --html=reports/group-final-chromium.html --self-contained-html
```

Record the actual result. Standalone scripts under `examples/` are not part of this pytest run.

Repeated guided tests demonstrate individual participation, not additional unique functional coverage. Do not repeatedly run the full suite across all browsers without a reason.

Commit and merge the summary through a PR. Everyone updates local `main` again.

### 12.6 Inspect Git history

```bash
git log --oneline --graph --decorate --all -20
```

Inspect a commit using its actual ID:

```bash
git show COMMIT_ID
```

Explain what changed and how you know.

### Final practical checkpoint

- [ ] Contributions and the summary are merged.
- [ ] Browser coverage and restrictions are documented.
- [ ] Everyone updated local `main`.
- [ ] Everyone can explain a commit.
- [ ] Actual outcomes are recorded honestly.
- [ ] No deliberately incorrect assertion remains.

***

## 13. Troubleshooting and command reference

### Before attempting a fix

1. Read the error message.
2. Confirm the intended command.
3. Check the folder, branch and Python interpreter.
4. Confirm the selected browser or channel.
5. Preserve your work.
6. Ask your Tutor if the state is unclear.

```bash
git status
git branch --show-current
python -c "import sys; print(sys.executable)"
```

### Common problems

| Problem | What to check first |
| --- | --- |
| Python is not recognised | Reopen the terminal; try the appropriate launcher. |
| Packages cannot be imported | Confirm the interpreter points to `.venv`. |
| Activation is blocked | Use an approved terminal or invoke the environment interpreter directly. |
| Chromium is missing | Run `python -m playwright install chromium`. |
| Firefox is missing | Run `python -m playwright install firefox`. |
| WebKit is missing | Run `python -m playwright install webkit`. |
| Chrome cannot be found | Check stable Chrome is installed in its normal location. |
| Edge cannot be found | Check stable Edge is installed in its normal location. |
| WebKit reports missing libraries | Ask your Tutor about supported systems and approved dependencies. |
| Chrome or Edge is blocked by policy | Document it; do not bypass the restriction. |
| Standalone script has no pytest report | It is run with `python`, not pytest; use guided tests for reports. |
| Browser closes after a standalone example | Expected: cleanup closes it when the script finishes or a check fails. |
| No tests are found | Check saved files, `test_` names and selected path. |
| Browser is not visible | Use `--headed` in pytest or `headless=False` in standalone code. |
| Locator does not match | Inspect the current page with Codegen or Developer Tools. |
| HTML report has no screenshot | Open Playwright artifacts separately. |
| Evidence disappeared | Copy selected artifacts before rerunning. |
| Evidence link is broken | Check path, case and whether the file was committed and pushed. |
| Too many files appear in Git | Check `.gitignore`. |
| Push is rejected | Check authentication, permissions and remote changes; do not force-push. |
| Sensitive data was committed | Stop sharing and inform your Tutor; deletion alone does not remove history. |

### Channel and engine mismatch

Use Chrome or Edge channels with Chromium:

```bash
python -m pytest tests/test_member_1.py --browser chromium --browser-channel chrome
python -m pytest tests/test_member_1.py --browser chromium --browser-channel msedge
```

Do not attach those channels to Firefox or WebKit.

### Playwright was upgraded

Reinstall required managed browsers:

```bash
python -m playwright install chromium firefox webkit
```

Browser binaries must match the installed Playwright version.

### `git pull --ff-only` refuses

Inspect before changing anything:

```bash
git status
git branch --show-current
git fetch origin
git log --oneline --graph --decorate --all -15
```

If you accidentally committed on local `main`, preserve those commits:

```bash
git switch -c recovery/my-main-work
```

Ask your Tutor how to integrate safely. Do not reset or force-push to bypass the problem.

### Browser command reference

| Browser | Command |
| --- | --- |
| Chromium | `python -m pytest tests/test_member_1.py --browser chromium --headed` |
| Firefox | `python -m pytest tests/test_member_1.py --browser firefox --headed` |
| WebKit | `python -m pytest tests/test_member_1.py --browser webkit --headed` |
| Chrome | `python -m pytest tests/test_member_1.py --browser chromium --browser-channel chrome --headed` |
| Edge | `python -m pytest tests/test_member_1.py --browser chromium --browser-channel msedge --headed` |

### Other testing commands

| Command | Purpose |
| --- | --- |
| `python -m pip install -r requirements.txt` | Install packages. |
| `python -m playwright install chromium firefox webkit` | Install managed browsers. |
| `python -m playwright codegen URL` | Open the recorder. |
| `python -m pytest tests/test_member_1.py -k test_add_task` | Select a named test. |
| `python -m playwright show-trace "PATH_TO_TRACE_ZIP"` | Open a trace. |
| `python examples/member_1_chrome.py` | Run the standalone Chrome example. |
| `python examples/member_1_edge.py` | Run the standalone Edge example. |

### Git commands

| Command | Purpose |
| --- | --- |
| `git status` | Inspect branch and working state. |
| `git branch --show-current` | Display the current branch. |
| `git diff` | Inspect unstaged changes to tracked files. |
| `git add FILE` | Select changes for a commit. |
| `git diff --staged` | Inspect selected changes. |
| `git commit -m "Message"` | Record selected changes locally. |
| `git push` | Upload commits to the matching branch. |
| `git fetch origin` | Download information about shared changes. |
| `git log --oneline` | Inspect compact history. |
| `git show COMMIT_ID` | Inspect a commit. |

***

## 14. Individual completion checklist

- [ ] I cloned the shared repository and created my own branch.
- [ ] I created a virtual environment and installed the tools.
- [ ] I checked browser availability and recorded restrictions.
- [ ] I inspected the website input.
- [ ] I recorded and replayed browser interactions.
- [ ] I created my own test file.
- [ ] I can distinguish actions from assertions.
- [ ] I ran positive and negative tests.
- [ ] I used a parameterized test.
- [ ] I selected another available browser.
- [ ] I recorded exact browser names and commands.
- [ ] I understand Chrome and Edge channel selection.
- [ ] I understand standalone scripts versus pytest tests.
- [ ] I generated an HTML report.
- [ ] I inspected a screenshot and trace.
- [ ] I restored the deliberately incorrect expectation.
- [ ] I created additional tests.
- [ ] I recorded actual outcomes and uncertainties.
- [ ] I committed and pushed my own work.
- [ ] I integrated my contribution through a PR.
- [ ] I completed my reflection.
- [ ] I can explain one of my commits.
- [ ] No sensitive information was committed.
- [ ] My local `main` is updated and my working directory is clean.

***

## 15. Optional extension activities — outside the in-class practical

These activities are not required for the guided 2.5-hour session. Attempt them independently if you have the interest, time and bandwidth. Continue using Git.

### A. Complete remaining browser comparisons

If all five options are available, run the same guided cases in each:

```text
Chromium: 5
Firefox: 5
WebKit: 5
Chrome: 5
Edge: 5

Total: 25 executions
```

These are five functional cases in five configurations, not 25 different functional scenarios. Standalone examples are separate executions.

### B. Complete both standalone examples

If your allocated work included only one browser, try the other example. Explain the difference between `channel="chrome"` and `channel="msedge"`.

### C. Compare failure evidence across browsers

Repeat the deliberate incorrect expectation in another browser. Use distinct report and artifact paths. Restore the correct expectation before committing final tests.

### D. Explore video evidence

```bash
python -m pytest tests/test_member_1.py -k test_add_task --browser firefox --video on
```

Compare video with a trace. Keep generated videos local unless your Tutor requests evidence.

### E. Extend your investigation

1. Choose an unanswered question.
2. Explain why it matters.
3. Design a follow-up case.
4. Execute it in one or more available browsers.
5. Record what changed in your understanding.

### F. Improve the handover

Check whether another student can locate the test source, starting state, inputs, expected and actual results, browser selection, evidence and uncertainties without a verbal explanation.

Keep records factual. Do not change outcomes merely to make documentation look complete.

***

## Closing reminder

The aim is not to memorise commands or simply make browsers move automatically. Develop the habit of understanding the task, selecting meaningful checks, identifying the browser used, inspecting results and preserving evidence.

```text
Explore → Record → Replay → Add checks → Vary data
        → Compare browsers → Investigate → Commit → Share → Reflect
```
