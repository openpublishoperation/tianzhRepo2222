# Configuring the repos
Content teams need to so some configuration in their repos after creation.

## 1. Initial repo configuration

The following steps assume you are just creating one docset. At the end of the section there are some examples of repo structure if you are creating multiple docsets  
1. At the root of the repo, create a **.gitignore** file. Edit it and add the following. This will make that the temporary build folders generated when running local builds don't get pushed into the repo:
```
log/
xhtml/
packages/
obj/
_site/
Tools/NuGet/
.optemp/

.openpublishing.build.mdproj
.openpublishing.buildcore.ps1
packages.config
```
 
2. Create at least one folder underneath your repo. That would be your docset.

3. Create a TOC.md inside your docset folder.
  
### 1.1 Examples of repo structure
The following is a repo structure with one docset.
```
/
|- .gitignore
|- README.md
|- docset/
|  |- a.md
|  |- b.md
|  \- TOC.md
```

The following is a repo structure with multiple docsets and independent TOCs.
```
/
|- .gitignore
|- README.md
|- docset1/
|  |- a.md
|  |- b.md
|  \- TOC1.md
\- docset2/
   |- c.md
   \- d.md
|  \- TOC2.md
```

The following is a repo structure with multiple docsets and a single TOC.
```
/
/
|- .gitignore
|- README.md
|- docset1/
|  |- a.md
|  \- b.md
\- docset2/
   |- c.md
   \- d.md
\- TOC.md
```

## 2. Branches
In open publishing, we use GIT branches to maintain different copies of the same content. Same topic in different branches will be published to different urls of rendering sites. This could be used in several scenarios:
1. Stage/promote. User can use one branch as staging branch and merge it to a live branch as a promote operation.
2. Private working branch. User can create his own branch to save files that is still under writing, and merge it to common branch when it's ready. Files in private branch can still be validated/previewed by open publishing.

### 2.1 Live Branch
Among all branches, there should be only one branch that is exposed to external users, and other staging/working branches are only used by writers for internal testing. This branch is called "Live" branch. Live branch can be identified by a special branch name. Content in live branch will be published to the live site. Content in other branches will still be published, but only to stage or sandbox.

## 4. Next steps
The next step is to [provision the repo](../engdocs/repo-provision.md). VSC will do that for you. Please make sure that:
Please send Xiaokai He and Sandra Aldana the following information:

- Repo URLs
- Publishing end-point: MSDN, TechNet, VS.com, other. If other, we need the canonical URL you would like to have for your site.
- Base URL for your content. This can be the docset name or a different one. This will be appended to the end-point URL. In our case, it is "openpublishing/docs", so the URL is `http://int.msdn.microsoft.com/en-us/openpublishing/docs`.