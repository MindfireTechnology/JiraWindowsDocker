
FROM mcr.microsoft.com/windows/servercore:ltsc2016

# We need to download & install the JDK
#WORKDIR /Downloads
# Where to download the Jdk from
#ADD https://download.java.net/openjdk/jdk11/ri/openjdk-11+28_windows-x64_bin.zip .
#COPY Downloads/openjdk-11+28_windows-x64_bin.zip .
#RUN powershell Expand-Archive -LiteralPath ./openjdk-11+28_windows-x64_bin.zip -DestinationPath C:/JDK/
WORKDIR /JDK
COPY Downloads/JDK .
ENV JAVA_HOME=C:/JDK

# We need to download & install Jira
# Where to download Jira from
#ADD https://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-software-8.2.3.zip .
#COPY Downloads/atlassian-jira-software-8.2.3.zip .
#RUN powershell Expand-Archive -LiteralPath ./atlassian-jira-software-8.2.3.zip -DestinationPath C:/Jira/
WORKDIR /Jira
COPY Downloads/Jira .
ENV JRE_HOME=C:/JDK
ENV CATALINA_HOME=C:/Jira

WORKDIR C:/JiraHome
ENV JIRA_HOME=C:/JiraHome

ENTRYPOINT ["C:/Jira/bin/start-jira.bat", "/fg"]
