#Get Your Hair Wet

##Table of Contents
* [Description](#description)
* [Interface Design](#design)
* [Technical Design](#technical-design)

#Description

This is the source code of the [Get Your Hair Wet website](http://getyourhairwet.net) which will now be refered to as the site.

#Design
There are two parts to the website, the user facing content, and the 
administrator/editor interface. The administrator/editor interface runs a CMS (content management system). The CMS allows editors to easily create new pages in the website. There are 2 types of pages that 
editors can create. The first type is the article page, an article page has a title, description, and a body. The body of the article is a richtext box 
input. This gives editors more freedom in the formatting of their article. All articles will appear under the resources tab of the site. The other 
type of page that an editor can create is a basic-page. A basic page is very similar to an article. The only difference is that an editor can specify 
what slug to publish their page on. More information about the editer interface can be found 
[here](http://wagtail.readthedocs.org/en/v1.4.3/editor_manual/index.html).

The user facing side has several features. Users can create accounts for the website. The registration process asks for basic information. After submitting 
this information, the site will send an email to the user with a link to allow them to activate their user profile. This was done, so that people wouldn't 
create profiles for someone that didn't want one. Users can also register a chapter. A chapter is a small group of girls that can set up events for 
their chapter.

#Technical Design
The site uses the [django](https://docs.djangoproject.com/en/1.9/) framework. The CMS is [wagtail](http://wagtail.readthedocs.org/en/v1.4.3/)
When a user creates a chapter, the chapter is tied to that user, so one the database, there is a foreign key called chapter_owner_id that points to the id 
of the currently logged in user. There is a similar mechanism for events, except that events have a foreign key towards a chapter.