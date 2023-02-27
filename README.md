Commands for creating an Unlocked Package
Authorize DevHub

sfdx force:auth:web:login -d -a DevHub
here DevHub is an alias of Salesforce instance where we enable "DevHub and Unlocked Packages and Second-Generation Managed Packages"

Check sfdx-project.json
{ "packageDirectories": [ { "path": "force-app", "default": true } ], "namespace": "", "sfdcLoginUrl": "https://login.salesforce.com", "sourceApiVersion": "50.0" }

Create the Package
sfdx force:package:create --name testunlocked --description "testunlocked package" --packagetype Unlocked --path force-app --nonamespace --targetdevhubusername DevHub

Create the Package Version
sfdx force:package:version:create -p testunlocked -d force-app -k test1234 --wait 10 -v DevHub --codecoverage --codecoverage Calculate and store the code coverage percentage by running the Apex tests included in this package version. Before you can promote and release a managed or unlocked package version, the Apex code must meet a minimum 75% code coverage requirement. Without this it is not possible to promote.

Promote
sfdx force:package:version:promote -p testunlocked@0.1.0-1 -v DevHub

Intall the package
sfdx force:package:install --wait 10 --publishwait 10 --package testunlocked@0.1.0-1 -k test1234 -r -u PackageDemoOrg

here PackageDemoOrg is alias of Salesforce instace where we want to install our package
