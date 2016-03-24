# Open Publishing Build Backend Error and Warning Log Codes and Messages

The Open Publishing Build Backend will generate a build report in **XML** format after completing a build. When examine the build report, you will find some `LogItem` with human-readable `Message`, log level `MessageSeverity` and happened component `Source`, e.g.,

```xml
<LogItem>
  <Message>Invalid file link(~/CGaarden CAPS-sample.md) in file "Content/TOC.md"</Message>
  <Source>Build Document</Source>
  <File>Content/TOC.md</File>
  <MessageSeverity>Error</MessageSeverity>
  <DateTime>2016-01-05T20:07:49.8501643Z</DateTime>
</LogItem>
```

## Backend Error Code and Message List
Open Publishing Build will generate some `LogItem` in different severity level, here we only includes the `Error` and `Warning` Level. Currently we only include the log code in server side, exclude the error messages from [DocFx](http://dotnet.github.io/docfx/).

All these errors are internal errors.

> [!NOTE]
> TODO: Machine-readable log code will be included in the report later.


**Error Log Code**|**Error Message**|**NOTE**  
---------|---------|---------|----------
BuildTableEntityNotFound | Cannot find build table entity for repository {0} and build {1} |
CannotMergeCommit | Cannot merge commit {0} in branch {1} of repository {2} into branch {3} (commit {4}) |
CannotSyncGitRepo | Cannot sync git repo to specified state. Please make sure the pull request is mergeable. Details: {0} |
DuplicateDocsetOutputFolder | Another docset inside the publishing config file has same output folder: {0}. Please change one of them |
GitRepoUnauthorizedWithoutSourceCommit | Unauthorized to sync git repostiory: {0} |
GitRepoUnauthorizedWithSourceCommit | {0}. Possible reason is that the repository is a private repository that requires token to access. The owner of the repository should logon to Open Publishing portal at '{1}' to grant Open Publishing Service the token to access the repository. After logon, please update the pull request to trigger the build again |
InvalidBuildToolConfigFile | Build tool's config file: {0} is not valid. Exception: {1} |
InvalidExternalBuildProperties | External build properties is not in valid format: {0} |
InvalidReference | Reference is invalid: {0} | 
LocalAndRemoteGitRepositoryMismatch | Local directory '{0}' maps to Git repository '{1}'. Expected Git repository is '{2}' |
ManifestNotSupported | {0} is not supported in publish and also is not defined in mapping types |
MessageCountMismatchTotalCount | Record count should match total count {0} for message {1}. Message count: {2} |
MissingFiles | Some files are missing: {0} | 
MissingSourceGitCommit | Source git commit should be specified for pull request |
MsBuildNotFound | Cannot locate msbuild in following folders: {0} |
NormalizeArticleFailed | Normalize file reference for file {0} failed. Error: {1} |
NormalizeImageFailed | Normalize image reference for file {0} failed. Error: {1} |
PublishToDHSFailed | Published of document '{0}' to document hosting service failed with asset id: {1} locale: {2}, depot name: {3}, branch name: {4} |
ProjectFileNotFound | Cannot find project file '{0} |
PullRequestFromDifferentRepositoriesNotSupported | Pull request from different repositories on {0} is not supported |
PullRequestTableEntityNotFound | Cannot find pull request table entity for repository {0} and pull request {1} | 
ReadBuildLogFailed | Error when reading build logs of project {0}, target {1}: {2} |
RepositoryInformationNotFound | Cannot find repository information for {0}. Please make sure the repository is correctly provisioned |
RepositoryTableEntityNotFound | Cannot find repository table entity for repository {0} |
ResolveContributorInformationFailed | Error when resolving contributor information for file {0}: {1} |
RunExternalBuildFailed | Build project {0}, target {1}, properties {2} failed: {3} |
RunPsScriptFailed | Run script {0} with arguments: {1} failed: {2} |
TocFileNotFound | Toc file content: {0} is not valid. Exception: {1} |
UnableToSaveSubMessagesToAzureTable | Cannot save submessages to Azure table:{0}. Message id: {1} |
UnrecognizedBuildType | Unrecognized build type {0} | Only allow Commit and PullRequest
UnrecognizedGitRepositoryType | Unrecognized git repository type {0} | Only allow Vso and GitHub
UserTableEntityNotFound | Cannot find user table entity for user {0} |


**Warning Log Code**|**Warning Message**|**NOTE**  
---------|---------|---------|----------
AuthorInformationNotFound | Cannot find author information for specified name '{0}' for file {1} |
DocsetInformationNotFound | Cannot find docset information for repository: {0} and docset name: {1}. Please make sure the docset is correctly provisioned | Follow instructions [Provision repository](../specdocs/ProvisionRepo.md)
DocsetPavedOver | Docset {0} in repository {1} is paved over. Please restore the docset to reenable publish | Follow instructions [Edit repository](../specdocs/UpdateDocset.md)
InvalidManifest | Manifest json file '{0}' is invalid |
InvalidTypeMapping | Type mapping in docset {0} is invalid |
ManifestNotExist | Build manifest file {0} of docset {1} does not exist. Please check the publish configuration |
NoDocsetProvisioned | No valid docset found in repository {0} | If you want to provision docsets in Open Publishing Build Service, also follow [Provision repository](../specdocs/ProvisionRepo.md)
NoDocumentPublished | No document is published |



> [!NOTE]
> {0}, {1}... are places holders, the error message you see will be replaced by actual value

If you see an error code which is not listed and the `Source` is also not *Build Document* in the above table, then enter a bug or Live Site Issue via http://MSDNHelp and include the following error text.
