# Authoring content for Open Publishing ##
This topic will contain information you need to know when authoring content in Open Publishing. 

1. Make sure all your files and arts are inside your docset. Open Publishing will not be able to reference to any file that is not inside the docset. Trying to reference a file outside the docset will make the build to fail. 
2. When adding HTML comments, use the following syntax: ```<!-- Comments -->```. 
3. If a topic has not been added to a TOC, then a TOC will not be shown when the topic is rendered.
4. While OP does not provide any templates, you can create your own templates and share them with your team. [Here is an example of how Azure is doing it](https://github.com/Azure/azure-content/tree/master/markdown%20templates).If you copy them in one folder, then you can exclude that folder and prevent it from building and publishing in docfx.json file.
