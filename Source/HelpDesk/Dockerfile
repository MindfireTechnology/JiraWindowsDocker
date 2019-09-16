ARG JIRAVERSION=4.2.3-x64
ARG JDKBUILD=28_windows-x64
ARG JDKVERSION=11

FROM mcr.microsoft.com/windows/servercore:ltsc2016 AS start
ARG JIRAVERSION
ARG JDKBUILD
ARG JDKVERSION

# ----------------- JDK -------------------
FROM start AS jdk
ARG JIRAVERSION
ARG JDKBUILD
ARG JDKVERSION

WORKDIR /Downloads
ADD ["https://download.java.net/openjdk/jdk${JDKVERSION}/ri/openjdk-${JDKVERSION}+${JDKBUILD}_bin.zip", "./openjdk.zip"]
RUN powershell Expand-Archive openjdk.zip -DestinationPath /JDK

# ---------------- JIRA --------------------
FROM start as jira
ARG JIRAVERSION
ARG JDKBUILD
ARG JDKVERSION

ADD ["https://www.atlassian.com/software/jira/downloads/binary/atlassian-servicedesk-${JIRAVERSION}.exe", "./servicedesk.exe"]
RUN servicedesk.exe -q -dir C:\ServiceDesk

# --------------- PUBLISH -------------------
FROM start as publish
ARG JIRAVERSION
ARG JDKBUILD
ARG JDKVERSION

ENV JAVA_HOME=C:/JDK
ENV JRE_HOME=C:/JDK
ENV CATALINA_HOME=C:/ServiceDesk
ENV JIRA_HOME=C:/data/JiraHome

COPY --from=jdk ["C:/JDK/jdk-${JDKVERSION}", "C:/JDK"]
COPY --from=jira ["C:/ServiceDesk", "C:/ServiceDesk"]

WORKDIR /data/JiraHome

EXPOSE 8080

ENTRYPOINT [ "C:/ServiceDesk/bin/start-jira.bat", "/fg" ]