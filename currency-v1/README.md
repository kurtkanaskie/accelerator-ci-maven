## Git Commands

### Intitial
* git checkout -b prod
* git push origin prod
* git checkout master

### Feature
* git checkout -b feature/jira1
MAKE changes for feature/jira1

#### Test locally
Set your ~/.m2/settings.xml
* mvn -X install -Ptest -Dcommit=local -Dbranch=/feature/jira1 
Run unit tests and integration tests in local environment
* mvn process-resources exec:exec@unit -Ptest
* mvn process-resources exec:exec@integration -Ptest
Run integration tests in each environment
* mvn process-resources exec:exec@integration -Ptest -Ddeployment.suffix=
* mvn process-resources exec:exec@integration -Pprod -Ddeployment.suffix=
OBSERVE build

#### Test via Jenkins
* git commit -am  "Added changes for feature1"
* git push origin feature/jira1
OBSERVE build

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

#### Update local Master
* git checkout master
* git pull

### Merge to Prod
This is automatic via Continuous Delivery, once the build in master succeeds

### Other local deploy commands
* mvn install -Ptest -Dcommit=local -Dbranch=/feature/jira3
* mvn install -Ptest -Ddeployment.suffix=jenkins -Dcommit=local -Dbranch=/master
* mvn install -Ptest -Ddeployment.suffix= -Dcommit=local -Dbranch=/master
* mvn install -Ptest -Ddeployment.suffix= -Dcommit=local -Dbranch=/test
* mvn install -Pprod -Ddeployment.suffix= -Dcommit=local -Dbranch=/prod

#### Notes

Note the use of deployment.suffix it controls the proxy name and basepath, currency-v1 (master, prod), currency-jenkinsv1 (jenkins feature branches)

NOTE: Jenkins in docker uses the "setup/.run_image.sh" that sets global environment variables, so to move to a different org, you have to restart Jenkins, its not sufficent to set those in the pom.xml

Test
