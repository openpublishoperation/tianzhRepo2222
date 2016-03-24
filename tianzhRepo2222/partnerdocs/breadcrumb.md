---
author: tspowen
---
#Breadcrumb 

Breadcrumb is a very common navigation component, it usually appears at the top of the page that enables the user to navigate to higher-level document collections. Also, the breadcrumb offers users an idea about under which part of the site a user is currently viewing. In OPS, breadcrumb is a very similar concept as TOC, that the structure is specified in a seperated file in a structured way, other pages just reference the breadcrumb file and render on the page. 

##What does the breadcrumb source file look like
In OPS, breadcrumb data is put into a toc.yml file and create in a tree structure, for example:

```md
- name: Enterprise Mobility
  href: /EM/
  homepage: /EM/index.html
  items:
  - name: Solutions
    href: /EM/Solutions/
    homepage: /EM/Solutions/byod-design-considerations-guide.html
  - name: Advanced Threat Analytics
    href: /ATA/
    homepage: /ATA/index.html
    items:
      - name: Understand and explore
        href: /ATA/Understand/
        homepage: /ATA/understand/ata-understand-and-explore.html
      - name: Plan and design 
        href: /ATA/PlanDesign/
        homepage: /ATA/plandesign/ata-plan-and-design.html      
  - name: Intune
    href: /InTune/
    homepage: /InTune/index.html
    items:
      - name: Understand and explore
        href: /Intune/Understand/
        homepage: /Intune/Understand/ways-to-do-enterprise-mobility.html
      - name: Deploy and use
        href: /Intune/DeployUse/learn-how-to-deploy-a-solution-for-protecting-company-email-and-documents.html
        homepage: 
``` 

This is a yaml format file and the breadcrumb data are organized in a parent-child relationship, this relation specifies a logic navigation path for the site. In the above example, there is a path of `Enterprise Mobility -> Advanced Threat Analytics -> Plan and Design`. There are also three types of input in the yaml file:
* `name` - The display text that shows up on the breadcrumb 
* `href` - This is the URL part to detect which breadcrumb node to match. For example, if current open page is `http://docs.microsoft.com/ATA/Understand/samplefile.html`, then it will look up the breadcrumb source and figured out that this page is under 'ATA -> Understand and Explore'. Then the node will be highlighted. 
* `homepage` - This is a URL that leads to a landing page after user click the breadcrumb node.

##Where to put the breadcrumb source file
Unlike TOC.md, the breadcrumb source file could be put into a different docset or even in a different repo. That is because breadcrumb is usually a global navigation concept and links different docsets and repos. So you could put the toc.yml file under any OP provisioned docset. For example, I could put the toc.yml file under the root folder of docset EM, whose base url is /EM/. After build the docset, user could verify the built breadcrumb data via `http://{SiteDomain}/EM/toc.json`.  

##How to reference the breadcrumb source file
It is a common scenario that different docsets need to reference the breadcrumb file from another repo. This referencing relationship is configured in the docfx.json file as a global metadata:

```json
    "globalMetadata": {
      "layout": "Conceptual",
      "breadcrumb_path": "/EM/toc.json",
      "ms.locale": "en-us"
    }
```
User need to set the breadcrumb_path as a globalMetadata so that current docset will pull breadcrumb data from specified location, in this case, is /EM/toc.json.

##Why the breadcrumb does not show on my page?
1. Please view your page source to check if there is a breadcrumb_path metadata in the page source. If yes, check if the path filled with expected location. 
2. If there is no breadcrumb_path metadata, please check if the breadcrumb_path is added as global_metadata in docfx.json in your repo
3. If everything above is correct, please double check the breadcrumb source file to see if the href is set correctly 
4. Report issue on //MSDNHelp

 
