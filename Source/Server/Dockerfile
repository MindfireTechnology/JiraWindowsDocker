ARG JDKVERSION=11
ARG JDKBUILD=28_windows-x64
ARG JIRAVERSION=8.2.3

FROM mcr.microsoft.com/windows/servercore:ltsc2016 AS start
ARG JDKVERSION
ARG JDKBUILD
ARG JIRAVERSION

FROM start as jdk
ARG JDKVERSION
ARG JDKBUILD
ARG JIRAVERSION

WORKDIR /JDK
# We need to download & install the JDK
# Where to download the Jdk from
ADD ["https://download.java.net/openjdk/jdk${JDKVERSION}/ri/openjdk-${JDKVERSION}+${JDKBUILD}_bin.zip", "./openjdk.zip"]
RUN powershell Expand-Archive openjdk.zip -DestinationPath .

FROM start as jira
ARG JDKVERSION
ARG JDKBUILD
ARG JIRAVERSION
WORKDIR /Jira
# We need to download & install Jira
# Where to download Jira from
ADD ["https://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-software-${JIRAVERSION}.zip", "./jira.zip"]
RUN powershell Expand-Archive jira.zip -DestinationPath /Jira

FROM start as publish
ARG JDKVERSION
ARG JDKBUILD
ARG JIRAVERSION

COPY --from=jdk ["C:/JDK/jdk-${JDKVERSION}", "C:/JDK"]
COPY --from=jira ["C:/Jira/atlassian-jira-software-${JIRAVERSION}-standalone", "C:/Jira"]

ENV JRE_HOME=C:/JDK
ENV CATALINA_HOME=C:/Jira
ENV JAVA_HOME=C:/JDK
ENV JIRA_HOME=C:/JiraHome

WORKDIR C:/JiraHome

EXPOSE 8080

ENTRYPOINT ["C:/Jira/bin/start-jira.bat", "/fg"]