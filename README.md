New Framework: a Schema Driven UI
=================================

By Mark Qian 8/2018 (markqian@hotmail.com)

<b>A. The demo page:</b> 

http://coolshare.github.io/NewFramework-SchemaDriven/

<b>B. Introduction:</b><br/>
As web software developers, our job is to automate web experience to make web users's life easier. But what about the life of ourselves, the web developer's own life: how much do we apply the same automation back to our own coding?<br/> 
For example, why do we need to repeat coding/maintain similar page over and over? Let's take a concrete case on forms, views used to collect user inputs. Forms are one of most frequently used views in web applications. Forms are very similar: they contain fields, styles, and related functions like loading, submission, validation and son on. Since all related functions can be shared so coding a form mainly is coding similar html tags and style them.<br/><br/>
But <b>why do we need to hard coding the html tags ourselve instead of automating them?</b> We should think about coding a form in a different way: form info such as fields and styles are data to be consumed by form renderer so that is no coding to build a form. Instead, the job of engineers is to provide form info (form schema) to the form renderer and the rest is the form renderer's job to show the view.    

<b>C. Problem:</b><br/>
In most of "regular" web applications, pages are constructed "concretely" with concrete html tags. For example, there may be many form views to collect data in your app and you normally build individual form view concretely using html tags where you specify a list of fields (a label and an input field) and a submit button/function. When you need another form, you normally recreate (or even clone and modify) another similar form with similar tags. After a while when your app reach certain size, you will see most of you views appear similar or redundant in term of fields (labels and inputs). <br/><br/>

Here are the problems with concrete coding:<br/>
<ul><li>The concrete coding for each page require concrete coding and maintenance on each page
</ul>


