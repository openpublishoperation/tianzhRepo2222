# Open Publishing Build Rest API Error Codes and Responses

The Open Publishing Build Rest API attempts to return appropriate [HTTP status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) for every request.

**HTTP Status Code**|**Text**|**Description**  
---------|---------|---------|----------
200 | OK | Get resource or log out successfully
201 | Created | Create resource(s) successfully
204 | NoContent| Delete resource or complete Basic Auth login successfully
207 | MultiStatus | Batch operations with partial success
302 | Redirect | OAuth login callback for Vso/GitHub
400 | BadRequest | Required field(s) or parameter(s) has not been provded, the value supplied is invalid, or the combination of provided fields is invalid
401 | Unauthorized | Authentication credential was missing, expired or incorrect
403 | Forbidden | Request doesn't have sufficient permission for accessing specified resource
404 | NotFound | Resource was not found which is specified in request
409 | Conflict | Create a resource which conflicts with an already existing one
422 | UnprocessableEntity | Failed to create a build from filtered branch, normally occurs for Vso/GitHub notification
500 | InternalServerError | A generic error message, given when an unexpected condition was encountered, e.g, insert/update Azure table failed
501 | NotImplemented | API has not implemented

## Structured Errors
When the Open Publishing Build Rest API returns error response, the body includes a machine-readable `error`, a human-readable `message` and a `documentation_url` pointing the client to further information about the error and how to resolve, e.g.,

```json
{
  "error": "UnsupportedProjectGetOperation",
  "message": "Only Vso supports get projects operation",
  "documentation_url": "https://ppe.msdn.microsoft.com/en-us/openpublishing/docs/open_publish_build_rest_api_error_codes_responses",
  "recommended_action": "Make sure you are login with Vso, for GitHub we don't support this API",
  "component": "Open Publishing Build Rest Api Service"
}
```

> [!NOTE]
> The error codes will stay the same, while the text for an error message may change.

## API Error Code and Message List
Requests made to our APIs can result in a number of different error responses, and there are a few basic recovery tactics.

**Error Code**|**Error Message**|**Recommended Action**  | **Will Occur in Portal**
---------|---------|---------|----------|--------
BranchNotFoundInGitRepository | Branch {0} is not found in git repository {1} | Confirm the branch name existed in your git repository | No
BuildIndexTableEntityNotFound | Build with repository name '{0}', commit Id '{1}' and branch name '{2}' is not found | Confirm the repository name, commit id and branch name are correct | No
BuildTableEntityNotFound | Build with repository id {0} and build id {1} is not found | Confirm the repository id and build id are correct | No
CreateGitRepositoryWebHookFailed | User {0} doesn't have rights to provision the repository {1}, details: Failed to create webhooks in Git repository: {1} | Make sure you have Admin permissions in the repository | Yes
DepotNotExist | Docset name '{0}' with product name '{1}' doesn't exist. | System error, enter a bug or Live Site Issue via http://MSDNHelp and include the following error text. | No
DocsetNamesDuplicatedInPublishConfig | The following docset names are listed multiple times: {0} | Remove duplicated docset names in your .openpublishing.publish.config.json file under your root directory of Vso/GitHub repository | Yes
DocsetNamesNotFoundInPublishConfig | Following docsets do not exist in {0}: {1} | Check the missing docset name(s) in your `.openpublishing.publish.config.json` file under your root directory of Vso/GitHub repository | Yes
DocsetTableEntityAlreadyExists | Docset with name '{0}' is already created with same base path '{1}' | Docset already created with same name and base path in this repository, choose another docset name | Yes
DocsetTableEntityAlreadyExistsDifferentBasePath | Docset with name '{0}' is already created, but the site base path is different from already created one. Site base path of current one is '{1}', and created one is '{2}' | Docset already created with same name in this repository, but different base path, choose another docset name | Yes
DocsetTableEntityConflictsWithBasePath | Docset with base path '{0}' conflicts with another one with same docset name '{1}' but different site base path '{2} | Same docset name and product names aren't allowed to map to two different base paths，choose another docset name, product name, or base path | Yes
DocsetTableEntityConflictsWithTenant | Docset with tenant '{0}' conflicts with another one with same docset name '{1}' but different tenant '{2}' | Same docset name and product name maps to two different tenants is not allowed, if you want to create a docset with same docset name and product name, please confirm the tenant names are same | Yes
DocsetTableEntityNotFound | Cannot find docset for repository {0} and docset {1} | Confirm the repository id, docset name are correct and docset is not deleted | No
GitHubSignatureMismatch | GitHub signature '{0}' doesn't match the secret token preset | This usually means you fake the GitHub notification | No
GitRepositoryAlreadyExists | Repostiory {0} under account {1} already exists | The repository already created in Vso/GitHub, please select a new repository name or change the account | Yes
HttpsRequired | Https required for accessing Open Publishing Build Rest Api Service | Change your url scheme to https, our service enabled full-site https | No
InsertOrUpdateAuthenticationCacheFailed | Insert/Update user {0} to authentication cache failed | System error,  retry after some time, or enter a bug or Live Site Issue via http://MSDNHelp and include the following error text. | Yes
InsertOrUpdateAuthenticationTableEntityFailed | Insert/Update user {0} to authentication table failed | As above | Yes
InsertOrUpdateBuildCommitIndexTableEntityFailed | Insert/Update build {0} to build commit index table failed | As above | Yes
InsertOrUpdateBuildTableEntityFailed | Insert/Update build {0} to build table failed | As above | Yes
InsertOrUpdateDocsetTableEntityFailed | Insert/Update docset {0} to docset table failed | As above | Yes
InsertOrUpdatePullRequestCommitIndexTableEntityFailed | Insert/Update pull request {0} to pull request commit index table failed | As above | Yes
InsertOrUpdatePullRequestTableEntityFailed | Insert/Update pull request {0} to pull request table failed | As above | Yes
InsertOrUpdateRepositoryTableEntityFailed | Insert/Update repository {0} to repository table failed | As above | Yes
InsertOrUpdateUserTableEntityFailed | Insert/Update user {0} to user table failed | As above | Yes
InvalidBuildIdParameter | {0} is not a valid build id | Make sure the build id in DateTime-branch format, especially the date time follows the `yyyyMMddHHmmssffff` format, e.g., `201601060808154999-master` | No
InvalidDateTimeParameter | {0} is not a valid datetime of format {1} | Check if the date time in {0} is in the format of {1}, normally this occurs when your query date time is not in the `yyyyMMddHHmmss` format | No
InvalidDocsetIdParameter | {0} is not a valid docset id | Make sure the docset id in Guid format(`8-4-4-4-12`), e.g., `1234567-89ab-cdef-0123-456789abcdef` | No
InvalidParameter | Parameter has invalid value or missing required parameter, details: {0} | Follows details to fix data, like add missing parameters | No
InvalidRepoIdParameter | {0} is not a valid repo id | Make sure the repository id in Guid format(`8-4-4-4-12`), e.g., `1234567-89ab-cdef-0123-456789abcdef` | No
InvalidRepositoryScope | {0} is not a valid repository scope, it should be Op or All, default is Op | Repository scope only allows `op` and `all` (case-insensitive), you should use any of them or remove this query string key `op` | No
MissingGitHubEvent | GitHub event delivery request doesn't contain header '{0}' or the value is empty | System error, directly enter a bug or Live Site Issue via http://MSDNHelp and include the following error text. | No
MissingPartitionAttribute | Type {0} doesn't define Partition attribute | As above | No
MissingVsoEvent | Vso event delivery request body doesn't contain attribute '{0}' or the value is empty | As above | No
PermissionNotSufficient | User with id {0} does not have sufficient permission to perform the API request. Details: required permission '{1}', actual permission '{2}'. Hint: {3} | Normally means you don't have permission of this git repository or you are not member of [OpenPublish Organization](https://github.com/orgs/openpublish/), if it's latter, please send email to us to join the organization or contact us to on-behalf of you to do specified operation. | Yes
PullRequestIdIndexTableEntityNotFound | Cannot find pull request for repository {0} and pull request {1} | Confirm the repository id and pull request id are correct | No
PullRequestTableEntityNotFound | Cannot find pull request for repository {0} and pull request {1} | As above | No
RepositoryTableEntityAlreadyExists | The repository {0} has already been created | Repository already created with same Vso/GitHub git repository url | No
RepositoryTableEntityNotFound | Cannot find repository for repository {0} | Confirm the repository id is correct | No
UnauthorizedOAuthAccess | OAuth authentication credentials were missing or incorrect | Try login through Portal again | Yes, but Portal will automatically redirect user to login page
UnauthorizedBasicAuthAccess | Authorization header was missing or not in the basic scheme format: `Authorization: Basic <base64encodedvalue>` | Make sure request contains Authorization header with Basic scheme | No
UploadGitRepositoryInitializationFilesFailed | Upload provisioning initialization files to github/vso failed. Details: {0} | System error, directly enter a bug or Live Site Issue via http://MSDNHelp and include the following error text. | Yes
UnrecognizedGitCommitType | Unrecognized git commit type {0} | As above | No
UnrecognizedGitRepositoryPermissionType | Unrecognized git repository type {0} | As above | No
UnrecognizedGitRepositoryType | Unrecognized git repository type {0} | Make sure the git repository type is Vso or GitHub | No
UnrecognizedSiteName | SiteName '{0}' is not supported | Site name should be one of following values: <ul><li>MSDN</li><li>MSDNINT</li><li>VisualStudio</li><li>VisualStudioINT</li><li>TechNet</li><li>TechNetINT</li></ul> | No
UnsupportedGitActivityEvent | Git activity event {0} of {1} is not supported | Normally occurs for Vso/GitHub notification when the push type is delete, which is not supported. | No
UnsupportedProjectGetOperation | Only Vso supports get projects operation | Make sure you are login with Vso, for GitHub we don't support this API | No
UserTableEntityNotFound | Cannot find user {0} | System error, directly enter a bug or Live Site Issue via http://MSDNHelp and include the following error text. | No
VsoSignatureMismatch | Vso signature '{0}' didn't match | This usually means you fake the Vso notification | No


> [!NOTE]
> {0}, {1}... are places holders, the error message you see will be replaced by actual value


If you see an error code which is not listed in the above table, then fall back to the HTTP status code in order to determine the best way to address the error.

If in Open Publishing Build Portal, you see an error code which is marked as 'Won't occur in Portal', please directly enter a bug or Live Site Issue via http://MSDNHelp and include the following error text..