# GitHub Terminology #
The GitHub documentation provides very good guidelines to ramp you up and get familiar. In any case, we include here some basic terminology to get you started.

- **Git** - An open-source version control system. Linus Torvalds created it.
- **GitHub** - A company that provides open source code repository hosting as a service. We are using their service as a content management system. GitHub is built on top of Git. To interact with GitHub, you can use their web interface or install Git tools (like Git Bash, or Visual Studio 2015) on your local machine.
- **repository (repo)** - Our content databases in GitHub. At the command line, commands that include “upstream” are acting on the repository. 
- **the public repo** - External facing content repo; customers and infrequent contributors can submit changes to articles.
- **the private repo** - Internal facing content repo; anyone inside Microsoft can obtain perms and contribute new articles and changes to existing articles. Frequent contributors should use the private repo, and all content with a disclosure date must be authored here.
- **fork** - Your online copy of the repository in GitHub. You push your changes into your fork first to help protect the core repository. At the command line, commands that include “origin” are acting on your fork of the repo.
- **clone** - The local copy of your fork on your computer. 
- **branch** - A copy of the repository within each core, fork, or local version of the repo. The core repository has a master branch, a daily publishing branch, and some milestone release branches. You check content into the branch that corresponds to the release you are targeting. On your local computer, you create and author within local working branches.
- **pull request** - You create a pull request to move changes from your fork to the main repository – the pull request shows all the diffs between your fork and the branch you want to changes to go to in the main repository. All pull requests are reviewed before acceptance to ensure that metadata is present, basic markdown is correct, content regressions are avoided, and that validation issues are resolved.
- **merge conflict** - When Git cannot automatically merge two different sets of changes to the same file. Merge conflicts have to be resolved manually.
