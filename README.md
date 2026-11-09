# Automated Testing Tools Practical

> A self-paced, hands-on introduction to browser automation for absolute beginners using Windows and Google Chrome or Microsoft Edge.

> [!NOTE]
> ## Educational Practice Materials
>
> This practical uses a public demonstration website. Use fictional task names only. Do not enter or share passwords, API keys, identification numbers, personal contact details or confidential information. Screenshots and traces may contain page content.

Learn automated testing by opening a task-list website, automating browser actions and checking the results.

No previous automated testing experience is needed. Complete Python examples are provided. If Python is also new to you, copy the examples and read the explanations beside them. You do not need to build a website, learn JavaScript or create an application server.

This is a learning practical, not an assessment. There are no marks, submissions, required reflections or evidence portfolios. Work independently at your own pace. Group coordination is not required.

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
| Playwright Trace Viewer | Look back through a test's actions and page snapshots. |
| Git, optional | Save versions of source files. |

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
> Chrome and Edge are both Chromium-based browsers. For pytest, `--browser chromium` selects the browser family, while `--browser-channel chrome` or `--browser-channel msedge` selects the installed browser.
>
> You do not need to download Playwright Chromium for the main Chrome or Edge tests. Do not leave out the channel when selecting an installed browser.

### Practical overview

| Item | Details |
| --- | --- |
| Operating system | Windows. |
| Working arrangement | Individual, self-directed practice. |
| Duration | Self-paced. Pause and return whenever needed. |
| Previous testing knowledge | None. |
| Python knowledge | Helpful, but complete examples are provided. |
| Main browser | Installed stable Google Chrome or Microsoft Edge. |
| Terminal | Windows Command Prompt inside VS Code. |
| Test website | [Playwright TodoMVC demonstration](https://demo.playwright.dev/todomvc/) |
| Assessment | None. No submission or written reflection. |

## Contents

1. [Learning goals](#1-learning-goals)
2. [Understand the workflow](#2-understand-the-workflow)
3. [Prepare your Windows computer](#3-prepare-your-windows-computer)
4. [Create the project and starting files](#4-create-the-project-and-starting-files)
5. [Prepare your Python environment](#5-prepare-your-python-environment)
6. [Choose your main browser](#6-choose-your-main-browser)
7. [Explore the website](#7-explore-the-website)
8. [Create your first automated check](#8-create-your-first-automated-check)
9. [Check task completion](#9-check-task-completion)
10. [Run one test with different inputs](#10-run-one-test-with-different-inputs)
11. [Record and replay browser actions](#11-record-and-replay-browser-actions)
12. [Create a results report](#12-create-a-results-report)
13. [Investigate a failed check](#13-investigate-a-failed-check)
14. [Troubleshooting and command reference](#14-troubleshooting-and-command-reference)
15. [Optional browsers and further practice](#15-optional-browsers-and-further-practice)

***

## 1. Learning goals

The activities introduce how to:

- Control Chrome or Edge using Playwright.
- Find an input or checkbox on a page.
- Distinguish actions from assertions.
- Check valid and invalid inputs.
- Run one test with several input values.
- Record and replay browser actions.
- Open an HTML results report.
- Use screenshots and traces to understand a failed check.

These goals describe what the guide teaches. There is no written assessment.

### Working through this practical

1. Follow the main sections in order.
2. Enter commands in the terminal.
3. Put Python code in the named `.py` file.
4. Save each file before running it.
5. Read the actual terminal result.
6. Use Section 14 when something differs from the description.

> [!IMPORTANT]
> Run commands from the project folder. Use its Python environment. Copy only the code inside code blocks, not the surrounding backticks or language labels.

Take breaks whenever needed. Setup and downloads may take longer than the test activities.

***

## 2. Understand the workflow

The website is the application you want to check. Playwright performs browser actions. pytest runs the tests. Assertions check the results.

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
| Browser channel | The installed Chrome or Edge browser selected for a run. |
| Headed | The browser window is visible. |
| Headless | The browser runs without displaying its window. |
| Report | A summary of test results. |
| Trace | A record for looking back through a run. |

### Actions and assertions

These actions enter and submit a task:

```python
task_input.fill("Read testing notes")
task_input.press("Enter")
```

This assertion checks the task text:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

These snippets explain the idea. Complete code follows later.

A script that only clicks and types may finish without checking that the correct task appeared.

### Positive and negative do not mean pass and fail

| Scenario | Expected behaviour | Passing outcome |
| --- | --- | --- |
| Add a normal task. | The task appears. | It appears with the correct text. |
| Submit an empty task. | No task is added. | The list stays empty. |

A negative test passes when invalid input is handled as expected.

> [!WARNING]
> Use small, deliberate practice runs. Do not run load tests, security scans or continuous repeated loops against the demonstration website.

***

## 3. Prepare your Windows computer

### 3.1 Install or check Python

Use Python 3.12 or 3.13 for this guide. Do not reinstall a suitable version if it is already available.

1. If needed, open [Python Downloads](https://www.python.org/downloads/).
2. Install Python for Windows.
3. Select `Add Python to PATH` if offered.
4. Close and reopen VS Code after installation.

You will check the installation in Section 4.

### 3.2 Install VS Code and its Python extension

1. Install [Visual Studio Code](https://code.visualstudio.com/) if needed.
2. Open VS Code.
3. Open Extensions.
4. Search for `Python`.
5. Install the extension published by Microsoft.

The extension does not install Python itself.

### 3.3 Choose Chrome or Edge

Use either installed stable Microsoft Edge or installed stable Google Chrome. You do not need both.

1. Open your chosen browser from the Windows Start menu.
2. Complete any first-run setup.
3. Confirm that you can open a website.

If installation is needed, use an approved installer:

- [Microsoft Edge](https://www.microsoft.com/edge/download)
- [Google Chrome](https://www.google.com/chrome/)

You do not need to sign in or connect a personal browser profile for this practical.

> [!NOTE]
> On managed computers, use the approved installation process. Ask IT support only when administrator access or system changes are required. Do not bypass computer policies. If one browser is unavailable, use the other approved browser.

***

## 4. Create the project and starting files

### 4.1 Create and open the project folder

1. Use Windows File Explorer to create `automated-testing-practice` where you can save files.
2. In VS Code, select File → Open Folder.
3. Open that folder.

### 4.2 Open Command Prompt in VS Code

Use Command Prompt throughout this guide to avoid PowerShell activation restrictions.

1. Select Terminal → New Terminal.
2. Find the dropdown beside the terminal's `+` button.
3. Select Command Prompt. If it is not listed, select Select Default Profile → Command Prompt, then open a new terminal.
4. Use the Command Prompt terminal for the following commands.

If you see a Python prompt beginning with `>>>`, enter `exit()` and press Enter first.

### 4.3 Check Python

```bat
python --version
```

If unavailable, try:

```bat
py -3 --version
```

You should see a Python version. If neither command works, reopen VS Code after installation and try again.

### 4.4 Create the starting structure

In VS Code's file explorer, right-click the project folder and use New File or New Folder to create:

```text
automated-testing-practice/
├── requirements.txt
├── pytest.ini
├── tests/
│   └── test_tasks.py
├── recordings/
└── reports/
```

### 4.5 Create `requirements.txt`

Paste and save:

```text
pytest-playwright
pytest-html
```

This lists the testing packages to install.

### 4.6 Create `pytest.ini`

Choose only one of the following configurations.

For Microsoft Edge:

```ini
[pytest]
testpaths = tests
addopts = -v --browser chromium --browser-channel msedge
```

For Google Chrome:

```ini
[pytest]
testpaths = tests
addopts = -v --browser chromium --browser-channel chrome
```

Save the file. Do not paste both configurations.

This tells pytest where the tests are, asks it to show test names, and selects your installed browser. The same test commands will now work with either choice.

Leave `tests/test_tasks.py` empty for now.

***

## 5. Prepare your Python environment

### 5.1 Create a virtual environment

In Command Prompt:

```bat
python -m venv .venv
```

If only the Windows launcher worked earlier, use this instead:

```bat
py -3 -m venv .venv
```

A virtual environment keeps this project's packages separate from other projects. A `.venv` folder should appear. The command may finish without a message.

### 5.2 Activate it

```bat
.venv\Scripts\activate.bat
```

Check the Python path:

```bat
python -c "import sys; print(sys.executable)"
```

The path should contain this project's `.venv\Scripts\python.exe`.

> [!TIP]
> If activation does not work, check that you are using Command Prompt. You can also replace `python` at the beginning of later commands with `.venv\Scripts\python.exe`. No security-policy change is needed.

### 5.3 Select the VS Code interpreter

1. Press Ctrl+Shift+P.
2. Search for `Python: Select Interpreter`.
3. Select the Python inside `.venv`.

The interpreter is the Python program that runs your code.

### 5.4 Install the packages

```bat
python -m pip install -r requirements.txt
```

Wait until the command finishes.

You do not need to run `python -m playwright install` for the main activities: they use your installed Chrome or Edge.

### 5.5 Check the tools

```bat
python -m pytest --version
python -m playwright --version
```

Each command should show a version number.

### Returning another day

Open the same folder, open Command Prompt and activate `.venv` again. You do not need to recreate the environment or reinstall packages each time.

***

## 6. Choose your main browser

Your browser choice is saved in `pytest.ini` from Section 4.6.

| Browser | Channel in `pytest.ini` |
| --- | --- |
| Microsoft Edge | `--browser-channel msedge` |
| Google Chrome | `--browser-channel chrome` |

The guided commands use that saved choice, so you do not need to repeat browser options each time.

To switch later, change only the channel value in `pytest.ini` and save it. Leave `--browser chromium` in place for both Chrome and Edge.

> [!IMPORTANT]
> Codegen is a separate command and does not read browser settings from `pytest.ini`. Section 11 provides separate recording commands for Chrome and Edge.
>
> The automated browser uses a separate session. It does not connect to your everyday signed-in browser profile.

***

## 7. Explore the website

### 7.1 Try the task list manually

In your chosen Chrome or Edge browser, open [Playwright TodoMVC](https://demo.playwright.dev/todomvc/).

1. Click `What needs to be done?`.
2. Enter `Read testing notes`.
3. Press Enter.
4. Find the new task.
5. Select its checkbox.
6. Try All, Active and Completed.

The tests will perform similar actions. You do not need to delete tasks from your usual browser before running tests.

### 7.2 Inspect the input

1. Right-click the task input and select Inspect.
2. Find the selected input in Developer Tools.
3. Look for `placeholder="What needs to be done?"`.
4. Close Developer Tools.

An attribute is extra information attached to a page element. The placeholder supplies the input's hint text. Playwright can use that text to find the input.

There is nothing to write or submit.

***

## 8. Create your first automated check

### 8.1 Paste the complete test

Open `tests/test_tasks.py`. Paste all of this code and save it. Keep the spaces at the start of lines inside the function.

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

### 8.2 Run the test

```bat
python -m pytest tests/test_tasks.py --headed --slowmo 300
```

### What you should see

Your selected Chrome or Edge opens, loads the website, adds the task and closes. If all checks succeed, the terminal reports `1 passed`.

Read the actual result. Use Section 14 if it differs.

| Option | What it does |
| --- | --- |
| `--headed` | Shows the browser. |
| `--slowmo 300` | Slows actions so you can watch them. |

The browser selection comes from `pytest.ini`.

### 8.3 Understand the code

| Code | Simple explanation |
| --- | --- |
| `from ... import ...` | Makes Playwright's tools available. |
| `URL = ...` | Stores the website address. |
| `def test_add_task(...)` | Defines a test. pytest looks for names starting with `test_`. |
| `page` | A browser page supplied by the Playwright pytest package. |
| `page: Page` | A type hint that helps the editor understand `page`. |
| `page.goto(URL)` | Opens the website. |
| `get_by_placeholder(...)` | Finds the task input by its hint text. |
| `exact=True` | Requires the whole hint text to match. |
| `locator(".todo-list li")` | Finds task rows using a CSS selector. |
| `task_items.locator("label")` | Finds task text inside those rows. |
| `fill(...)` | Replaces input text. |
| `press("Enter")` | Presses Enter in the input. |
| `expect(...)` | Starts a check. |
| `to_have_count(...)` | Checks the number of rows. |
| `to_have_text([...])` | Checks the task labels. |
| `to_have_value("")` | Checks that the input is empty. |

You can reuse the CSS selector without learning CSS first. Square brackets in the text assertion hold a list of expected labels.

Playwright's page assertions wait briefly for the expected condition. Do not add arbitrary pauses to make a test work.

***

## 9. Check task completion

### 9.1 Add another test

Paste this below the first test in the same file. Keep the existing code.

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

### 9.2 Run both tests

Save and run:

```bat
python -m pytest tests/test_tasks.py --headed
```

### What you should see

If both tests succeed, the terminal reports `2 passed`.

| New code | What it does |
| --- | --- |
| `first` | Selects the first task row. |
| `get_by_role("checkbox")` | Finds its checkbox. |
| `check()` | Selects the checkbox. |
| `to_be_checked()` | Checks that it is selected. |
| `get_by_role("link", name="Completed", exact=True)` | Finds the Completed link. |

Each test gets a fresh browser session. The second test creates its own task rather than relying on the first test.

***

## 10. Run one test with different inputs

### 10.1 Understand the expectation

An empty or spaces-only task should not be added. These negative tests pass when the list stays empty.

### 10.2 Add the import

Add `import pytest` at the top of the test file. Keep the other import, URL and tests.

```python
import pytest
from playwright.sync_api import Page, expect

URL = "https://demo.playwright.dev/todomvc/"
```

### 10.3 Add the test

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

The line starting with `@` tells pytest to run the function once per input. This is parametrization.

| Part | Meaning |
| --- | --- |
| `""` | No characters. |
| `" "` | One space. |
| `"   "` | Three spaces. |
| `task_text` | Receives the current input. |
| `ids` | Gives the runs readable names. |
| `task_text: str` | A type hint saying the input is text. |

### 10.4 Run the file

```bat
python -m pytest tests/test_tasks.py --headed
```

### What you should see

Two earlier tests plus three input cases produce five runs. If all succeed, the terminal reports `5 passed`.

These introductory examples do not cover every possible invalid input.

***

## 11. Record and replay browser actions

### 11.1 Start Codegen in your chosen browser

Check that the `recordings` folder exists. Run only the command matching your main browser.

Microsoft Edge:

```bat
python -m playwright codegen --channel msedge --target python-pytest -o recordings/recorded_task.py https://demo.playwright.dev/todomvc/
```

Google Chrome:

```bat
python -m playwright codegen --channel chrome --target python-pytest -o recordings/recorded_task.py https://demo.playwright.dev/todomvc/
```

> [!NOTE]
> Codegen uses `--channel`. pytest uses `--browser-channel`. These option names are different.

### 11.2 Record a short scenario

1. Enter `Try the recorder` in the recording browser.
2. Press Enter.
3. Find the text assertion control in the recording toolbar. Hover over controls to read their labels.
4. Select it, then select the new task's text.
5. Look for an `expect(...)` check in the generated code.
6. Close the recording windows to finish.

### 11.3 Add a check if needed

If no task-text check was recorded, open `recordings/recorded_task.py`. Inside its test function, after the action that presses Enter, add:

```python
expect(page.locator(".todo-list li label")).to_have_text(
    ["Try the recorder"]
)
```

Match the indentation of the function's other lines. If `expect` is not already imported, add this at the top:

```python
from playwright.sync_api import expect
```

### 11.4 Replay

Save and run from the project folder:

```bat
python -m pytest recordings/recorded_task.py --headed --slowmo 300
```

### What you should see

The recorded actions run in the browser selected in `pytest.ini`. The assertion checks the task text.

The recording is separate from the five cases in `tests/test_tasks.py`. A recording with only actions may finish without checking the intended result. Read the generated code before relying on it.

***

## 12. Create a results report

### 12.1 Generate the report

Check that the `reports` folder exists, then run:

```bat
python -m pytest tests/test_tasks.py --html=reports/results.html --self-contained-html
```

The selected Chrome or Edge runs without displaying a window because this command leaves out `--headed`.

### 12.2 Open the report

1. Open the project folder in Windows File Explorer.
2. Open `reports`.
3. Double-click `results.html` to open it in a browser.

The report shows test names, results, durations and errors. Expand a failed result to read more.

> [!NOTE]
> A report summarises a run. It does not prove that the tests cover everything the website can do. There is no separate report to write or submit.

***

## 13. Investigate a failed check

You will deliberately change an expectation to make one test fail. This demonstrates troubleshooting, not a confirmed website defect.

### 13.1 Change one expectation

In `test_add_task()`, change:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

temporarily to:

```python
expect(task_labels).to_have_text(["A different task"])
```

Do not change the input text in `task_input.fill(...)`.

### 13.2 Run that test with diagnostic output

```bat
python -m pytest tests/test_tasks.py::test_add_task --headed --screenshot only-on-failure --tracing retain-on-failure --output test-results/failure-demo
```

| Option | Purpose |
| --- | --- |
| `::test_add_task` | Run only that test function. |
| `--screenshot only-on-failure` | Save a screenshot if it fails. |
| `--tracing retain-on-failure` | Keep the failed run's trace. |
| `--output ...` | Choose the generated-output folder. |

### What you should see

The test fails: it enters `Read testing notes`, but expects `A different task`. Find the expected and actual text in the error.

Here, the expectation is deliberately wrong. The failure does not demonstrate a website defect.

### 13.3 Open the screenshot

In VS Code's file explorer, open `test-results/failure-demo`, then its generated test subfolder. Open the screenshot.

The test subfolder name is generated automatically. Find it rather than guessing it.

### 13.4 Open the trace

Find `trace.zip` in the same subfolder. Right-click it in VS Code and select Copy Relative Path.

Replace the placeholder with that path. Keep the quotation marks.

```bat
python -m playwright show-trace "PASTE_RELATIVE_PATH_HERE" --browser-channel msedge
```

The command above opens the viewer using installed Edge. To use installed Chrome, replace `msedge` with `chrome`.

Look through the page loading, text entry, Enter key and failed check. No screenshots of the viewer or written answers are required.

### 13.5 Restore and rerun

Restore:

```python
expect(task_labels).to_have_text(["Read testing notes"])
```

Save and run:

```bat
python -m pytest tests/test_tasks.py
```

If all checks succeed, the summary reports `5 passed`.

> [!IMPORTANT]
> Restore the meaningful check. Do not delete or skip the assertion to hide the failure.
>
> Later runs using the same output location may replace generated screenshots and traces. Copy a file elsewhere first only if you want to keep it for yourself.

***

## 14. Troubleshooting and command reference

### Before attempting a fix

1. Save the file.
2. Read the error message.
3. Check the project folder and Python path.
4. Check the channel in `pytest.ini`.
5. Preserve your files before making larger changes.

```bat
python -c "from pathlib import Path; import sys; print('Folder:', Path.cwd()); print('Python:', sys.executable)"
```

The folder should be `automated-testing-practice`. The Python path should contain `.venv`.

### Common problems

| Problem | What to try |
| --- | --- |
| Python is not recognised | Reopen VS Code. Try `py -3 --version`. Review installation if neither command works. |
| Packages cannot be imported | Activate `.venv`, check the Python path, then repeat `python -m pip install -r requirements.txt`. |
| Activation fails | Use Command Prompt and `.venv\Scripts\activate.bat`, not PowerShell. |
| Chrome cannot be found | Check stable Chrome opens from Start. If Edge is available instead, change the channel to `msedge`. |
| Edge cannot be found | Check stable Edge opens from Start. If Chrome is available instead, change the channel to `chrome`. |
| A Playwright Chromium executable is missing | For main tests, check that `pytest.ini` contains the Chrome or Edge channel. For recording, include `--channel chrome` or `--channel msedge`. You do not need to download Chromium to fix a missing channel. |
| Browser is blocked by policy | Use an approved alternative browser or the approved IT process. Do not bypass policy. |
| No tests are found | Save the file. Check it is `test_tasks.py`, not `test_tasks.py.txt`, and function names start with `test_`. |
| File cannot be found | Check the terminal is in the project folder and the filename matches. |
| `IndentationError` | Match the leading spaces. Use four spaces inside a function. Do not mix tabs and spaces. |
| `SyntaxError` | Check quotes, brackets and colons. Do not paste Markdown backticks into code. |
| Browser is not visible | Add `--headed`. |
| Browser closes quickly | Normal after a run. Use `--headed --slowmo 300`, then read the result. |
| Wrong browser opens | Check `pytest.ini`. For Codegen, check its `--channel` option separately. |
| Expected text differs | Compare spelling, capital letters and spaces in the input and assertion. |
| Website cannot load | Try the URL manually. Check the connection. If unavailable, save your work and retry later. |
| Locator times out | Check the website loaded and the locator matches the page. Use Inspect or Codegen to examine it. |
| Report has no screenshot | Open screenshots separately under `test-results`. |
| Generated files disappeared | Later runs may replace output. Copy files first if you want to keep them. |
| Downloads are blocked | Use approved network and software processes. Do not disable security controls. |

If a problem remains, keep your files and the full error message. Do not delete the project as the first troubleshooting step. Optional activities can wait.

### Main command reference

These pytest commands use Chrome or Edge from `pytest.ini`.

| Goal | Command |
| --- | --- |
| Watch the tests | `python -m pytest tests/test_tasks.py --headed --slowmo 300` |
| Run without showing the browser | `python -m pytest tests/test_tasks.py` |
| Run one test | `python -m pytest tests/test_tasks.py::test_add_task --headed` |
| Create a report | `python -m pytest tests/test_tasks.py --html=reports/results.html --self-contained-html` |
| Replay the recording | `python -m pytest recordings/recorded_task.py --headed --slowmo 300` |

***

## 15. Optional browsers and further practice

These activities are optional. There is no required number and nothing to submit.

### 15.1 Try the other main browser

If both Chrome and Edge are installed, change the channel in `pytest.ini` to the other browser, save and rerun:

```bat
python -m pytest tests/test_tasks.py --headed
```

Your Python code stays unchanged. Restore your preferred channel afterwards.

### 15.2 Try Playwright Chromium, Firefox or WebKit

These optional browsers need separate downloads. Ordinary Firefox does not replace Playwright's supported build. Playwright WebKit is not installed Safari.

> [!IMPORTANT]
> Your main `pytest.ini` includes a Chrome or Edge channel. The commands below override its `addopts` for that run, so a Chrome or Edge channel is not accidentally applied to another browser.

Playwright Chromium:

```bat
python -m playwright install chromium
python -m pytest tests/test_tasks.py -o "addopts=-v" --browser chromium --headed
```

Playwright Firefox:

```bat
python -m playwright install firefox
python -m pytest tests/test_tasks.py -o "addopts=-v" --browser firefox --headed
```

Playwright WebKit:

```bat
python -m playwright install webkit
python -m pytest tests/test_tasks.py -o "addopts=-v" --browser webkit --headed
```

If an optional browser is unsupported or blocked on your computer, skip it. Compare functional results, not browser speed. These small runs are not performance benchmarks.

After upgrading Playwright, reinstall any Playwright-managed browser you use. This does not mean reinstalling your ordinary Chrome or Edge.

### 15.3 Change a task name

In `test_add_task()`, replace `Read testing notes` with another fictional task name in both the input action and assertion. Save and rerun.

### 15.4 Add another input

Replace the parametrization block above the blank-input function with:

```python
@pytest.mark.parametrize(
    "task_text",
    ["", " ", "   ", "    "],
    ids=["empty", "one-space", "three-spaces", "four-spaces"],
)
```

Keep the function below it unchanged. There is one ID per input. Your file now runs six cases.

### 15.5 Use a helper to add two tasks

A helper is a function that performs reusable steps. Add both functions below to your existing test file. Keep its imports and URL.

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

Run your file again. This adds one test to the existing count. The helper performs actions; the test contains the checks.

### 15.6 Record another action

Try completing, editing or deleting a task manually. Record it in your main browser using Section 11. Read the code and reuse earlier assertions to check the result.

If expected behaviour is unclear, treat the result as an observation rather than a confirmed defect.

### 15.7 Save source files with Git

Git is not needed for the main activities. Your local project folder is enough.

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

Keep source and configuration files. Do not share private data or generated traces. Review files before uploading.

Group branches, pull requests, contribution records, evidence portfolios and reflections are not required.

***

## Closing reminder

A passing test means its particular checks succeeded in that run. It does not prove that the whole website is error-free.

Keep examples small and understandable. Repeat activities whenever needed. Use failures to understand what happened, rather than trying to obtain a pass at any cost.

```text
Understand the action → Define the expected result → Automate
                     → Run → Investigate → Improve
```
