---
title: "Yaml Builds Azure Devops"
date: 2018-12-15T13:55:27Z
draft: false
tags: ["azure","azure devops","yaml"]
---

My first delve into the new Azure Devops has been great fun and easy to set up simple builds and deployments. I wanted to add SonarQube analysis into the generated YAML builds.

The first stop is the [SonarQube TFS Documentation](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Extension+for+VSTS-TFS) which details the extension which needs to be installed in Azure Devops (Called TFS in the documents). This installed easily but I found later that is needed to be reinstalled as the tasks where not showing up in the Azure DevOps menu.


I found the YAML easy enough to understand but I couldn't find the documentation for the YAML steps required for Sonarqube, then I saw a tip to use the [build designer](https://docs.microsoft.com/en-us/azure/devops/pipelines/get-started-designer?view=vsts&tabs=new-nav) and then select the view YAML button. This can then be copied and shows the Sonarqube steps which  can be further edited with any requirements and added into source control. 

This [blog](http://www.codewrecks.com/blog/index.php/2018/10/10/azure-devops-pipelines-and-sonar-cloud-gives-free-analysis-to-your-os-project/) was a great resource to point me in the right direction.


The complete YAML looked like this;

{{< highlight yaml>}}
 resources:
- repo: self
queue:
  name: Hosted VS2017
#   demands: java
variables:
  buildConfiguration: 'Release'

steps:
- task: DotNetCoreCLI@2
  displayName: Restore
  inputs:
   command: restore
   vstsFeed: lib
   projects: '**/*.csproj'

- task: SonarSource.sonarqube.15B84CA1-B62F-4A2A-A403-89B77A063157.SonarQubePrepare@4
  displayName: 'Prepare analysis on SonarQube'
  continueOnError: true
  inputs:
    SonarQube: 'FM-SonarQube1'
    projectKey: <**Replace with project key**>
    projectName: <**Replace with project name**>

- task: DotNetCoreCLI@2
  displayName: Build
  inputs:
    projects: <**Replace with solution name**>
    arguments: '--configuration $(BuildConfiguration)'

- task: DotNetCoreCLI@2
  displayName: Test
  inputs:
    command: test

    projects: '$(Parameters.TestProjects)'

    arguments: '--configuration $(BuildConfiguration)'



- task: SonarSource.sonarqube.6D01813A-9589-4B15-8491-8164AEB38055.SonarQubeAnalyze@4
  displayName: 'Run Code Analysis'
  continueOnError: true


- task: DotNetCoreCLI@2
  displayName: Publish
  inputs:
    command: publish
    arguments: '--configuration $(buildConfiguration) --output $(Build.ArtifactStagingDirectory)' (Breaks the code)
    publishWebProjects: true
    modifyOutputPath: true
    zipAfterPublish: true
    projects: <**Replace with project name to publish**>

- task: PublishBuildArtifacts@1
  displayName: 'Publish Artifact'



{{< / highlight >}}  