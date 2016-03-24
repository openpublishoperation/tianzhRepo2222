#I Want to Publish Reference through OP

In this article, we will publish managed/unmanaged reference from source code.
Generally, we can share the same steps as publishing markdown articles. So here we will focus on the particular part in publishing reference.

##STEP1-3: Prepare the repo and docset

- Firstly, we need to finish `STEP1` to `STEP3` in [I want to create a Git and OP repository on portal](https://ppe.msdn.microsoft.com/en-us/openpublishing/docs/specdocs/newrepo).

##STEP4: Prepare the input `yml` files

> [!NOTE]
> When publishing **UNMANAGED** reference, we can skip this STEP because the input is already `.yml` files.

- Instead of using `.md` as input to generate conceptual article, we use `.yml` to generate reference. In this step, we will use `docfx` to generate `yml` files from source code, then use them as input of the docset.
  1. Download the latest `docfx` from [docfx homepage](http://dotnet.github.io/docfx/index.html).  
  2. Extract the `docfx.zip` to obtain the `docfx.exe` and DLLs.
  3. Run the following command to generate `yml` files from source code. `<code project>` can support following formats: `.sln`, `.csproj`, `.vbproj`, `.cs`, `.vb`. 
  ```
    docfx.exe metadata <code project>
  ```
  4. `yml` filses will be generated in `_api` folder.
    
- **Advanced**: We can also use `docfx.json` to specify the source code. More information can be found on [docfx tutorials](http://dotnet.github.io/docfx/tutorial/walkthrough_create_a_docfx_project_2.html#step2-generate-metadata-for-the-c-project). 

##STEP5: Add `yml` files to repo

- Copy the generated `yml` files (including `toc.yml`, `.manifest`) to the repo created in `STEP1-3`. Remove the auto generated `TOC.md`.

##STEP6: Edit `docfx.json`

- Add `{"files": [ "**/*.yml" ],"dest": "api"}` to the auto generated `docfx.json`. The updated `docfx.json` is like below. 

```
{
  "build": {
    "content": [
      {
        "files": [ "**/*.yml" ],
        "dest": "api"
      },
      {
        "files": [
          "**/*.md"
        ],
        "exclude": [
  ...
```
##STEP7: Publish

- After commit and push the change, we return to [STEP4: Manual Publish](https://ppe.msdn.microsoft.com/en-us/openpublishing/docs/specdocs/newrepo?branch=master#step4-manual-publish) to publish the managed/unmanaged reference contents!