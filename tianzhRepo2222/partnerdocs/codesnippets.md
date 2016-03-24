# Code Snippets
Inline code snippets, coloring, language selector, and external codesnippets are now supported in OP.

Example

Click on Contribute to this topic link to see the content in MD:


## 1. Internal code snippets

`To be documented.`

## 2. External code snippets

You can reference code snippets stored in your repo by using the code language specified. The content of specified code path will be expanded and included in your file.

We don’t have restrictions on the folder structure of code snippets. You should just manage the code snippets as normal source code.

Syntax:
```md
[!code-<language>[<name>](<codepath><queryoption><queryoptionvalue> "<title>")]
```

* __`<language>`__ can be made up of any number of character and '-'. However, the recommend value should follow [Highlight.js language names and aliases](http://highlightjs.readthedocs.org/en/latest/css-classes-reference.html#language-names-and-aliases).
* __`<codepath>`__ is the relative path in file system which indicates the code snippet file that you want to expand.
* __`<queryoption>`__ and __`<queryoptionvalue>`__ are used together to retrieve part of the code snippet file in the line range or tag name way. We have 2 query string options to represent these 2 ways:
    * __`#`__: _`#L{startlinenumber}-L{endlinenumber}`_ (line range) or _`#L{tagname}`_ (tag name)
    * __`?`__: _`?start={startlinenumber}&end={endlinenumber}`_ (line range) or _`?{name}={tagname}`_ (tag name)
* __`<title>`__ can be omitted.

#### Code Snippet Sample
```md
[!code-csharp[Main](Program.cs)]

[!code[Main](Program.cs#L12-L16 "This is source file")]
[!code-vb[Main](../Application/Program.vb#testsnippet "This is source file")]

[!code[Main](index.xml?start=5&end=9)]
[!code-javascript[Main](../jquery.js?name=testsnippet)]
```

#### Tag Name Representation in Code Snippet Source File
DFM currently only supports following __`<language>`__ values to be able to retrieve by tag name:
* C#: cs, csharp
* VB: vb, vbnet
* C++: cpp, c++
* F#: fsharp
* XML: xml
* Html: html
* SQL: sql
* Javascript: javascript 

##3. Tabbed code snippets
This works for both inline and external code snippets. You can have multiple samples grouped together so the user can see them in different tabs. 

Example:

````markdown
> [!div class="tabbedCodeSnippets"]
```cs
var outlookClient = await CreateOutlookClientAsync("Calendar");
var events = await outlookClient.Me.Events
  .Take(10)
  .ExecuteAsync();
foreach(var calendarEvent in events.CurrentPage)
{
  System.Diagnostics.Debug.WriteLine("Event '{0}'.", calendarEvent.Subject);
}
```
```javascript
outlookClient.me.events.getEvents().fetch().then(function (result) {
    result.currentPage.forEach(function (event) {
console.log('Event "' + event.subject + '"')
    });
}, function(error) {
    console.log(error);
});
```
````

Will be rendered as:

> [!div class="tabbedCodeSnippets"]
```cs
var outlookClient = await CreateOutlookClientAsync("Calendar");
var events = await outlookClient.Me.Events
  .Take(10)
  .ExecuteAsync();
foreach(var calendarEvent in events.CurrentPage)
{
  System.Diagnostics.Debug.WriteLine("Event '{0}'.", calendarEvent.Subject);
}
```
```javascript
outlookClient.me.events.getEvents().fetch().then(function (result) {
    result.currentPage.forEach(function (event) {
console.log('Event "' + event.subject + '"')
    });
}, function(error) {
    console.log(error);
});
```
