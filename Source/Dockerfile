FROM mcr.microsoft.com/windows/servercore:ltsc2016 AS start
ARG JDKVERSION
ARG JIRAVERSION

WORKDIR /JDK
# We need to download & install the JDK
# Where to download the Jdk from
ADD ["https://download.java.net/openjdk/jdk11/ri/openjdk-${JDKVERSION}_bin.zip", "./openjdk.zip"]
#COPY Downloads/openjdk-11+28_windows-x64_bin.zip .
RUN powershell Expand-Archive openjdk.zip -DestinationPath /JDK
RUN powershell Remove-Item -Force openjdk.zip
#COPY Downloads/JDK .
ENV JAVA_HOME=C:/JDK

WORKDIR /Jira
# We need to download & install Jira
# Where to download Jira from
ADD ["https://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-software-${JIRAVERSION}.zip", "./jira.zip"]
#COPY Downloads/atlassian-jira-software-8.2.3.zip .
RUN powershell Expand-Archive jira.zip -DestinationPath /Jira
RUN powershell Remove-Item -Force jira.zip
# COPY Downloads/Jira .
ENV JRE_HOME=C:/JDK
ENV CATALINA_HOME=C:/Jira

WORKDIR C:/JiraHome
ENV JIRA_HOME=C:/JiraHome

ENTRYPOINT ["C:/Jira/bin/start-jira.bat", "/fg"]
