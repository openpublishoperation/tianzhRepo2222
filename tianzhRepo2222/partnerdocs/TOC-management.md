# TOC creation and management #

**TOC.md** is used to define the Table of Contents (TOC) structure of a docset. The TOC is described in Markdown format.

We use Markdown headers to specify the level of the TOC. For example:
 ```markdown
# Tutorial
## Step 1
## Step 2
## Step 3
```

The above example illustrates a parent topic "Tutorial" with three children Step 1-3.

We use standard Markdown link syntax to specify the target topic of the toc node. For example:
  ```markdown
 # [Tutorial](tutorial.md)
 ## [Step 1](step-1.md)
 ## [Step 2](step-2.md)
 ## [Step 3](step-3.md)
```

If a toc node is not a link, it will become a container node: it can contain children and it will be just a expanding/collapsing node.

## Important information ##

-  The TOC for Open Publishing is a self-contained TOC not integrated into the global MSDN/TN TOC.
-  You can use an external link to connect the Open Publishing TOC to your MSDN/TN Global TOC.
-  Since Markdown only supports 6 levels of header, we'll only support 6 levels of TOC for now. This can be extended in the future.
-  You cannot reference a file outside a docset/folder. 
- TOC.md cannot contain arbitrary Markdown content. For example, you cannot have images in it. All content that are not headers will lead to build error.

## Localized TOC ##
Localized TOC is maintained in sync with English via the handoff and handback process. TOC.md will be included in the handoff package. 
