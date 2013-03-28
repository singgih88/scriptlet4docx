# Welcome to Scriptlet4Docx project
This project allows you to use [Groovy](http://groovy.codehaus.org/) template scriptlets inside a docx-document. Template document may be created directly from MS Word. All document styles will be preserved.

## Usage
1. Add scriptlet4docx maven dependency to your project [com.github.snowindy:scriptlet4docx](http://mvnrepository.com/artifact/com.github.snowindy/scriptlet4docx).
2. Add [Groovy scriptlets](http://groovy.codehaus.org/Groovy+Templates) to your docx-document.
3. Generate binding parameters to fill the template: Map&lt;String, Object&gt;.
4. Use docxTemplater.process() process method to generate result docx.

## Available scriptlet types

1. ```${contract.number}```
2. ```<%= contract.number %>```
3. ```<% out.print('This is your first contract!'); %>```
4. ```$[ @person.name ]```

## Scriptlet types explanation
### ${ data }
Equivalent to ```out.print(data)```
### &lt;%= data %&gt;
Equivalent to ```out.print(data)```
### &lt;% any_code %&gt;
Evaluates containing code. No output applied.
May be used for divided conditions:

```
<% if (cond) { %>
This text block will be printed in case of "cond == true"
<% } else { %>
This text block will be printed otherwise.
<% } %>
```
### $[ @listVar.field ]
This is a custom Scriptlet4docx scriptlet type designed to output collection of objects to docx tables. It must be used inside a table cell.

Say, we have a list of person objects. Each has two fields: 'name' and 'address'. We want to output them to a two-column table.

1. Create a binding with key 'personList' referencing that collection.
2. Create a two-column table inside a template docx-document: two columns, one row.
3. ```$[@person.name]``` goes to the first column cell; ```$[@person.address]``` goes to the second.
4. Voila, the whole collection will be printed to the table.

## Live template example 
You can check all mentioned scriptlets usage in a [demonstration template](https://github.com/snowindy/scriptlet4docx/raw/master/documentation/examples/template-example.docx).

## Code example
```
HashMap<String, Object>	params = new HashMap<String, Object>();
params.put("name", "John");
params.put("sirname", "Smith");

DocxTemplater docxTemplater = new DocxTemplater(new File("path_to_docx_template/template.docx"));
docxTemplater.process(new File("path_to_result_docx/result.docx"), params);
```

## History
0.6.2 fixed [issue#1](https://github.com/snowindy/scriptlet4docx/issues/1)

## Licence
Licenced under [The (New) BSD License](http://www.opensource.org/licenses/bsd-license.php).

## Authors and Contributors
Eugene Sapozhnikov (@snowindy).


[![githalytics.com alpha](https://cruel-carlota.pagodabox.com/0383d29cb8a1af9f9b8fc569d130fc25 "githalytics.com")](http://githalytics.com/snowindy/scriptlet4docx)