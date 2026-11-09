# Automated Testing Tools Practical

> A self-paced, hands-on introduction to browser automation for absolute beginners.

> [!NOTE]
> ## Educational Practice Materials
>
> This guide uses a public demonstration website for introductory automated testing practice. Use fictional task names only.
>
> Do not enter or share passwords, API keys, identification numbers, personal contact details or confidential information. Screenshots and traces may contain information shown on the page.

This practical helps you learn automated testing tools by using them. You will open a demonstration task-list website, automate browser actions and check the results.

No previous automated testing experience is needed. Complete Python examples are provided. If Python is also new to you, copy the examples first and read the explanations beside them. You do not need to build a website, learn JavaScript or create an application server.

This is a learning practical, not an assessment. There are no marks, submissions, required reflections or evidence portfolios. Work independently at your own pace. You may discuss problems with others, but group coordination is not required.

### Tools used in this practical

| Tool | What you will use it for |
| --- | --- |
| Python | Run the test code. |
| Visual Studio Code, or VS Code | Create and edit files. |
| Microsoft Python extension for VS Code | Help VS Code use the project's Python environment. |
| Browser Developer Tools | Look at a page element and its attributes. |
| Playwright | Open a browser, perform actions and check page behaviour. |
| Playwright Codegen | Record browser actions and create starting code. |
| pytest | Find and run tests. |
| pytest-html | Create a results page you can open in a browser. |
| Playwright Trace Viewer | Look back through a test's actions and page snapshots. |
| Git, optional | Save versions of your source files. |

Codegen and Trace Viewer are included with Playwright. Developer Tools is included with desktop browsers such as Chrome and Edge.

### Browser options included

Use Chromium for the main activities. Other browsers are optional.

| Browser option | How it is made available | Test selection |
| --- | --- | --- |
| Chromium | Download through Playwright. | `--browser chromium` |
| Firefox, optional | Download Playwright's Firefox build. | `--browser firefox` |
| WebKit, optional | Download Playwright's WebKit build. | `--browser webkit` |
| Google Chrome, optional | Use installed stable Chrome. | `--browser chromium --browser-channel chrome` |
| Microsoft Edge, optional | Use installed stable Edge. | `--browser chromium --browser-channel msedge` |

> [!IMPORTANT]
> Ordinary Firefox does not replace Playwright's supported Firefox build. Playwright WebKit is not the installed Safari application.

### Practical overview

| Item | Details |
| --- | --- |
| Working arrangement | Individual, self-directed practice. |
| Duration | Self-paced. Pause and return whenever needed. |
| Previous testing knowledge | None. |
| Python knowledge | Helpful, but complete examples and explanations are provided. |
| Test website | [Playwright TodoMVC demonstration](https://demo.playwright.dev/todomvc/) |
| What you will create | A small test file, a recording and local results files. |
| Assessment | None. No submission or written reflection is required. |
| Focus | Learning testing tools, not developing an application. |

## Contents

1. [Learning goals](#1-learning-goals)
2. [Understand the workflow](#2-understand-the-workflow)
3. [Prepare your computer](#3-prepare-your-computer)
4. [Create the project and starting files](#4-create-the-project-and-starting-files)
5. [Prepare your Python environment](#5-prepare-your-python-environment)
6. [Explore the website](#6-explore-the-website)
7. [Create your first automated check](#7-create-your-first-automated-check)
8. [Check task completion](#8-check-task-completion)
9. [Run one test with different inputs](#9-run-one-test-with-different-inputs)
10. [Record and replay browser actions](#10-record-and-replay-browser-actions)
11. [Create a results report](#11-create-a-results-report)
12. [Investigate a failed check](#12-investigate-a-failed-check)
13. [Troubleshooting and command reference](#13-troubleshooting-and-command-reference)
14. [Optional browser comparisons](#14-optional-browser-comparisons)
15. [Optional further practice](#15-optional-further-practice)

***

## 1. Learning goals

The guided activities introduce how to:

- Open and control a browser with Playwright.
- Find an input or checkbox on a page.
- Distinguish an action from an assertion.
- Check valid and invalid inputs.
- Run one test with several input values.
- Record and replay browser actions.
- Open an HTML results report.
- Use a screenshot and trace to understand a failed check.

These goals describe what the guide teaches. You do not need to submit answers or demonstrate completion.

### Working through this practical

1. Follow the main activities in order.
2. Read the short explanation before running a command.
3. Type commands in the terminal.
4. Put Python code in the named `.py` file.
5. Save a file before running it.
6. Compare the result with the description under the command.
7. Use Section 13 if something differs.

> [!IMPORTANT]
> Run commands from the project folder unless a step says otherwise. Activate the project's Python environment before running tests.
>
> Copy only the code inside a code block. Do not copy the surrounding backticks or the language label, such as `python`.

### Suggested learning sessions

| Session | Activities |
| --- | --- |
| Setup | Sections 3–5. Allow extra time for downloads. |
| First tests | Sections 6–9. |
| Recording and diagnostics | Sections 10–12. |
| Further practice | Sections 14–15, only when you are ready. |

There is no fixed completion time. Repeat a section whenever useful.

***

## 2. Understand the workflow

### A simple mental model

The website is the application you want to check.

Playwright follows your browser instructions. pytest finds and runs the test functions. Assertions check whether the page matches your expectations.

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
| Positive test | A test of valid input or an expected action. |
| Negative test | A test of invalid input or an invalid action. |
| Parametrization | Running the same test with different input values. |
| Virtual environment | A separate set of Python packages for this project. |
| Headed | The browser window is visible during the run. |
| Headless | The test runs without displaying the browser window. |
| Report | A summary of a test run. |
| Trace | A record that helps you look back through a test run. |

### Actions and assertions

These lines perform actions:

```python
task_input.fill("Read testing notes")
task_input.press("Enter")
```

This line checks a result:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

These are explanatory snippets, not complete programs. You will use complete examples later.

A script that only types and clicks may finish without checking that the correct task appeared.

### Positive and negative do not mean pass and fail

| Scenario | Expected behaviour | Passing outcome |
| --- | --- | --- |
| Add a normal task. | The task appears. | The task appears with the correct text. |
| Submit an empty task. | No task is added. | The list remains empty. |

A negative test passes when the website handles invalid input as expected.

> [!WARNING]
> Use small, deliberate practice runs. Do not perform load testing, security scans or continuous repeated runs against the public website.

***

## 3. Prepare your computer

### 3.1 Install or check Python

Use Python 3.12 or 3.13 for this guide. If a suitable version is already installed, do not reinstall it.

#### Windows

1. Open [Python Downloads](https://www.python.org/downloads/).
2. Install Python for your computer.
3. Select `Add Python to PATH` if offered.
4. Close and reopen your terminal after installation.
5. Run:

```powershell
python --version
```

If that command is unavailable, try:

```powershell
py -3 --version
```

You should see a Python version. If only the second command works, use it to create the environment in Section 5.1.

#### macOS or Linux

Open Terminal and run:

```bash
python3 --version
```

If necessary, install Python using the approved installation method for your computer. For macOS, an installer is available from [Python Downloads for macOS](https://www.python.org/downloads/macos/).

> [!NOTE]
> On managed computers, software installation may need administrator permission. Use the approved software process or ask IT support to install missing software. Do not replace system-managed Python or bypass restrictions.

### 3.2 Install VS Code and its Python extension

1. Install [Visual Studio Code](https://code.visualstudio.com/) if needed.
2. Open VS Code.
3. Open Extensions.
4. Search for `Python`.
5. Install the extension published by Microsoft.

The extension helps the editor work with Python. It does not install Python itself.

### What you should have now

Python displays a version number, and VS Code opens successfully. Git, GitHub, Chrome and Edge are not required for the main activities.

***

## 4. Create the project and starting files

### 4.1 Create and open the project folder

1. Create a folder named `automated-testing-practice` where you can save files.
2. In VS Code, select File → Open Folder.
3. Open that folder.
4. Select Terminal → New Terminal.

The terminal is where you enter commands. Keep this project folder open throughout the practical.

> [!TIP]
> If the terminal shows a Python prompt beginning with `>>>`, enter `exit()` and press Enter. Commands such as `python -m pytest` belong in the normal terminal, not inside Python.

### 4.2 Create the starting structure

In the VS Code file explorer, right-click the project folder and use New File or New Folder to create:

```text
automated-testing-practice/
├── requirements.txt
├── pytest.ini
├── tests/
│   └── test_tasks.py
├── recordings/
└── reports/
```

The `tests` folder holds your test code. The other two folders hold local recordings and reports.

### 4.3 Create `requirements.txt`

Paste and save:

```text
pytest-playwright
pytest-html
```

This lists the Python testing packages to install.

### 4.4 Create `pytest.ini`

Paste and save:

```ini
[pytest]
testpaths = tests
addopts = -v
```

This tells pytest to look in `tests` and display each test's name.

Leave `tests/test_tasks.py` empty for now.

### What you should see

The files and folders appear in VS Code's file explorer. No tests have been run yet.

***

## 5. Prepare your Python environment

### 5.1 Create a virtual environment

A virtual environment keeps this project's packages separate from other projects.

Run only the command for your computer.

Windows:

```powershell
python -m venv .venv
```

If only the Windows launcher worked earlier:

```powershell
py -3 -m venv .venv
```

macOS or Linux:

```bash
python3 -m venv .venv
```

A `.venv` folder should appear. The command may finish without displaying a message.

If Linux reports missing virtual-environment support, use the approved software process or ask IT support to install that component.

### 5.2 Activate the environment

Use the command for your terminal. Do not run all the alternatives.

| Terminal | Command |
| --- | --- |
| Windows PowerShell | `.\.venv\Scripts\Activate.ps1` |
| Windows Command Prompt | `.venv\Scripts\activate.bat` |
| Windows Git Bash | `source .venv/Scripts/activate` |
| macOS or Linux | `source .venv/bin/activate` |

Check which Python is running:

```bash
python -c "import sys; print(sys.executable)"
```

The displayed path should contain this project's `.venv` folder.

> [!TIP]
> If PowerShell blocks activation, open Command Prompt using the dropdown beside the terminal's `+` button, then use the Command Prompt command above. You do not need to weaken security settings.
>
> You can also replace `python` in later commands with `.\.venv\Scripts\python.exe` in PowerShell, or `./.venv/bin/python` on macOS/Linux.

### 5.3 Select the VS Code interpreter

1. Press Ctrl+Shift+P on Windows/Linux or Cmd+Shift+P on macOS.
2. Search for `Python: Select Interpreter`.
3. Select the Python inside `.venv`.

The interpreter is the Python program that runs your code.

### 5.4 Install the testing packages

```bash
python -m pip install -r requirements.txt
```

Wait until the command finishes and the terminal is ready for another command.

### 5.5 Install Chromium

```bash
python -m playwright install chromium
```

This downloads Playwright's browser. Installing ordinary Chrome does not replace this step.

If a download fails, check your connection and retry. On a managed network, use approved settings rather than disabling security controls.

### 5.6 Check the installation

```bash
python -m pytest --version
python -m playwright --version
```

Each command should display a version number.

### Returning another day

Open the same folder, open a terminal and activate `.venv` again. You do not need to repeat installation unless the environment has been removed or the packages have changed.

***

## 6. Explore the website

### 6.1 Try the task list manually

Open [Playwright TodoMVC](https://demo.playwright.dev/todomvc/) in your usual browser.

1. Click the input labelled `What needs to be done?`.
2. Enter `Read testing notes`.
3. Press Enter.
4. Find the new task.
5. Select its checkbox.
6. Try the All, Active and Completed links.

Your tests will perform similar actions.

Your usual browser and the test browser use separate sessions. You do not need to delete the tasks in your usual browser before running tests.

### 6.2 Look at the input element

In Chrome or Edge:

1. Right-click the task input and select Inspect.
2. Find the selected input in Developer Tools.
3. Look for `placeholder="What needs to be done?"`.
4. Close Developer Tools when finished.

An attribute is extra information attached to a page element. Here, the placeholder gives the input its hint text. Playwright can use that text to find the input.

There is nothing to write or submit for this activity.

***

## 7. Create your first automated check

### 7.1 Paste the complete test

Open `tests/test_tasks.py`. Paste all of this code and save it. Keep the indentation: the spaces at the start of lines inside the function.

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

### 7.2 Run the test

In the terminal:

```bash
python -m pytest tests/test_tasks.py --browser chromium --headed --slowmo 300
```

### What you should see

A browser opens, the website loads, a task appears and the browser closes. If all checks succeed, the terminal reports `1 passed`.

Read the actual terminal result. If it differs, use Section 13.

| Option | Purpose |
| --- | --- |
| `--browser chromium` | Use Chromium. |
| `--headed` | Show the browser. |
| `--slowmo 300` | Slow browser actions so you can watch them. |

### 7.3 Understand the code

| Code | Simple explanation |
| --- | --- |
| `from ... import ...` | Makes Playwright's tools available. |
| `URL = ...` | Stores the website address. |
| `def test_add_task(...)` | Defines a test. pytest recognises names starting with `test_`. |
| `page` | A browser page supplied by the Playwright pytest package. |
| `page: Page` | A type hint that helps the editor understand `page`. |
| `page.goto(URL)` | Opens the website. |
| `get_by_placeholder(...)` | Finds the task input by its hint text. |
| `exact=True` | Requires the whole placeholder text to match. |
| `locator(".todo-list li")` | Finds task rows using a CSS selector. |
| `task_items.locator("label")` | Finds the text labels inside those rows. |
| `fill(...)` | Replaces text in the input. |
| `press("Enter")` | Presses Enter in the input. |
| `to_have_count(...)` | Checks the number of matching rows. |
| `to_have_text([...])` | Checks the expected task labels. |
| `to_have_value("")` | Checks that the input is empty. |

You can reuse the CSS selector without learning CSS first. Square brackets in the text check hold a list of expected labels.

Playwright's page checks wait briefly for the expected condition. Do not add arbitrary pauses to make the test work.

***

## 8. Check task completion

### 8.1 Add the second test

Paste this below the first test in `tests/test_tasks.py`. Keep the existing code.

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

Save, then run:

```bash
python -m pytest tests/test_tasks.py --browser chromium --headed
```

### What you should see

If both tests succeed, the terminal reports `2 passed`.

| New code | What it does |
| --- | --- |
| `first` | Selects the first matching task row. |
| `get_by_role("checkbox")` | Finds the checkbox in that row. |
| `check()` | Selects the checkbox. |
| `to_be_checked()` | Checks that it is selected. |
| `get_by_role("link", name="Completed", exact=True)` | Finds the Completed link. |

Each test gets a fresh browser session. The second test creates its own task; it does not use a task left by the first test.

***

## 9. Run one test with different inputs

### 9.1 Understand the expected behaviour

Submitting an empty or spaces-only task should not add a task. These negative tests pass when the list remains empty.

### 9.2 Add the import

Add `import pytest` at the top of `tests/test_tasks.py`. Keep the existing imports and tests.

The top should now look like this:

```python
import pytest
from playwright.sync_api import Page, expect

URL = "https://demo.playwright.dev/todomvc/"
```

### 9.3 Add the test

Paste this at the bottom of the same file:

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

### 9.4 Understand the input list

The line beginning with `@` tells pytest to run this function once for each input. This is called parametrization.

| Part | Meaning |
| --- | --- |
| `""` | An empty string: no characters. |
| `" "` | One space. |
| `"   "` | Three spaces. |
| `task_text` | Receives the current input. |
| `ids` | Supplies readable names for the three runs. |
| `task_text: str` | A type hint saying that the input is text. |

### 9.5 Run the file

```bash
python -m pytest tests/test_tasks.py --browser chromium --headed
```

### What you should see

Your two earlier tests and three blank-input cases produce five runs. If they all succeed, the terminal reports `5 passed`.

These examples do not cover every possible invalid input.

***

## 10. Record and replay browser actions

### 10.1 Start Codegen

Check that the `recordings` folder exists. Run:

```bash
python -m playwright codegen --target python-pytest -o recordings/recorded_task.py https://demo.playwright.dev/todomvc/
```

A browser and recording controls should open.

### 10.2 Record a short scenario

1. In the recording browser, enter `Try the recorder`.
2. Press Enter.
3. Find the text assertion control in the recording toolbar. Hover over controls to read their labels.
4. Select that control, then select the new task's text.
5. Look for an `expect(...)` line in the generated code.
6. Close the recording windows to finish.

> [!TIP]
> If you cannot find the assertion control, record the actions first. You can add the check manually using the steps below.

### 10.3 Add a check if needed

Open `recordings/recorded_task.py`. If the generated test does not check the task text, add this after its action that presses Enter:

```python
expect(page.locator(".todo-list li label")).to_have_text(
    ["Try the recorder"]
)
```

Indent these lines to match the other code inside the function.

If `expect` is not already imported, add this at the top of the file:

```python
from playwright.sync_api import expect
```

### 10.4 Replay

Save and run:

```bash
python -m pytest recordings/recorded_task.py --browser chromium --headed --slowmo 300
```

### What you should see

The recorded browser actions run again. The text assertion checks the resulting task.

This command explicitly selects the recording file. The recording is separate from the five cases in `tests/test_tasks.py`.

A recording with only clicks and typing may finish successfully without checking the intended result. Always read the generated code.

***

## 11. Create a results report

### 11.1 Generate the report

Check that the `reports` folder exists, then run:

```bash
python -m pytest tests/test_tasks.py --browser chromium --html=reports/results.html --self-contained-html
```

This command leaves out `--headed`, so the browser is not displayed. The tests still run.

### 11.2 Open the report

1. Find your project folder in File Explorer or Finder.
2. Open `reports`.
3. Open `results.html` in your usual browser.

### What you should see

The report shows test names, results, durations and any error details. Expand a failed result to read more.

> [!NOTE]
> The report summarises that run. It does not prove that the tests cover everything the website can do. You do not need to write or submit a separate report.

***

## 12. Investigate a failed check

You will deliberately change an expectation to make one test fail. This demonstrates troubleshooting, not a confirmed website defect.

### 12.1 Change one expectation

In `test_add_task()`, temporarily change:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

to:

```python
expect(task_labels).to_have_text(["A different task"])
```

Do not change the text entered by `task_input.fill(...)`.

### 12.2 Run that test with diagnostic output

Save and run:

```bash
python -m pytest tests/test_tasks.py::test_add_task --browser chromium --headed --screenshot only-on-failure --tracing retain-on-failure --output test-results/failure-demo
```

| Option | Purpose |
| --- | --- |
| `::test_add_task` | Select only this test function. |
| `--screenshot only-on-failure` | Save a screenshot if the test fails. |
| `--tracing retain-on-failure` | Keep the failed test's trace. |
| `--output ...` | Choose where generated files are saved. |

### What you should see

The test fails because it enters `Read testing notes` but expects `A different task`. Read the expected and actual text in the terminal error.

Here, the test expectation is deliberately wrong. The failure does not demonstrate a website defect.

### 12.3 Open the screenshot

In VS Code's file explorer, open `test-results/failure-demo`, then the generated test subfolder. Open its screenshot.

The subfolder name is generated automatically. Find it in the file explorer rather than guessing its name.

### 12.4 Open the trace

Find `trace.zip` in that subfolder. Right-click it in VS Code and select Copy Relative Path.

Replace the placeholder below with the copied path. Keep the quotation marks.

```bash
python -m playwright show-trace "PASTE_RELATIVE_PATH_HERE"
```

In Trace Viewer, select actions in order. Look at the page loading, text entry, Enter key and failed check.

There is no written investigation to submit. Use the viewer to understand what happened.

### 12.5 Restore and rerun

Restore the correct assertion:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

Save and run:

```bash
python -m pytest tests/test_tasks.py --browser chromium
```

If all checks succeed, the summary reports `5 passed`.

> [!IMPORTANT]
> Do not remove or skip the assertion to hide the failure. Restore the meaningful expectation.
>
> Generated screenshots and traces may be replaced by later runs using the same output location. Copy a file elsewhere first only if you want to keep it for yourself.

***

## 13. Troubleshooting and command reference

### Before attempting a fix

1. Save the file.
2. Read the error message.
3. Check the current folder and Python interpreter.
4. Check the selected file and browser.
5. Preserve your work before making larger changes.

```bash
python -c "from pathlib import Path; import sys; print('Folder:', Path.cwd()); print('Python:', sys.executable)"
```

The folder should be `automated-testing-practice`. The Python path should contain `.venv`.

### Common problems

| Problem | What to try |
| --- | --- |
| Python is not recognised | Reopen the terminal. On Windows, try `py -3 --version`. Review Section 3 if Python is missing. |
| Packages cannot be imported | Activate `.venv`, check the Python path, then repeat `python -m pip install -r requirements.txt`. |
| Activation is blocked | Use Command Prompt or invoke the environment's Python directly as described in Section 5.2. |
| Chromium is missing | Run `python -m playwright install chromium`. |
| No tests are found | Save the file. Check its name is `test_tasks.py`, not `test_tasks.py.txt`, and its functions begin with `test_`. |
| A file cannot be found | Check that the terminal is in the project folder and the filename matches the command. |
| `IndentationError` | Match the example's leading spaces. Use four spaces inside a function. Do not mix tabs and spaces. |
| `SyntaxError` | Check quotes, brackets and colons. Do not paste Markdown backticks into Python files. |
| Browser is not visible | Add `--headed`. |
| Browser closes quickly | Normal after a run. Use `--headed --slowmo 300` and read the terminal result afterwards. |
| Expected text differs | Compare the input and assertion, including spelling, capital letters and spaces. |
| Website does not load | Open the demo URL in your usual browser. Check the connection. If the site is unavailable, save your work and retry later. |
| Locator times out | Check that the page loaded and the locator text matches the page. Use Inspect or Codegen to examine the element. |
| Report has no screenshot | Open the generated Playwright screenshot separately under `test-results`. |
| Generated output disappeared | Later runs may replace it. Copy files elsewhere first if you want to keep them. |
| Browser or download is blocked by policy | Use approved software and network processes. Do not bypass the restriction. |
| Linux reports missing browser libraries | Use a supported approved environment or ask IT support to install the required system dependencies. |

If Playwright has been upgraded, run its browser installation command again:

```bash
python -m playwright install chromium
```

If the problem remains, keep your files and the full error message. Do not delete the project as a first troubleshooting step. Optional activities can wait.

### Testing command reference

| Goal | Command |
| --- | --- |
| Watch the tests | `python -m pytest tests/test_tasks.py --browser chromium --headed --slowmo 300` |
| Run without a visible browser | `python -m pytest tests/test_tasks.py --browser chromium` |
| Run one test | `python -m pytest tests/test_tasks.py::test_add_task --browser chromium --headed` |
| Create a report | `python -m pytest tests/test_tasks.py --browser chromium --html=reports/results.html --self-contained-html` |
| Replay the recording | `python -m pytest recordings/recorded_task.py --browser chromium --headed --slowmo 300` |

***

## 14. Optional browser comparisons

The main activities use Chromium. Try another browser only when you are comfortable running your existing tests. You do not need to install every option.

### 14.1 Firefox

```bash
python -m playwright install firefox
python -m pytest tests/test_tasks.py --browser firefox --headed
```

This uses Playwright's supported Firefox build, not an ordinary installed Firefox.

### 14.2 WebKit

```bash
python -m playwright install webkit
python -m pytest tests/test_tasks.py --browser webkit --headed
```

This is Playwright WebKit, not the installed Safari application. Skip this option if approved system dependencies are unavailable.

### 14.3 Installed Google Chrome

If stable Chrome is installed:

```bash
python -m pytest tests/test_tasks.py --browser chromium --browser-channel chrome --headed
```

### 14.4 Installed Microsoft Edge

If stable Edge is installed:

```bash
python -m pytest tests/test_tasks.py --browser chromium --browser-channel msedge --headed
```

The channel selects the installed browser. Your test code stays the same.

> [!IMPORTANT]
> Use Chrome and Edge channels only with Chromium. Do not combine them with Firefox or WebKit selections.
>
> Compare the functional results, not browser speed. These small test runs are not performance benchmarks.

***

## 15. Optional further practice

These activities are for extra practice. There is no required number to complete and no written submission.

### A. Change the task name

In `test_add_task()`, change `Read testing notes` to another fictional task name in both places: the input action and the text assertion. Save and rerun.

### B. Add another input

Replace the parametrization block above the blank-input function with:

```python
@pytest.mark.parametrize(
    "task_text",
    ["", " ", "   ", "    "],
    ids=["empty", "one-space", "three-spaces", "four-spaces"],
)
```

Keep the function below it unchanged. There is one ID for each input. Your file now runs six cases.

### C. Use a helper to add two tasks

A helper is a function that performs steps you want to reuse. Add both functions below to your existing test file. Keep its imports and URL.

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

Run your file with the command from Section 13. This adds one test to your existing count. The helper performs actions; the test contains the checks.

### D. Record another action

Record completing, editing or deleting a task. Try the action manually first. Read the generated code and reuse earlier assertion patterns to check the result.

If expected behaviour is unclear, treat the result as an observation rather than claiming a confirmed defect.

### E. Save source files with Git

Git is optional. Your local project folder is enough for the main activities.

If you already use Git, create `.gitignore` before adding files:

```gitignore
.venv/
__pycache__/
.pytest_cache/
test-results/
reports/
recordings/
.env
```

Keep source files and configuration files. Do not share private data or generated traces. Review files before uploading them.

Group branches, pull requests, contribution records, evidence portfolios and reflections are not required.

***

## Closing reminder

A passing test means its particular checks succeeded in that run. It does not prove that the whole website is error-free.

Keep examples small and understandable. Repeat activities whenever needed. Use failed checks to understand what happened rather than trying to obtain a pass at any cost.

```text
Understand the action → Define the expected result → Automate
                     → Run → Investigate → Improve
```
