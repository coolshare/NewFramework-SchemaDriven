New Framework: a Schema Driven UI
=================================

By Mark Qian 8/2018 (markqian@hotmail.com)

<b>A. Introduction:</b> 
A Schema-driven UI: I am not the first one doing this but happened to have the similar idea with what others had:<br/>
<ul>
  <a href="https://medium.com/@hintology/sdd-schema-driven-development-f1d232d73ea6" target=_blank>SDD — Schema Driven Development</a><br/>
  <a href="https://www.npmjs.com/package/react-schema-u" target=_blank>What is React Schema UI</a><br/>
  ...
</ul>
The "thing" to be driven by schema is view renderers. Many people accept using a renderer for a table but very few develops/architects do the same thing for another majority type of view, form.  People keep writing html tags for forms redundantly. We should think about this in a different way: the form info (schema) is the input data of form renderer instead of html codes. In my project, each type of view such as form, table, D3 diagram has a renderer.
<br/></br/>
Here is the flow of schema driven in my approach:<br/>
<ul>
  <div>1. models delivered by server (either generating in case of model-driven or memually give to UI).<br/>
      <ul>
        <p> A model defined by server should contain: field list where each field has attributes like name, data type and validation info like the following:<br/>
<pre>
          {
            "Student":{
              "fields": [
                {"name":"name", "type":"string", "validate":["required"]},
                {"name":"age", "type":"int", "validate":["required", "int"]},
                {"name":"campus", "type":"enum", "validate":["required", "int"], "typeMap":{"0":"Hayward", "1":"San Jose", "2":"SF"},
                  ...
              ]  
            }
</pre>
        
        </p>
      </ul>
  </div>
  <div>2. UI use the models from server as "super" classes to generate "schemas".
    <ul>
        <p> A schema contains more UI related info besides info in its model: formType, tableType, renderStle and so on. This "schema" work as a primitive UI image for that component/field, like the following:<br/>
<pre>
          {
            "Student":{
              "fields": [
                {"name":"name", props:{"formType":"Input", "tableType":"text"}},
                {"name":"name", props:{"formType":"Input", "tableType":"text"}},
                {"name":"campus", props:{"formType":"Select", "tableType":"text", "typeList":["2", "0", "1"]}},
                  ...
              ]  
            }
</pre>
      </p>
      </ul>
  </div>
  <div>3. UI defines "views", as instances of schemas, to be used by each individual screen out of "schemas" above.
    <ul>
        <p> A schema can be used in many views and a view may use different fields from different schemas. In many of our screen, a "visual form" could consist of fields from different server model  objects. For example, you may want to show a "form" on your page with fields like student name, student favor course, student favor teacher.  </p>
      </ul>
  </div>
</ul>

<b>B. Problem:</b><br/>
As web software developers, our job is to automate web experience to make web users's life easier. But what about the life of ourselves: the web developer's own life: how much do we apply the same automation back to our own coding?<br/> 
For example, why do we need to repeat coding/maintain similar page over and over? Let's take a concrete case on forms, views used to collect user inputs. Forms are one of most frequently used views in web applications. Forms are very similar: they contain fields, styles, and related functions like loading, submission, validation and son on. Since all related functions can be shared so coding a form mainly is coding similar html tags and style them.<br/><br/>
But <b>why do we need to hard coding the html tags ourselve instead of automating them?</b> 

<b>C. Solution:</b><br/>
We should think about coding a form in a different way: form info (form schema) such as fields and styles are data to be consumed by form renderer so that is no coding to build a form. Instead, the job of engineers is to provide form info (form schema) to the form renderer and the rest is the form renderer's job to show the view.    


(Under construction)
