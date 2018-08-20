New Framework: a Schema Driven UI
=================================

By Mark Qian 8/2018 (markqian@hotmail.com)

<b>A. The demo page:</b> 

http://coolshare.github.io/NewFramework-SchemaDriven/

<b>B. Introduction:</b><br/>
As web software developers, our job is to automate web access experience to make web users's life easier. But what about the life of ourselves, the web developer's own life? Why do we need to repeat coding/maintain similar page over and over? Why can't we treat structure (fields in a view) of UI views like form (fields in the form, the schema of the form) as data to a view(form) renderer instead of hard coding them to build views?<br/><br/>
<b>C. Problem:</b><br/>
In most of "regular" web applications, pages are constructed "concretely" with concrete html tags. For example, there may be many form views to collect data in your app and you normally build individual form view concretely using html tags where you specify a list of fields (a label and an input field) and a submit button/function. When you need another form, you normally recreate (or even clone and modify) another similar form with similar tags. After a while when your app reach certain size, you will see most of you views appear similar or redundant in term of fields (labels and inputs). <br/><br/>

Here are the problems with concrete coding:<br/>
<ul><li>The concrete coding for each page require concrete coding and maintenance on each page
</ul>


