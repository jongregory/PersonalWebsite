---
title: "Yaml Builds Azure Devops"
date: 2018-12-15T13:55:27Z
draft: true
tags: ["azure","azure devops","yaml"]
---

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