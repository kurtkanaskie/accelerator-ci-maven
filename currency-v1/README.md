## Git Commands

### Intitial
* git checkout -b prod
* git push origin prod
* git checkout master

### Feature
* git checkout -b feature/jira1
* git push origin feature/jira1
MAKE changes for feature/jira1
* git commit -am  "Added changes for feature1"
* git push origin feature/jira1
OBSERVE build

#### Test locally
* set your ~/.m2/settings.xml
* mvn -X install -Ptest -Dcommit=local -Dbranch=/feature/jira1 

#### Merge to Master
##### Pull Request
* Go to repo and create pull request from feature/jira1 to master
* Comment on pull request
* Do the merge pull request "Create a merge commit" or use command line

##### Via command line
* git checkout master
* git merge --no-ff feature/jira1
* git push
Clean up feature branch
* git branch -d feature/1
* git push origin :feature/1


### Merge to Prod
This is automatic, once the build in master succeeds
