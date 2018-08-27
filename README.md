New Framework: a Schema Driven UI
=================================

By Mark Qian 8/2018 (markqian@hotmail.com)

<b>A. Introduction:</b><br/> 
A Schema-driven UI: I am not the first one doing this but happened to have the similar idea with what others had:<br/>
<ul>
  <a href="https://medium.com/@hintology/sdd-schema-driven-development-f1d232d73ea6" target=_blank>SDD — Schema Driven Development</a><br/>
  <a href="https://github.com/mozilla-services/react-jsonschema-form" target=_blank>react-jsonschema-form</a><br/>
  ...
</ul>
The "thing" to be driven by schema is view renderers. Many people accept using a renderer for a table but very few develops/architects do the same thing for another majority type of view, form.  People keep writing html tags for forms redundantly. <b>We should think about this in a different way</b>: the form info (schema) is the input data of form renderer instead of html codes. In my project, each type of view such as form, table, D3 diagram has a renderer.
<br/></br/>
Here is the <b>flow of schema driven</b> in my approach:<br/><br/>
<ul>
  <div><b>1. Models delivered by server</b> (either generated from model-driven server side or given memually to UI).<br/>
      <ul>
        <p> Models defined by server contain: a field list where each field has attributes like name, data type and validation info like the following:<br/>
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
      },
      "Teacher":{
        "fields": [
          {"name":"id", "type":"string", "validate":[]},
          {"name":"name", "type":"string", "validate":["required"]},
            ...
        ]  
      },
      "Course":{
        "fields": [
          {"name":"id", "type":"string", "validate":[]},
          {"name":"name", "type":"string", "validate":["required"]},
            ...
        ]  
      },
      "Campus":{
        "fields": [
          {"name":"id", "type":"enum", "validate":[], "typeMap":{"0":"Hayward", "1":"San Jose", "2":"SF"},
          {"name":"name", "type":"string", "validate":["required"]},
          {"name":"address", "type":"string", "validate":["required"]},  
          {"name":"totalStuden", "type":"int", "validate":[]},  
            ...
        ]  
      }
</pre> 
        </p>
      </ul>
  </div>
  <div><b>2. UI use the models from server as "super" classes to generate "schemas"</b>.
    <ul>
        <p> A schema contains more UI related info besides info in its model: formType, tableType, renderStle and so on. This "schema" work as a primitive UI image for that component/field, like the following:<br/>
<pre>
    {
      "Student":{
        "fields": [
          {"name":"id", props:{"formType":"Hidden", "tableType":"Hidden"}},
          {"name":"name", props:{"formType":"Input", "tableType":"text"}},
          {"name":"age", props:{"formType":"Input", "tableType":"text"}},
            ...
        ]  
      }
</pre>
      The framework will generate a "default" schema for each model while the props specified in schema above overwrites props in generated default props. So if no specified in schema, defaults will be applied like "formType":"Input" and "tableType":"text".
      </p>
      </ul>
  </div>
  <div><b>3. UI defines "views", as instances of schemas, to be used by each individual screen out of "schemas" above.</b>
    <ul>
        <p> A schema can be used in many views and a view may use different fields from different schemas. In many of our screen, a "visual form" could consist of fields from different server model  objects. For example, you may want to show couple "forms" on your page with fields like student name, student favor course, student campus address, like the following:<br/>
<pre>
    {
      "StudentView":{
        "fieldList": [
          {"path":"Student.name"},
          {"path":"Student.id"},
          {"path":"Course.name", props:{"label":"Most frequently taking course"}},
          {"path":"Campus.name", props:{"typeList":<b>["1", "2", "0"]</b>}},
            ...
        ]  
      },
      "TeacherView":{
        "fieldList": [
          {"path":"Teacher.name"},
          {"path":"Student.name", props:{"label":"Favor Student"}},
          {"path":"Course.name", props:{"label":"Most frequently involved course"}},
          {"path":"Campus.name", props:{"label":"Closest campus", "typeList":<b>["0", "2", "1"]</b>}},
            ...
        ]  
      },
      //Nested View
      "CombinedView": {
        "fields": [
          {"name":"studenView", props:{"schemaName":"StudentView"}},
          {"name":"teacherView", props:{"schemaName":"TeacherView"}},
            ...
        ]  
      }
</pre>
      As you can see above, fields in each view definition will overwrite the props with the same name in the "schema" so that each view can have its own characters. For example, "StudentView" and "TeacherView" both contain "Campus.name" but each wants to display the campus names in its own order so they use "typeList" to tell the order differently. View can be nested like "CombinedView" above
      </p>
      </ul>
  </div>
<a name="UIRendersViews"></a>
<div><b>4. UI Renders Views</b>. 
    <ul>
        <p> My framework provides a variety of renderers like Form, Table, D3Canvas, LineChart and so on. In this way, it is much easy to apply systematic approaches like validation, submission, data loading. For example, for most "regular" forms, there is not codes are needed to load and submit data since the framework will introspect the "fieldList" in views above to obtain what need to be loaded and submitted: for "TeacherView", the framework needs to load data from model/object Teacher, Student and Campus and similarly when submiting.
      </p>
      </ul>
  </div>
<a name="UIHandlingApplicationLogic"></a>
<div><b>5. UI Handling Application Logic</b>. 
    <ul>
        <p> Any application built with my framework is a container containing isolated "Objects" (UI views and service). This objects has no  knowledge about others or the "application logic". For example, let's take a look at a navigation view, HeaderTab:
<pre>
      "HeaderTab":{
        "fields": [
          {"name":"StudentTab", "props":{"formType":"Button", "<b>route</b>":{"viewType":"Screen"}}},
          {"name":"TeacherTab", "props":{"formType":"Button", "route":{"viewType":"Screen"}}},
          {"name":"CampusTab", "props":{"formType":"Button", "route":{"viewType":"Dialog"}}},
            ...
        ]  
      }
</pre> 
      As you can see above, there is only a "route" attribute that includes no info about what to do after "StudentTab" is clicked! This is key of my design: <b>no appliaction logic resides in codes!</b>. The application logic will be loaded as data at runtime in json file as following:
<pre>
  "Route":{
      "HeaderTab.StudentTab":"StudentView",
      "HeaderTab.TeacherTab":"TeacherView",
      "HeaderTab.CampusTab":"CampusTabView",
        ... 
  }
</pre>
      The key of the map above is the unique id of each field such as "HeaderTab.StudentTab" and the value is the unique name of the view
      </p>
      </ul>
  </div>
<a name="EachFieldHandleSpecialInteraction"></a>
<div><b>6. Each Field Handle Special Interaction</b>. 
    <ul>
        <p> Each field may have some special need to send or received event/data. So Pub/Sub is now in place. For example, when the field "Campus.name" in "StudentView" is changed, we want to give "CanpusView" a chance to update its "Canpus.totalStuden":
<pre>
    {
      "StudentView":{
        "fieldList": [
          {"path":"Student.name"},
          {"path":"Student.id"},
          {"path":"Course.name", props:{"label":"Most frequently taking course"}},
          {"path":"Campus.name", props:{"typeList":["1", "2", "0"], "<b>pub</b>":{"type":"/Updated/StudentView/Campus.name", {"event":"change"}}},
            ...
        ]  
      },
      "CanpusView":{
        "fieldList": [
          {"path":"Canpus.name"},
          {"path":"Canpus.totalStuden", props:{"label":"Total Number of Student"}},
            ...
        ],
        "props":{
            "<b>sub</b>":{"type":"/Updated/StudentView/Campus.name", "handler":function() {
              //make update here
              
            }            
        }
      }
</pre>   
As you can see above, field "Campus.name" register a topic "/Updated/StudentView/Campus.name" for an event of "change" and "CanpusView" subscribe the topic at view level and then handle the update there.
      </p>
      </ul>
  </div>


(More coming soon)
