Reporting Issues with pfSense Software
======================================

This page serves as a guide for providing legitimate bug reports with
pfSense® software. Most of the bug reports from outside users are not
bugs at all, simply misconfigurations. Or alternatively, do not contain
nearly enough information for a developer to replicate the problem. If
a bug report does not contain the appropriate information to verify a
legitimate bug, it will be rejected.

.. attention:: The |issue_tracker| site is not a discussion platform and is
   never to be used for support issues.

Unless a precise and specific description of the problem is noted, including
which portion(s) of the underlying system are causing problems/misconfigured and
how, first inquire about the problem using one of our available support
resources. If/when a specific bug is found, a bug ticket can be opened.

An example of an invalid bug report is "XYZ doesn't work!" without appropriate
accompanying detail. An alternative, to make that a legitimate bug report, is
"XYZ doesn't work, because the underlying xyz.conf has option1=1 where it should
be option1=5 when I check box A on thispage.php in the web interface".

.. seealso:: `How to report bugs effectively`_.

Where to submit
---------------

For anything that is not a confirmed, specific, detailed bug report, post to the
|forum_link| or |subreddit| first. Those sites are platforms where the problem
can be discussed and the specifics required to replicate the issue can be
identified.

After discussion and confirmation of a specific, legitimate bug report
on the forum or pfSense subreddit, please open a ticket in the |issue_tracker|.

.. attention:: The |issue_tracker| site is not a discussion platform and is
   never to be used for support issues.

What to Include
---------------

When submitting a bug report to the |issue_tracker| site, fill out the report
completely and include enough supporting information to reproduce the issue.

Use the following guidelines when completing the issue report.

File issues with the base system under `pfSense`_ and issues with packages
belong under `pfSense Packages`_.

.. note:: Not all fields will be available to all users.

:Tracker: Use the appropriate issue tracker type, following these guidelines:

  :Bug: Problems, unexpected behavior, crashes, or when the other categories do
    not apply.
  :Feature: Feature requests or changes in (working) behavior.
  :Todo: Tasks or work that need to be completed that are not specifically bugs
    or features.

:Subject: A brief but complete and accurate description of the problem. If the
  problem is specific to one page or file, prefix the subject with that page
  filename.

  Example: ``services_rfc2136_edit.php: Save and Force Update button does not
  perform any action``

:Description: A full description of the problem. Include any relevant detail,
  supporting evidence such as log entries, and if possible a complete recount of
  how to reproduce the bug that includes every necessary step.

  .. warning:: **Information in this issue tracker is public!** Do not include
     any personal information such as usernames, e-mail addresses, IP addresses,
     and so on. If developers require that information they will request it
     privately.

  * Please use appropriate formatting, such as <pre> tags around log data or
    command output.
  * Files may also be attached, such as logs or crash dumps. Check for personal
    data before attaching files and obfuscate/mask info as needed.

:Status: Leave this as *New*.

:Priority: Leave this as *Normal* or set lower for minor issues. **Higher
  priorities will be set by developers only when appropriate**.

:Assignee: Leave this **empty** unless directed by a developer to assign it to
  them directly.

:Category: Pick the closest relevant category for the issue, if possible, or a
  generic category such as "Web Interface" for GUI issues and "Operating System"
  for OS-level issues.

:Target Version: Leave this **empty** unless directed by a developer to assign a
  specific target. **Developers will assign a target version after evaluating
  the issue.**

:Affected Version: Pick the version number of the firewall experiencing the
  issue.

:Affected Architecture: Pick *All* unless the issue is known to only affect a
  single architecture.

Leave other fields blank.

.. _How to report bugs effectively: http://www.chiark.greenend.org.uk/~sgtatham/bugs.html
.. _pfSense: https://redmine.pfsense.org/projects/pfsense
.. _pfSense Packages: https://redmine.pfsense.org/projects/pfsense-packages
