---
title: "Why I use SonarQube...."
date: 2016-02-23T18:02:14Z
draft: false
tags: ["sonarqube","quality","architecture"]
---

**Why I use SonarQube...** 

SonarQube [http://www.sonarqube.org/](http://www.sonarqube.org/) is a fantastic opensource tool for measuring code quality across multiple projects. I use it to provide an ''At-a-glance'' view of the size and quality of the projects I am involved in.

Where ReSharper or equivalent provides a point of creation view of code issues to the developer, SonarQube provides a historical and aggregated view.

SonarQube provides Customisable dashboards , Historical Views, Multi Language Support and much more. The features page describes in more detail [http://www.sonarqube.org/features/](http://www.sonarqube.org/features/) and the fantastic Nemo site shows a working instance of SonarQube [https://nemo.sonarqube.org/](https://nemo.sonarqube.org/)

I gave a 15 minute talk introducing SonarQube at my local usergroup DotNetNotts and the slides are here [http://www.slideshare.net/JonathanGregory4/code-quality-llightning-talk](http://www.slideshare.net/JonathanGregory4/code-quality-llightning-talk)

**Useful Applications**

These are just some of the situations I have SonarQube useful in over the last few years.

*   Automating the mundane parts of code review process
*   Identifying training needs in the team
*   Provide Return on Investment Metrics for Technical Debt work to management.
*   Target precious re-factoring time to most beneficial areas
*   Consistency in Applying Standards
*   Incentive to write cleaner code
*   Map a teams improvement over time
*   Basis for code reviews

**Running an Analysis**

In order to get a project into SonarQube it is necessary to run an analysis application, this reads a Sonar-Project.Properties file in the root of the project.

There are several ways to integrate this analysis runner into your CI process, more details are here [http://docs.sonarqube.org/display/SONAR/Analyzing+Source+Code](http://docs.sonarqube.org/display/SONAR/Analyzing+Source+Code). 

If you are lucky enough to be using TFS it can be integrated into MSBuild and the TFS flow [http://docs.sonarqube.org/display/SONAR/Analyzing+with+SonarQube+Scanner+for+MSBuild](http://docs.sonarqube.org/display/SONAR/Analyzing+with+SonarQube+Scanner+for+MSBuild).

I am currently working on multiple projects across many CI processes depending upon so have set up a dedicated SonarQube server in Azure to bring all the projects together.

For the analyser I  used the command line runner [http://docs.sonarqube.org/display/SONAR/Analyzing+with+SonarQube+Scanner](http://docs.sonarqube.org/display/SONAR/Analyzing+with+SonarQube+Scanner)

I wrote some bespoke PowerShell to do the following;

1.  Read a Config File of projects and the repository URL''s
2.  Check if first run
3.  Do a pull for updates
4.  If there are any changes run SonarQube

I fire this off daily using a task scheduler on the server and can then only analyse projects that have been active. This is far more efficient as I am analysing multiple smaller projects, and I can also see when project where last active in the dashboard view.

The main advantage of this script is any developer can add a project to the config file and check into source control, on the next run the updated config file is pulled and the project analysed.

I have put this script in GitHub as it maybe a useful base for others. [https://github.com/jongregory/SonarCaller](https://github.com/jongregory/SonarCaller)

**Conclusion**

SonarQube is very quick and easy to set up with no licence costs, there is a two minute getting started guide [http://docs.sonarqube.org/display/SONAR/Get+Started+in+Two+Minutes](http://docs.sonarqube.org/display/SONAR/Get+Started+in+Two+Minutes) and a more detailed set up from Microsoft projects [https://github.com/SonarSource-VisualStudio/sonar-.net-documentation](https://github.com/SonarSource-VisualStudio/sonar-.net-documentation)

I would recommended it to anyone and it one of the first actions I do now on a new project to start recording the quality of the project.