PROCESSWIRE 2.1 TEMPLATES
=========================

The files in this directory correspond with the templates list in ProcessWire admin. Template files are just
PHP files that output markup. They may also be just basic HTML files (with a .PHP extension). Every page in
the site is assigned to one of the template files in this directory. 

These template files typically comprise the majority of what makes your site unique from any other 
ProcessWire installation. In keeping with this approach, you'll also see '/scripts/' and '/styles/' 
directories within this templates directory, and they contain the site's javascript and CSS files. Though 
that is stylistic only, you could certainly place them whenever you wanted.

Templates have full unrestricted access to the ProcessWire API and typically use it for finding pages and 
referencing their properties for output. If desired, templates may go further than this and call upon other 
web applications or anything else that you might do with PHP. 

Every template is supplied with a $page object that refers to the current page being viewed. This $page 
object is locally scoped to the template file, so the only thing you need to do to access it is just 
directly refer to it in your PHP code.  For instance, if you wanted to echo the page's $title field
from your template, you would do the following:

<?php echo $page->title; ?>

or short syntax (if supported by your web host): 

<?=$page->title?>

And likewise for any other fields assigned to the template. Though some fields require more, like 
files, images, page references and the like -- please see the documentation at processwire.com/api/ 


LOADING OTHER PAGES FROM YOUR TEMPLATE
======================================

Templates are also supplied with a $pages object that provides capability for loading and finding other pages. 
The most common methods used in that object are get() and find(), both of which take a string selector to 
locate and return pages. The only difference between them is that get() always returns 1 page, and find() 
returns a PageArray. Below are examples:

// find all pages using the skyscraper template
$skyscrapers = $pages->find("template=skyscraper"); 

// find all skyscrapers with a height greater than 500 ft, and less than or equal to 1000 ft. 
$skyscrapers = $pages->find("template=skyscraper, height>500, height<=1000"); 

// find all skyscrapers in Chicago with 60+ floors, sorted by floors ascending
$skyscrapers = $pages->get("/cities/chicago/")->children("floors>=60, sort=floors"); 

// find all skyscrapers built before 1950 with 10+ floors, sorted by year descending, then floors descending
$skyscrapers = $pages->find("template=skyscraper, year<1950, floors>=10, sort=-year, sort=-floors"); 

// find all skyscrapers by architects David Childs or Renzo Piano, and sort by height descending
$david = $pages->get("/architects/david-childs/"); 
$renzo = $pages->get("/architects/renzo-piano/"); 
$skyscrapers = $pages->find("architect=$david|$renzo, sort=-height"); 

// find all skyscrapers that mention the words "limestone" and "granite" somewhere in their body copy. 
$skyscrapers = $pages->get("/cities/")->find("template=skyscraper, body~=limestone granite"); 

// find all skyscrapers that mention the phrase "empire state building" in their body copy. 
$skyscrapers = $pages->find("template=skyscraper, body*=empire state building"); 


INCLUDING A TEMPLATE FROM ANOTHER TEMPLATE
==========================================

When you include a template from another template, use the following syntax:

	include("./my-template.php"); 

Do NOT use this syntax:

	include("my-template.php"); 

The difference between the second [incorrect] example and the first [correct] example is that the first 
example starts with: "./". This tells PHP to look in the current directory. Whereas if you omit that part,
PHP will search your include path, which could result in an error, or even worse, include the wrong file.
So just remember to always precede your included files with "./". 


MORE INFORMATION
================

The information in this file is very brief. Please see the official documentation at: 
http://processwire.com/api/

Also, join the ProcessWire forum and we're always glad to assist with any questions you have:
http://processwire.com/talk/ 

