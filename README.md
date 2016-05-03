#Get Your Hair Wet

##Table of Contents
* [Description](#description)
* [Interface Design](#design)
* [Accounts](#accounts)
* [About](#about)
* [Chapters](#chapters)
* [Events](#events)
* [Community](#community)
* [Resources](#resources)
* [Profile](#profile)
* [TODO](#todo)

#Introduction
The purpose of this report is to provide information as to why getyourhairwet.net was created, how it should be utilized, how it was created, and what needs to be done to complete the site. This is the source code of the [Get Your Hair Wet website](http://getyourhairwet.net) which will now be refered to as the site.

#Background
Amy Poehler’s Smart Girls is headed by Amy Poehler, Meredith Walker, and Amy Miles. Smart Girls’ mission is to encourage girls to break the mold of typical stereotypes, do things that people tell them they can’t, and show the world the tenacity that they have. The organization wants to empower young girls. 

The Get Your Hair Wet website is a tool to support the organization’s cause. The site provides the ability to create groups called “chapters” to build community and give girls with similar interests and motives a platform to communicate, share ideas, and act on their interests.

#Technical Design
[Wireframe](https://docs.google.com/presentation/d/1Nzin20_Po3kQ131UeRfnf6yuyJdUHwQHw17cuwMW-6U/edit?usp=sharing) on Google Slides

The site uses the [django](https://docs.djangoproject.com/en/1.9/) framework. The content management system (CMS) is [wagtail](http://wagtail.readthedocs.org/en/v1.4.3/)
When a user creates a chapter, the chapter is tied to that user, so one the database, there is a foreign key called chapter_owner_id that points to the id 
of the currently logged in user. There is a similar mechanism for events, except that events have a foreign key towards a chapter.

#Overview
This section describes each portion of the site in detail.

###Accounts
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

###About
(Design overview here)

###Chapters
Chapters are groups of girls who have similar interests or missions. Chapters are supposed to provide a community for girls to interact, learn, and grow from and with. In order to form a Chapter a user must visit the "create" tab under Chapters. The Chapter must have at least three members in order to be created. Chapters must also have a title, description, neighborhood, city, state, list of users who are members, whether or not the chapter has been approved, a private latitude and longitude used for putting the Chapter on the map on "Find Chapters", list of users who are admins, a list of chapter events, and an optional image. Users are also able to find chapters via a map or keyword searches.

###Chapters Technical Overview
To create a chapter, a person must be registered as a user. A user must also specify at least two other registered users in order to create the chapter, however this has not been enforced yet in our implementation. When an chapter is created an entry is created in the database following the Chapter model(chapters/models.py) which includes the fields listed in the non-technical description. The Chapters front-end includes a Google map with the lat, longs of the events as markers. It also includes an HTML form for searching through the events as well as a scrollable list of Chapters. Currently users are able to click on a Chapter and the map will center on the location. Users can also hover over the markers on the map and the corresponding event will be highlighted. One problem (which is also true for events) is that the markers are currently at the exact lat, longs. We would like them to be small circles so to protect the privacy of the users. Something similar to what we want can be found on Airbnb's website when looking at the map for a property. This should be possible using Google maps API. Currently not implemented (also true for events), we would like to be able to allow a user to click on the "Join" button and which would be sent to the Chapter admins for approval. The HTML and Javascript can be found in chapters/templates/chapters and the CSS can be found in chapters/static/css.

###Events
Events are created by members chapters to hold chapter meetings or to attend a function such as a volunteering event. Events have a title, public location (such as zipcode - seen by anybody), private location (the actual address - seen by users who RSVP), owning chapter, start date and time, end date and time, description, list of users who are attending, list of admins (users who can edit the event), whether or not the event has been approved, a private latitude and longitude used for putting the Chapter on the map on "Find Events", and an optional image. Users are also able to find events via a map or keyword searches.

###Events Technical Overview
To create an event, a user must be logged in and part of a chapter. When a user creates and event, they must choose a chapter for the event to belong to. When an event is created via the form on the "Create" tab under events, an entry is created in the database following the Event model(events/models.py) which includes the fields listed in the non-technical description. Also note that you can access the chapter, but it does not show up in the event model because it is a ManyToMany field in chapters/models.py. Currently the lat, long has the same issue with the Google map as noted in the Chapters Technical Overview. On the front-end Events are set up almost exactly the same way as Chapters. There is a Google map on the right and on the left there is a search form and a list of cards containing each event detail and a join button. The HTML and Javascript can be found in events/templates/events/ and the CSS can be found in events/static/css.

###Community
The site has basic message board functionality under a tab called Community. This was designed to provide smart girls users with a place to share ideas online and ask questions in a safe and positive environment. In the design phase of this project, posts had the ability to be 'starred' to promote the post to the top of the message board. We decided to hide this feature in order to prevent posts from enabling popularity contests among users. Instead, this star functionality will 'favorite' the post for the user only. The number of stars a post has received may also influence the ranking of posts on the back-end only. Currently, users are able to create posts, search for keywords within posts, and filter posts by clicking on tags.

###Community Technical Overview
The post is implemented using a Django ModelForm and may be found in ForumView called Thread. It may be beneficial to extend a Wagtail article for easier indexing, searching, and moderation by admins. Code is found in 'forum' folder. 

###Resources
Resources are used to give girls tools to learn. An example of resources include tool kits that Smart Girls provides that range from "how to change a tire" to "how to adopt a pet". Resources are essentially articles that staff can create.
To create one, you must log in with a staff account (admin, moderator, or editor) and go to the resources tab. Then you
click on the bird on the bottom right of the page and click on "Add a child page" this will take you to the admin interface
where you can create and article by providing a title, intro, and body.

###Resources Technical Overview
Resources were implemented as Article objects in the backend. An Article is an extension of a wagtail Page. This way it can
be easily indexed. Besides the Page fields, Articles have a date, which is automatically written whenever an Article is created or modified, an intro (250 length character field), and a body (a wagtail richtext field).

###Profile
The site will have a simple profile page with the following features:
* Edit personal information
* Add profile picture
* See active chapters
* Set reminders for events attending
* View past events

#Recommendations and TODO
###Community
* Restrict message board to logged-in users
* Restrict message board by chapter
* Implement reply for posts
* Use foreign key to associate posts and replies with users
* Make messages clickable
* Save 'starred' posts for users and display them as filter
* The ability to 'report' a user, Event, Chapter, or message
* Implement the need for three users to create a Chapter
* Add optional images to Events and Chapters
* "Join" button sends message to Chapter/Event admins for approval for Chapters and Events

###Profile
* Need to implement

#Conclusion
We hope the site will provide Get Your Hair Wet the platform to empower girls worldwide. The site offers an abundance of resources to help the organization with its laudable mission. 
