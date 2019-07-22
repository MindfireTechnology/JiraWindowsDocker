# JiraWindowsDocker
Jira on Windows Docker

## JDK
The JDK is added to the container dynamically, but you _must_ include the version to be used. This can be done either with the `build` command, or through a `docker-compose.yml` file. The arg is JDKVERSION and is downloaded from the OpenJDK website. Use the full version name (e.g. 11+28_windows-x64).

## Jira
The Jira installer is also added dynamically, and you _must_ include the version to be used. As with the JDK, this can be done with either the `build` command or through a `docker-compose.yml` file. The arg is JIRAVERSION, and must be a complete version number (e.g. 8.2.3)