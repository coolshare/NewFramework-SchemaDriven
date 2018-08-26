New Framework: a Schema Driven UI
=================================

By Mark Qian 8/2018 (markqian@hotmail.com)

<b>A. Introduction:</b> 
A Schema-driven UI: I am not the first one doing this but happened to have the similar idea with what others had:<br/>
<ul>
  <a href="https://medium.com/@hintology/sdd-schema-driven-development-f1d232d73ea6" target="_blank">SDD — Schema Driven Development</a><br/>
  <a href="https://www.npmjs.com/package/react-schema-u" target="_blank">What is React Schema UI</a><br/>
  ...
</ul>
The "thing" to be driven by schema is view renderers. Many people accept using a renderer for a table but very few develops/architects do the same thing for another majority type of view, form.  People keep writing html tags for forms redundantly. We should think about this in a different way: the form info (schema) is the input data of form renderer instead of html codes. In my project, each type of view such as form, table, D3 diagram has a renderer.
<br/></br/>
Here is the flow of schema driven:<br/>



<b>B. Problem:</b><br/>
As web software developers, our job is to automate web experience to make web users's life easier. But what about the life of ourselves: the web developer's own life: how much do we apply the same automation back to our own coding?<br/> 
For example, why do we need to repeat coding/maintain similar page over and over? Let's take a concrete case on forms, views used to collect user inputs. Forms are one of most frequently used views in web applications. Forms are very similar: they contain fields, styles, and related functions like loading, submission, validation and son on. Since all related functions can be shared so coding a form mainly is coding similar html tags and style them.<br/><br/>
But <b>why do we need to hard coding the html tags ourselve instead of automating them?</b> 

<b>C. Solution:</b><br/>
We should think about coding a form in a different way: form info (form schema) such as fields and styles are data to be consumed by form renderer so that is no coding to build a form. Instead, the job of engineers is to provide form info (form schema) to the form renderer and the rest is the form renderer's job to show the view.    


(Under construction)
