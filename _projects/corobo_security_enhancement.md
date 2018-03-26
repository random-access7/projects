---
collaborating_projects:
  - IGitt
name: "corobo security enhancements through team support patches to IGitt"
desc: "pre-validation of users before corobo commands are executed by verifying privilege level"
requirements:
 - "Merged pull requests/merge request  to corobo, IGitt"
difficulty: "medium"
person_involved: random-access7
issues:
 - "https://github.com/coala/corobo/issues/509"
 - "https://gitlab.com/gitmate/open-source/IGitt/issues/94"
 - "https://github.com/coala/corobo/issues/462"

initiatives:
 - GSoC

---

One of the most integral part of open source development is the communication between contributors and 
for the coala organization this is through Gitter. In order to facilitate communication on Gitter, the coala
organization uses corobo as an automated chatbot which can be used to assign issues, invite new people,
mark PRs etc. However, in recent times, it has been seen that corobo has been misused by newcomers and 
banned members which mandates security enhancements in corobo so that such incidents are not repeated again. 

The major purpose of this project would be to enhance corobo through increased security measures which will 
begin by creating an enhanced labhub plugin which will ensure greater flexibility for maintainers to 
control usage of corobo. In order to achieve this, the IGitt module should be introduced with a teams class
which can be used to determine the teams within an organization.

The next phase will involve working upstream on errBot, specifically on the re_botcmd decorator and BotPlugin
in order to implement a new parameter for privilege level which can be used by labhub (or other plugins) for 
the pre-validation support. 

This will provide an interface for plugins to determine which team a particular user belongs to and this can
thereafter be used to determine whether a user has the requisite privilege level to access a labhub/plugin 
command by making use of a unique configuration file created by the maintainers. 

This **configuration file** will map groups to certain privilege levels which can then be used to determine 
commands/methods within the plugin that are accessible to members of each team.

The added advantage of this configuration file is the flexibility offered to maintainers in that they can 
change the privilege levels of particular teams as and when required. This can also be used in an "apocalyptic" 
scenario to ban everyone if required. 

Once this process of adding pre-validation support has been done for the labhub plugin, it will be extended to other 
plugins of corobo, thereby leading to complete control of commands through configuration files which further provides
maintainers the ability to completely ban members from using any commands of corobo.


#### Process

In order to create a teams class within the IGitt module, the foremost requirement is a GitHub 
implementaion through GitHub REST APIs:

 - https://developer.github.com/v3/teams/

in order to determine which teams are present within an organization and an 'is_member' function will
also be developed in order to determine which teams a member belongs to. The project will also explore
implementations for GitLab through orgs and suborgs as substitutes for teams in GitHub.

Following this, the labhub plugin will be modified to follow this procedure before any command is executed:
* Receive username/handle of user who wrote a command that is matched by re_botcmd decorator
* Determine the privilege level needed by the particular command from the configuration file made by maintainers
* Determine the privilege level of the user through the IGitt interface which determines the user's teams
* Validate this privilege level and execute command if validation succeeds

This is collectively know as the **pre-validation support** process and this methodology will be later extended to 
other plugins in order to get complete coverage of all commands offered by corobo.

#### Milestones

##### GSOC 2018 COMMUNITY/BONDING

* Create a cEP describing the process of pre-validation to be used by methods to validate users which includes
  implementation plans about interfacing between IGitt and labhub/plugin methods.
* Create cEP describing the format of the configuration files to be used by maintainers to define privilege levels.
* Create cEP/plan to introduce a new parameter that will support the pre-validation support.
* Explore ways to implement team support for GitLab.
##### CODING PHASE 1

* IGitt enhancements to be completed by adding a team class which uses the GitHub REST API to determine teams and 
  creation of method(s) to determine if a member belongs to a particular team or not.
* Add GitLab support if implementation ways discovered in community bonding.

##### CODING PHASE 2

* Enhancing the labhub plugin to include pre-validation support for users through IGitt interface and using the 
  configuration file to verify privilege levels. This will be achieved by working upstream on errBot to introduce 
  a parameter for re_botcmd/BotPlugin in order to support the pre-validation process.

##### CODING PHASE 3

* Extending pre-validation support to other plugins developed for corobo.
