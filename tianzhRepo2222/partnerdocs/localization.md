#Localization

Localization is offered via the Open Localization service. 

##Repo creation
Repos are created automatically by updating the [.localization-config](repo-creation.md) 

## Handoff 
- Whenever there is any content pulled to the English “master” branch, the localization service will be triggered and the handoff package is created automatically. The package is being updated until the files are handed off. Then, a new package will be created.  

## Hand back
After the files are translated and hand back is placed in the right location, hand back gets triggered and the localized content will be pushed to the localized repository’s “master” branch. At this time build will be also triggered and localized content will be published to stage.

## Content Publishing
This section only contains any differences between English and localized languages publishing. Make sure to refer to the [Content publishing](publish.md) topic for complete information.

Alike English, once the hand back is done into the master branch, the content will be published to stage. This is an automatic process.

Merging the content to the live branch is a manual process. Once the content is in the live brnach, the localized content will go to live.

## Build status and reports
The submitter of the changes as well as those in the (notification list)[repo-config.md], will get a mail indicating whether the build is successful or not, a link to the documentation, as well as a link to the build report. 

Alternatively, teams can look at the [Open Publishing Portal](https://op-portal-sandbox.azurewebsites.net) for build status and logs of current and past builds.