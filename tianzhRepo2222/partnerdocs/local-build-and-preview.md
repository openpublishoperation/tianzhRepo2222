# Local builds and preview
Open Publishing allows you to build your content locally to detect any potential error (like broken links), as well as preview your content locally for validation. 

Our team has been working on the simplification of the setup and maintenance of the configuration files for Open Publishing. In Sprint 94 our new schema will allow that dev’s features or changes won’t affect your repositories any more. We are also aiming at not having to change the configuration files after this time.

As a result, local build and preview commands have changed. 

## 1. <a name="local-build"></a>Local validation build 
Local build only runs build command to validate all the files build correctly. 
* Step 1: Clone your repo to your local machine. You can use Visual Studio, [GitHub Desktop](https://desktop.github.com/).
    * From Visual Studio, right-click on the cloned repo and click on **Open command prompt**.
        * Run the command `powershell .openpublishing.build.ps1`    
    * From GitHub Desktop, right-click on the repo and click on **Open in Git Shell**.
        * Run the command `.\.openpublishing.build.ps1

> [!IMPORTANT]
> If you meet the warning that "Api rate limit exceeded", please append one more parameter to give your access toekn after the command above.
> For example:
> 
> From Visual Studio: `powershell .openpublishing.build.ps1 -parameters:"_op_accessToken=<your personal access token here>"`
> 
> From GitHub Desktop: `.\.openpublishing.build.ps1 -parameters:"_op_accessToken=<your personal access token here>"`

You may specify additional arguments separated by `;` as below

`.openpublishing.build.ps1 -parameters:"{arg1}={value1};{arg2}={value2};...;{argN}={valueN}"`

Below table shows all optional arguments supported by Open Publishing tool:

| Argument | Setting | Example |
| -------- | ------- | ------- |
| _op_accessToken | The Git access token to access Git data. [[GitHub]](https://help.github.com/articles/creating-an-access-token-for-command-line-use/) [[Vso]](https://www.visualstudio.com/en-us/get-started/setup/use-personal-access-tokens-to-authenticate)  <ul><li>Optional if the Git repo is public.</li><li>Required if the Git repo is private.</li></ul> | `-parameters:"_op_accessToken={your access token}" ` | 

* Step 2: Look at the report and fix any errors that you might have. Run the command again to validate you are error free. 

## 2. Local preview
In addition to do build validation, local preview validates that the content and TOC look as you expect. 

* Step 1: Clone your repo to your local machine. You can use Visual Studio, [GitHub Desktop](https://desktop.github.com/).
    * From Visual Studio, right-click on the cloned repo and click on **Open command prompt**.
        * If you are working on content for docs.microsoft.com, run this command `git submodule update --init`. This downloads the docs.microsoft.com themes to your machine.
        * Run the command `powershell .openpublishing.build.ps1 -parameters:targets=serve`    
    * From GitHub Desktop, right-click on the repo and click on **Open in Git Shell**.
        * If you are working on content for docs.microsoft.com, run this command `git submodule update --init`. This downloads the docs.microsoft.com themes to your machine.
        * Run the command `.\.openpublishing.build.ps1 -parameters:targets=serve`
* Step 2: Look at the report and fix any errors that you might have. Run the command again to validate you are error free. Once you do not have any errors, you will be able to see the preview. 
* Step 3: Open http://localhost:8080 to see your content locally.

Note that any changes that you make after this point, are not going to be reflected in the local web site. You will need to close the command prompt window that popped up and run the preview command again.

## 3. Local HTML output
`<To be documented>`

## 4. <a name="local-pdf"></a>Local PDF output
Follow same steps as [local validation build](#local-build) and make sure you turn on the build of PDF in [publish configuration](publish-configuration.md#publish-config-need_generate_pdf).

After local build, go to your repository folder, the generated pdf(s) are under `_site` folder. Each docset will be built into one PDF named by `{docset name}.{locale}.v{version}.pdf`.
