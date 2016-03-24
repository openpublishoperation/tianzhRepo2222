# Provisioning the GIT repos - (VSC task)

After all the following steps are completed, Open Publishing will automatically build and publish the updated content from a monitored docset to MSDN, TechNet, or VS.com web sites. You should have got the information listed in the [repo creation page](../partnerdocs/repo-creation.md) from the partner.

You can get a sample of the files to be added to the repo from this site.
 
## 1. Making the repo an Open Publishing repo


### 1.1. Adding the Publishing Service Configuration File: .openpublishing.publish.config.json
This file needs to be under the repository. It tells Open Publishing how to build and publish the content found in the GIT repo.

> [!IMPORTANT]
> This file needs to be placed in the **live** branch in order for the repo to be provisioned.

Find details on how to set the configurations [here](../partnerdocs/publish-configuration.md).

### 1.2. Provisioning on the portal
- Once you have the publish configuration file under the repository and make sure you also have the live branch contains that configuration file, go to [portal](https://op-portal-prod.azurewebsites.net) to have the repo monitored.
- Open Publishing portal will only parse the configuration file under **live** branch when doing provision.
- "Base Path": It can be configured via the portal. This field would be the common base path for all the topics in this docset, and is eventually part of the rendering URL.

## 2. Adding the Build Tools Configuration
The Open Publishing service provides the entry point for how to build the content. Users can either use their own build tools or use the build tool provided by Open Publishing service.

The default build tool for Open Publishing is [DocFX](https://dotnet.github.io/docfx/).

### 2.1. Using DocFX to build contents
By default, Open Publishing tool uses [DocFX](https://dotnet.github.io/docfx/) to build contents. It also leverages plugin mechanism of [DocFX](https://dotnet.github.io/docfx/) and uses Git commit history and user information to generate additional metadata related to:
- Author
- Update date
- Contributors
- Content Git URL

### 2.2. Customize [build_entry_point](#publish-config-build_entry_point) to use your own tool
	- Coming Soon~
	
## 3. Creating and setting up localized repos
The localized content will live in separated repos, connected to the English one via our Open Localization service. Details:
- One locale per localized repo.
- One single repo for handoff and hand back for the a group or organization. Right now, there is only one repo across Microsoft, but this will be fixed in the future.  
 
 1. Work with partner to grant READ access to "olprod" account in the English repo.
 2. Work with partner on branches that need to be monitored (hand off) to localization.
 3. Work with partner to define which locales the content is going to be localized into.
 4. Update the **.localization-config** with the following information.
 
	- **locales** - add the locales the partner would like to localize in the form of locale-culture set. E.g. "ja-jp", "de-de",...
	- **files** - List all the folders and file types to localize, include the docset name plus "**" to include all the folders underneath, and then mask the file types. E.g. `"virtualization/*/*.md"` and `"virtualization/**/*.md"` includes all the Markdown files under the docset, including all the subfolders.
	- **includeDependencies**
		- Set to true to include in the handoffs the topic dependencies (includes). 
		- Set to false to only include the Markdown files.
	- **autoPush**
		- Set to true to automatically check-in the hand back files into the localized repo.
		- Set to false to create a pull request for the hand back so an admin can approve.

 5. Copy this file into the branch that needs to be monitored, at the root of the repo.
 6. Have OL service to monitor English repo
		- Add GIT repository which need to be monitored to OL service configuration
			- Locate the open localization configuration file in ol prod server machine at C:\OpenLocalization\src\OpenLocalization.Runner\OpenLocalization.json (we will move it to ambient configuration in the future)
			- Add source repo(remote url + path + workingbranch) and target repo(owner + path + workingbranch) information to repos list.
		- Monitoring needs to happen for each branch
 7. Changes a file in the English repository, in the branch that is monitored to create the localized repos and create the first handoff. Right now handoff repo's name is https://github.com/Microsoft/Virtualization-Documentation-Private.handoff/tree/master/ol-handoff/Microsoft, and contains the XLIFF files. Right now, this repo is common for all teams at Microsoft.
 8. Localization repo(s) get created automatically based on the locales in the localization.json file.
	- File has the same than English with ".locale" added at the end.
 9. Log with "olprod" account into localized repos and add IPMs as owners.
 	- You would need to get the IPMs GitHub accounts.
 10. Add the OP configurations to all the loc repos.
	- Provision is the same than for English with one exception. In ".openpublishing.publish.config.json" add "branches_to_filter": ["master-oldev", "live-oldev"].
 11. work with partner to grant read or write permissions to the IPMs to the English repo.

## 4. Create and provision multiple docsets in one repo 
There are cases that partners want to have mutliple docsets in one repo, or even nested docsets. This is not a recommended scenario but we do see some requests and this is supported in OPS. Please be noticed there are  some limitation, e.g. cross docset reference, so please confirm with user that this is really needed before create multiple docsets/nested docest in one repo.

### Nested Docsets
For example, there is a docset at root level called 'IntuneDocs', and partner request to create another sub-docset inside the IntuneDOcs, called 'GetStarted'. Here is how we provision and set up this:
1. Clone the repo to your local machine
2. Creat 'GetStarted' folder under 'IntuneDocs' folder
3. Create a docfx.json file in the 'GetStarted' folder with below changes:
    - Update the 'dest' value to `"dest": "InTuneDocs/GetStarted"`
    - Update the 'basepath' value to `"basepath": "/InTune/GetStarted"`
4. Update the docfx.json file in the 'IntuneDocs' folder:
    - Add one exclued rule for both content/resources sub docsets, otherwise the content will be published twice in both docsets e.g:
    ```json
    "content": [
      {
        "files": [
          "**/*.md"
        ],
        "exclude": [
          "**/obj/**",
          "GetStarted/**"      
        ]
      }
    ],
    "resource": [
        {
          "files": [
          "**/images/**", 
          "**/*.png",
          "**/*.jpg",
          "**/*.gif",
          "**/*.bmp",
          "**/*.html",
          "**/*.css",
          "_themes/**"
          ],
        "exclude": [
          "**/obj/**",
          "_themes/DocPacker/**",
          "GetStarted/**"  
        ]
      }
    ],
    ```
 5. Update the publish config file on live branch to add the new docsets
 6. Still need to go to OP portal to add selected docset for provision 
 
 > [!IMPORTANT]
> Previously, we need to creat a get submodule reference in the newly created docsets, however this is not needed anymore. We will have only one template submodule in each repo, no matter how many docsets created. And submodule reference set up will be automatica done during the provision step. 
