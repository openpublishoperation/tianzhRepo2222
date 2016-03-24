# Create a link reference in OPS
Adding links to another content in OPS is a very common use case and OPS has a capability to resolve and validate the links in below situations: 

## Reference content in the same Docsets
Docset is an OPS concept that is a group of similar content. A Docset is created during provisioning process and should contain a TOC.md and some specific configuration file. In OPS, the build system treat Docsets as the boundry for reference validation. So for any link reference within the Docsets, the build service is able to resolve and validate that link in common GFM markdonw syntax:

```md
[My link text](..\active-directory\active-directory-article-name.md)
```
Writers could use relative path in above examples to create link reference within the same docset. 

## Reference content in external Docsets
As mentioned above, OPS currently doesn't support resolve and validate logic for cross-docset reference, that is, if you want to reference a file in another docsets, you will not be able to use the syntax in above case. However, if you need to add a cross-docset reference, you need to use *absolute path reference*, for example:

```md
[My link text](/active-directory/active-directory-article-name.html)
```
the "/active-directory/active-directory-article-name.html" is part of the full URL without the domain, so it creates a link to https://{Domsin}/active-directory/active-directory-article-name.html