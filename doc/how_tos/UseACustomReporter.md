<a id="top"></a>

# How to Use A Custom Reporter

<!-- toc -->
<!-- endToc -->

This guide is for creating the ability to use a custom reporter that works on your machine.

For figuring out how to make a more robust custom reporter, that you might want to submit back to us as a Pull Request, check out [How to Submit a New Reporter to ApprovalTests](/doc/how_tos/SubmitANewReporterToApprovalTests.md#top).

Let's say that you really enjoy using Sublime Merge, and on your system it's located in `"/Applications/Sublime Merge.app/Contents/SharedSupport/bin/smerge"`

If you were to run this the command line, the full command would look this this:

<!-- snippet: CustomReporterTests.Creating_Custom_Reporters.approved.txt -->
<a id='snippet-CustomReporterTests.Creating_Custom_Reporters.approved.txt'></a>
```txt
"/Applications/Sublime Merge.app/Contents/SharedSupport/bin/smerge" mergetool --no-wait "test.received.txt" "test.approved.txt" -o "test.approved.txt" &
```
<sup><a href='/tests/DocTest_Tests/reporters/approval_tests/CustomReporterTests.Creating_Custom_Reporters.approved.txt#L1-L1' title='File snippet `CustomReporterTests.Creating_Custom_Reporters.approved.txt` was extracted from'>snippet source</a> | <a href='#snippet-CustomReporterTests.Creating_Custom_Reporters.approved.txt' title='Navigate to start of snippet `CustomReporterTests.Creating_Custom_Reporters.approved.txt`'>anchor</a></sup>
<!-- endSnippet -->

You can do this simply by creating a Reporter using:

<!-- snippet: use_custom_reporter -->
<a id='snippet-use_custom_reporter'></a>
```cpp
auto path = "/Applications/Sublime Merge.app/Contents/SharedSupport/bin/smerge";
auto arguments = "mergetool --no-wait {Received} {Approved} -o {Approved}";
auto reporter = CustomReporter::create(path, arguments);
```
<sup><a href='/tests/DocTest_Tests/reporters/CustomReporterTests.cpp#L9-L13' title='File snippet `use_custom_reporter` was extracted from'>snippet source</a> | <a href='#snippet-use_custom_reporter' title='Navigate to start of snippet `use_custom_reporter`'>anchor</a></sup>
<!-- endSnippet -->

By default, this will run in the background. Most of the time this is what you want.

However, you can force it to run in the foreground with:

<!-- snippet: use_custom_foreground_reporter -->
<a id='snippet-use_custom_foreground_reporter'></a>
```cpp
auto reporter = CustomReporter::createForegroundReporter(path, arguments);
```
<sup><a href='/tests/DocTest_Tests/reporters/CustomReporterTests.cpp#L39-L41' title='File snippet `use_custom_foreground_reporter` was extracted from'>snippet source</a> | <a href='#snippet-use_custom_foreground_reporter' title='Navigate to start of snippet `use_custom_foreground_reporter`'>anchor</a></sup>
<!-- endSnippet -->

On Windows, you can specify a search path for the installed location of a program with `{ProgramFiles}`.

<!-- snippet: use_custom_windows_reporter -->
<a id='snippet-use_custom_windows_reporter'></a>
```cpp
auto path = "{ProgramFiles}Beyond Compare 4\\BCompare.exe";
auto reporter = CustomReporter::create(path);
```
<sup><a href='/tests/DocTest_Tests/reporters/CustomReporterTests.cpp#L22-L25' title='File snippet `use_custom_windows_reporter` was extracted from'>snippet source</a> | <a href='#snippet-use_custom_windows_reporter' title='Navigate to start of snippet `use_custom_windows_reporter`'>anchor</a></sup>
<!-- endSnippet -->

See [Registering a default reporter](/doc/Reporters.md#registering-a-default-reporter) for wiring up this reporter as default, or you can dereference it and pass it in to individual `verify("text", *reporter)` method calls...

---

[Back to User Guide](/doc/README.md#top)