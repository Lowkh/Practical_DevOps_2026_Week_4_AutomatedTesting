# Learn Automated Testing: A Self-Paced Practical

A step-by-step introduction using Python, Playwright and pytest.

## About this guide

You will use a browser to test a demonstration task-list website. You do not need to build a website or application server.

This is a learning practical, not an assessment. There are no marks, submissions, required reflections or evidence portfolios. You can repeat activities and take breaks whenever you need them.

Start with one browser: Chromium. Other browsers and Git are optional later activities.

### What you need to know first

You do not need previous automated testing experience. This guide provides complete test code for you to copy.

Some Python code is used. You do not need to memorise it. If Python is also new to you, read the explanations after each example and change only the lines the guide identifies.

### What you will do

1. Set up the tools.
2. Try the website by hand.
3. Run your first automated test.
4. Add another test.
5. Try several inputs with one test.
6. Record browser actions.
7. Read a report and investigate a failed check.
8. Try optional activities when you are ready.

Work at your own pace. Setup and downloads may take longer than the activities themselves. You do not need to finish everything in one sitting.

### Use safe practice data

Use fictional task names such as `Read testing notes`.

Do not enter passwords, personal details, API keys or confidential information. Screenshots and traces can contain page content.

Use this demonstration site only for the small practice runs in this guide. Do not run load tests, security scans or continuous loops against it.

---

## 1. Meet the tools

| Tool | Simple explanation |
| --- | --- |
| Python | Runs the code you write. |
| VS Code | An editor for creating and changing files. |
| Terminal | A window where you type commands. |
| Playwright | Opens a browser and performs actions such as typing and clicking. |
| pytest | Finds your tests, runs them and displays the results. |
| Chromium | The browser used for the main activities. |
| Codegen | A Playwright tool that records browser actions and creates code. |
| HTML report | A results page you can open in a browser. |
| Trace Viewer | A tool for looking back through the actions in a test run. |

An automated test usually follows this pattern:

```text
Open a page → Perform an action → Check the result
```

An action does something. An assertion checks something.

For example:

- Typing a task is an action.
- Checking that the task appears is an assertion.

---

## 2. Set up your computer

Complete this section once for this project.

When you return another day, use Section 3 instead.

### 2.1 Install Python and VS Code

If they are already installed, do not reinstall them.

- Python: https://www.python.org/downloads/
- VS Code: https://code.visualstudio.com/

Use Python 3.12 or 3.13 for this guide.

On Windows, select `Add Python to PATH` if the installer offers it.

Close and reopen VS Code after installation.

In VS Code:

1. Open Extensions.
2. Search for `Python`.
3. Install the extension published by Microsoft.

This extension helps the editor work with Python. It does not install Python itself.

On a managed computer, use the approved software installation method. If installation requires administrator access, ask your IT support team to install the missing software. Do not bypass computer policies.

### 2.2 Create and open a project folder

1. Create a folder named `automated-testing-practice` in a location where you can save files.
2. Open VS Code.
3. Select File → Open Folder.
4. Open `automated-testing-practice`.
5. Select Terminal → New Terminal.

Keep this folder open throughout the practical.

Commands go in the terminal.

Python code goes in a `.py` file.

Do not type commands at a Python `>>>` prompt. If you see `>>>`, type `exit()` and press Enter first.

### 2.3 Check Python

On Windows, enter:

```powershell
python --version
```

If that does not work, try:

```powershell
py -3 --version
```

On macOS or Linux, enter:

```bash
python3 --version
```

You should see a Python version.

If the command is not found, reopen the terminal after installing Python and try again.

### 2.4 Create a virtual environment

A virtual environment keeps this project's Python packages separate from other projects.

Run only the command for your computer.

Windows:

```powershell
python -m venv .venv
```

If you used the Windows launcher in the previous step:

```powershell
py -3 -m venv .venv
```

macOS or Linux:

```bash
python3 -m venv .venv
```

You should now have a `.venv` folder.

The command may finish without displaying a message.

If Linux reports that virtual-environment support is missing, use your approved software installation process or ask IT support to install it. Do not replace the system Python installation.

### 2.5 Activate the environment

Look at the terminal name and use the matching command.

Do not run all of them.

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Windows Command Prompt:

```bat
.venv\Scripts\activate.bat
```

Windows Git Bash:

```bash
source .venv/Scripts/activate
```

macOS or Linux:

```bash
source .venv/bin/activate
```

Check which Python you are using:

```bash
python -c "import sys; print(sys.executable)"
```

The displayed path should contain this project's `.venv` folder.

#### If PowerShell blocks activation

You do not need to change its security settings.

In VS Code:

1. Find the dropdown beside the terminal's `+` button.
2. Open Command Prompt.
3. Use the Command Prompt activation command above.

Alternatively, run the virtual environment's Python directly.

Replace `python` at the start of later commands with:

- PowerShell: `.\.venv\Scripts\python.exe`
- macOS or Linux: `./.venv/bin/python`

For example, in PowerShell:

```powershell
.\.venv\Scripts\python.exe -m pip install pytest-playwright pytest-html
```

### 2.6 Select Python in VS Code

1. Press Ctrl+Shift+P on Windows/Linux or Cmd+Shift+P on macOS.
2. Search for `Python: Select Interpreter`.
3. Choose the Python inside your project's `.venv` folder.

The interpreter is the Python program that runs your code.

### 2.7 Install the testing tools

In the terminal, run these commands one at a time.

Wait for each command to finish.

```bash
python -m pip install pytest-playwright pytest-html
```

```bash
python -m playwright install chromium
```

The first command installs the Python testing packages.

The second downloads the browser used by Playwright. An ordinary Chrome installation does not replace this download.

If a download fails, check your internet connection and retry the same command.

On a managed network, use approved network settings rather than disabling security controls.

### 2.8 Create the starting files

Use VS Code's file explorer to create this structure inside your project:

```text
automated-testing-practice/
├── .venv/
├── pytest.ini
└── tests/
    └── test_tasks.py
```

The `.venv` folder already exists.

Create the `tests` folder and the two files yourself.

To create a folder or file in VS Code, right-click the project folder in the file explorer and select New Folder or New File.

In `pytest.ini`, paste:

```ini
[pytest]
testpaths = tests
addopts = -v
```

Save the file.

This tells pytest where the tests are and asks it to show each test's name.

Leave `test_tasks.py` empty for now.

---

## 3. Returning to the practical

When you reopen the project:

1. Open the same project folder in VS Code.
2. Open a terminal.
3. Activate `.venv` using Section 2.5.
4. Check the Python path with the command in that section.
5. Continue with your next activity.

You do not need to create the environment or download Chromium again unless the environment has been removed or Playwright has been updated.

---

## 4. Try the website yourself

Open this website in your usual browser:

https://demo.playwright.dev/todomvc/

1. Click the box labelled `What needs to be done?`.
2. Type `Read testing notes`.
3. Press Enter.
4. Find the task in the list.
5. Select its checkbox to mark it complete.
6. Try the All, Active and Completed links.

The automated tests will perform similar actions.

Your usual browser and the browser opened by the tests use separate sessions.

You do not need to delete the tasks in your usual browser before running the tests.

---

## 5. Run your first automated test

### 5.1 Paste the complete code

Open `tests/test_tasks.py`.

Paste all of the following code and save it.

Keep the spaces at the beginning of the indented lines.

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

    expect(task_labels).to_have_text(
        ["Read testing notes"]
    )

    expect(task_input).to_have_value("")
```

### 5.2 Run the test

In the terminal, enter:

```bash
python -m pytest tests/test_tasks.py --browser chromium --headed --slowmo 300
```

You should see:

1. A browser opens.
2. The task-list website loads.
3. A task appears.
4. The browser closes.

The terminal should report `1 passed` if all checks succeed.

Do not type this result yourself. Read what the terminal actually reports.

| Command option | What it does |
| --- | --- |
| `--browser chromium` | Selects Chromium. |
| `--headed` | Makes the browser visible. |
| `--slowmo 300` | Slows browser actions so you can watch them. |

A browser closing after the test is normal.

If the result differs, use Section 11.

### 5.3 Understand the code

| Code | What it does |
| --- | --- |
| `from ... import ...` | Makes Playwright's tools available in the file. |
| `URL = ...` | Stores the website address. |
| `def test_add_task(...)` | Defines a test. pytest looks for names beginning with `test_`. |
| `page` | A browser page supplied by the pytest Playwright package. |
| `page: Page` | A type hint that helps the editor understand what `page` is. |
| `page.goto(URL)` | Opens the website. |
| `get_by_placeholder(...)` | Finds the input by its displayed hint text. |
| `page.locator(".todo-list li")` | Finds task rows inside the task list. |
| `task_items.locator("label")` | Finds the task text inside those rows. |
| `fill(...)` | Replaces the input's text. |
| `press("Enter")` | Presses the Enter key in the input. |
| `expect(...)` | Starts a check. |
| `to_have_count(1)` | Checks that there is exactly one matching item. |
| `to_have_text([...])` | Checks the displayed task text. |
| `to_have_value("")` | Checks that the input is empty. |

A locator tells Playwright which part of the page to use.

The expression `.todo-list li` is a CSS selector. In this example, it identifies the task rows. You can reuse it without learning CSS selectors first.

In `to_have_text(["Read testing notes"])`, the square brackets contain a list of expected task labels.

Playwright's checks wait briefly for the expected page condition. You do not need to add your own pauses between these steps.

---

## 6. Check task completion

Add this code below the first test in the same file.

Do not replace the existing code.

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

    page.get_by_role(
        "link",
        name="Completed",
        exact=True,
    ).click()

    expect(task_items).to_have_count(1)

    expect(task_items.locator("label")).to_have_text(
        ["Practise automated testing"]
    )
```

Save and run:

```bash
python -m pytest tests/test_tasks.py --browser chromium --headed
```

If both tests succeed, the summary reports `2 passed`.

### What the new code does

- `first` selects the first task row.
- `get_by_role("checkbox")` finds its checkbox.
- `check()` selects the checkbox.
- `to_be_checked()` checks that it is selected.
- Clicking Completed shows completed tasks.
- The final checks confirm that the completed task appears.

Each test receives a fresh browser session.

The second test creates its own task rather than using a task left by the first test.

---

## 7. Try several inputs with one test

A valid task name should create a task.

An empty or spaces-only entry should not create one.

A test of invalid input is often called a negative test. It passes when the website handles the invalid input as expected.

“Negative” does not mean the test must fail.

### 7.1 Add an import

At the very top of `tests/test_tasks.py`, add:

```python
import pytest
```

Keep the existing import, URL and tests.

The top of your file should now look like this:

```python
import pytest
from playwright.sync_api import Page, expect

URL = "https://demo.playwright.dev/todomvc/"
```

### 7.2 Add the new test

At the bottom of the same file, paste:

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

The line beginning with `@` tells pytest to run the function once for each supplied input.

This is called parametrization.

| Part | Meaning |
| --- | --- |
| `""` | An empty string: no characters. |
| `" "` | A string containing one space. |
| `"   "` | A string containing three spaces. |
| `task_text` | Receives the input for the current run. |
| `ids` | Gives each run a readable name. |

### 7.3 Run the tests

Save and run:

```bash
python -m pytest tests/test_tasks.py --browser chromium --headed
```

Your file now runs:

- One add-task test.
- One completion test.
- Three blank-input cases.

That produces five test runs.

If they all succeed, the summary reports `5 passed`.

These introductory checks do not prove that every possible invalid input is handled correctly.

---

## 8. Record browser actions

Codegen can help you create starting code.

You still need to read the code and decide what results it should check.

### 8.1 Create a recording folder

In VS Code, create a folder named `recordings` beside `tests`.

Your project now includes:

```text
automated-testing-practice/
├── .venv/
├── pytest.ini
├── recordings/
└── tests/
    └── test_tasks.py
```

### 8.2 Start the recorder

In the terminal, run:

```bash
python -m playwright codegen --target python-pytest -o recordings/recorded_task.py https://demo.playwright.dev/todomvc/
```

A browser and recording controls should open.

1. In the recording browser, enter `Try the recorder` in the task input.
2. Press Enter.
3. Look for the text assertion control in the recording toolbar.
4. Hover over controls to read their labels.
5. Select the text assertion control, then select the new task's text.
6. Inspect the generated code for an `expect(...)` check.
7. Close the recording windows to finish.

If you cannot find the assertion control, you can still replay the recorded actions.

To add a check yourself, open `recordings/recorded_task.py`. Inside its test function, after the recorded action that presses Enter, add:

```python
expect(page.locator(".todo-list li label")).to_have_text(
    ["Try the recorder"]
)
```

Keep the same indentation as the other lines inside that function.

The file also needs this import at the top:

```python
from playwright.sync_api import expect
```

If `expect` is already included in an existing import, do not add it again.

### 8.3 Replay the recording

Save the file and run:

```bash
python -m pytest recordings/recorded_task.py --browser chromium --headed --slowmo 300
```

This command explicitly selects the recording file.

It does not add the recording to the five cases in `tests/test_tasks.py`.

If the recording has only actions, it may run successfully without checking that the correct task appeared.

Successful actions and a meaningful check are not the same thing.

---

## 9. Open a results report

Create a folder named `reports` beside `tests`.

Then run:

```bash
python -m pytest tests/test_tasks.py --browser chromium --html=reports/results.html --self-contained-html
```

This command does not show the browser because it leaves out `--headed`.

The tests still run.

Find `reports/results.html` in your project folder.

Open it in your usual browser. For example, locate it in File Explorer or Finder and double-click it.

The report shows:

- Test names.
- Results.
- Time taken.
- Error details for failed tests.

Expand a failed result to read its details.

A report summarises a run. It does not guarantee that the tests cover everything the website can do.

You do not need to write a separate report or submit this file.

---

## 10. Understand a failed check

A failed test is information to investigate.

It does not automatically mean the website is broken.

In this activity, you will deliberately give one check the wrong expected text.

### 10.1 Change only one check

In `test_add_task()`, find:

```python
expect(task_labels).to_have_text(
    ["Read testing notes"]
)
```

Temporarily change it to:

```python
expect(task_labels).to_have_text(
    ["A different task"]
)
```

Do not change:

```python
task_input.fill("Read testing notes")
```

### 10.2 Run just this test

Save, then run:

```bash
python -m pytest tests/test_tasks.py::test_add_task --browser chromium --headed --screenshot only-on-failure --tracing retain-on-failure --output test-results/failure-demo
```

The `::test_add_task` part selects that one function.

The other options save information to help you investigate:

| Option | What it does |
| --- | --- |
| `--screenshot only-on-failure` | Saves a screenshot when the test fails. |
| `--tracing retain-on-failure` | Keeps a trace when the test fails. |
| `--output test-results/failure-demo` | Chooses where to save these files. |

This run should fail.

The test enters `Read testing notes`, but its check expects `A different task`.

Read the terminal error. Find the expected text and the actual text.

Here, the problem is the deliberately incorrect test expectation. This is not a demonstrated website defect.

### 10.3 Open the screenshot

In VS Code's file explorer:

1. Open `test-results`.
2. Open `failure-demo`.
3. Open the generated test subfolder.
4. Find and open the screenshot.

The exact subfolder name is generated automatically.

Use the file explorer rather than guessing it.

The screenshot shows the page at failure. It helps you see what happened, but it does not replace reading the failed assertion.

### 10.4 Open the trace

In the same test subfolder, find `trace.zip`.

In VS Code:

1. Right-click `trace.zip`.
2. Select Copy Relative Path.
3. Use that path in the following command.

Replace `PASTE_RELATIVE_PATH_HERE` with the copied path. Keep the quotation marks.

```bash
python -m playwright show-trace "PASTE_RELATIVE_PATH_HERE"
```

In Trace Viewer, select actions in order.

Look at:

- The page opening.
- The text being entered.
- The Enter key being pressed.
- The failed check.

A trace lets you look back through the test.

You do not need to save screenshots of the viewer or write answers to questions.

### 10.5 Restore the correct check

Change the expected text back to:

```python
expect(task_labels).to_have_text(
    ["Read testing notes"]
)
```

Save and run the full test file again:

```bash
python -m pytest tests/test_tasks.py --browser chromium
```

If all checks succeed, the summary reports `5 passed` again.

Do not remove the assertion simply to make the failure disappear.

Restore the check that matches the intended behaviour.

Generated screenshots and traces may be replaced by later runs using the same output location. Copy a file elsewhere first only if you want to keep it for your own reference.

---

## 11. Solve common problems

Start with these checks:

1. Save the file you changed.
2. Make sure VS Code has opened `automated-testing-practice`, not only its `tests` subfolder.
3. Make sure the terminal is in that project folder.
4. Check that Python comes from `.venv`.
5. Read the first useful error message before rerunning.

This command displays your current folder and Python location:

```bash
python -c "from pathlib import Path; import sys; print('Folder:', Path.cwd()); print('Python:', sys.executable)"
```

| What you see | What to try |
| --- | --- |
| `python` is not recognised | Reopen the terminal. On Windows, try `py -3 --version`. Follow Section 2 again if Python is missing. |
| `No module named pytest` or `playwright` | Check the Python path. Activate `.venv`, then repeat the package installation command in Section 2.7. |
| Browser executable is missing | Run `python -m playwright install chromium`. |
| PowerShell blocks activation | Use Command Prompt or the direct Python path in Section 2.5. Do not weaken security settings. |
| `no tests ran` | Check that the file is saved as `tests/test_tasks.py`, not `test_tasks.py.txt`. Test function names must start with `test_`. |
| File or folder not found | Check the project folder, spelling and selected path. Create the folder if the guide asks for it. |
| `IndentationError` | Compare the leading spaces with the example. Use four spaces inside a test function. Do not mix tabs and spaces. |
| `SyntaxError` | Check quotation marks, brackets and colons. Copy plain code without the surrounding Markdown backticks. |
| Browser opens and closes quickly | This is normal after a run. Add `--headed --slowmo 300` to watch actions, then read the terminal result. |
| A check reports different text | Compare the entered text with the expected text, including spelling, capital letters and spaces. |
| The page cannot load | Open the demo URL in your usual browser. Check the connection. If the site is unavailable, save your work and retry later. |
| A locator times out | Check that the site loaded and the locator text matches the page. Use the recorder or browser Inspect tool to examine the current page. |
| A report has no screenshot | The HTML report and Playwright screenshots are separate outputs in this guide. Open the screenshot under `test-results`. |
| A download or browser is blocked by policy | Use the approved software or network process. Do not bypass the restriction. Other optional browsers can wait. |
| Linux reports missing browser libraries | Use an approved supported environment or ask IT support to install the required system dependencies. |

### If Playwright was upgraded

Download its matching Chromium build again:

```bash
python -m playwright install chromium
```

### If a problem remains

Keep your files and the full error message.

Do not delete your project as a first troubleshooting step.

If one optional activity is blocked, you can leave it and continue with activities that use your working setup.

---

## 12. Optional: try another browser

You can stop after the main activities.

Try this section only when you are comfortable running your existing tests.

You do not need all browsers installed. Choose one available option.

### Firefox

Install Playwright's Firefox build:

```bash
python -m playwright install firefox
```

Run the same tests:

```bash
python -m pytest tests/test_tasks.py --browser firefox --headed
```

An ordinary Firefox installation does not replace Playwright's supported build.

### WebKit

Install Playwright's WebKit build:

```bash
python -m playwright install webkit
```

Run:

```bash
python -m pytest tests/test_tasks.py --browser webkit --headed
```

WebKit here is Playwright's browser build.

This is not a test in the installed Safari application.

If system dependencies are unavailable, skip this option rather than changing system settings without permission.

### Installed Google Chrome

If stable Google Chrome is already installed:

```bash
python -m pytest tests/test_tasks.py --browser chromium --browser-channel chrome --headed
```

### Installed Microsoft Edge

If stable Microsoft Edge is already installed:

```bash
python -m pytest tests/test_tasks.py --browser chromium --browser-channel msedge --headed
```

The channel selects an installed Chrome or Edge browser.

Use these channels only with `--browser chromium`, not with Firefox or WebKit.

The Python tests stay the same. Only the run command changes.

Compare whether the checks produce the same outcomes.

These small runs are not browser-speed benchmarks.

---

## 13. Optional: make one small change

These are practice ideas, not assessment tasks.

There is no required number to complete.

### Change the task name

In `test_add_task()`, change `Read testing notes` to another fictional task name in both places:

1. The input action.
2. The text assertion.

Save and rerun.

### Add another blank-input case

In the parametrized test:

1. Add a string containing four spaces to the input list.
2. Add `"four-spaces"` to `ids`.

Keep one ID for each input.

The updated part looks like this:

```python
@pytest.mark.parametrize(
    "task_text",
    ["", " ", "   ", "    "],
    ids=["empty", "one-space", "three-spaces", "four-spaces"],
)
```

Keep the test function below it unchanged.

Rerun the file. It now has six cases.

### Try recording another action

Start a new recording and try completing a task.

Read the generated checkbox action and compare it with Section 6.

Add a check for the checkbox state if it is missing.

### Explore editing or deleting

Try the action manually first.

Record it with Codegen, then inspect the generated code.

Reuse earlier assertions to check the changed task text or the remaining task count.

If you are not sure what the website is meant to do, treat the result as an observation rather than deciding that it is a defect.

---

## 14. Optional: save your work with Git

Git is not needed to learn the main testing activities.

You can keep your local project folder as your practice workspace.

If you already use Git, create `.gitignore` in the project folder before adding files:

```gitignore
.venv/
__pycache__/
.pytest_cache/
test-results/
reports/
recordings/
.env
```

Keep test source files and configuration files.

Do not upload virtual environments, private data or generated browser traces.

Review what you are sharing before pushing to a remote repository.

Group branches, pull requests, contribution records and written reflections are not required for this practical.

---

## Quick command reference

Run these from the project folder using its virtual environment.

### Watch your tests

```bash
python -m pytest tests/test_tasks.py --browser chromium --headed --slowmo 300
```

### Run without showing the browser

```bash
python -m pytest tests/test_tasks.py --browser chromium
```

### Run the add-task test only

```bash
python -m pytest tests/test_tasks.py::test_add_task --browser chromium --headed
```

### Create a report

Create the `reports` folder first if it does not exist.

```bash
python -m pytest tests/test_tasks.py --browser chromium --html=reports/results.html --self-contained-html
```

### Start recording

Create the `recordings` folder first if it does not exist.

```bash
python -m playwright codegen --target python-pytest -o recordings/recorded_task.py https://demo.playwright.dev/todomvc/
```

### Replay your recording

```bash
python -m pytest recordings/recorded_task.py --browser chromium --headed --slowmo 300
```

---

## Closing note

You have practised:

- Opening a page.
- Performing browser actions.
- Checking results.
- Trying several inputs.
- Recording actions.
- Reading results.
- Investigating a failure.

A passing test means its particular checks succeeded in that run.

It does not prove that the whole website is error-free.

Keep your examples small and understandable. Repeat an activity whenever you need to, and use failed checks to understand what happened.
