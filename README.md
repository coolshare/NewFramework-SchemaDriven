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
          {"name":"id", "type":"string", "validate":[]},
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
          {"name":"id", props:{"formType":"Hidden", "tableType":"Hidden"}},
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
        <p> A schema can be used in many views and a view may use different fields from different schemas. In many of our screen, a "visual form" could consist of fields from different server model  objects. For example, you may want to show couple "forms" on your page with fields like student name, student favor course, student campus address, like the following:<br/>
<pre>
    {
      "StudentView":{
        "fieldList": [
          {"path":"Student.name"},
          {"path":"Student.id"},
          {"path":"Course.name", props:{"label":"Most frequently taking course"}},
          {"path":"Campus.address", props:{"typeList":["1", "2", "0"]}},
            ...
        ]  
      },
      "TeacherView":{
        "fieldList": [
          {"path":"Teacher.name"},
          {"path":"Student.name", props:{"label":"Favor Student"}},
          {"path":"Course.name", props:{"label":"Most frequently involved course"}},
          {"path":"Campus.address", props:{"label":"Closest campus", "typeList":["0", "2", "1"]}},
            ...
        ]  
      }
</pre>
      </p>
      </ul>
  </div>
</ul>
As you can see above, fields in each view definition will overwrite the props with the same name in the "schema" so that each view can have its own characters.


(Under construction)
