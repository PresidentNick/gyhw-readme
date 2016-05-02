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

#Design
[Wireframe](https://docs.google.com/presentation/d/1Nzin20_Po3kQ131UeRfnf6yuyJdUHwQHw17cuwMW-6U/edit?usp=sharing) on Google Slides

#Technical Overview
The site uses the [django](https://docs.djangoproject.com/en/1.9/) framework. The content management system (CMS) is [wagtail](http://wagtail.readthedocs.org/en/v1.4.3/)
When a user creates a chapter, the chapter is tied to that user, so one the database, there is a foreign key called chapter_owner_id that points to the id 
of the currently logged in user. There is a similar mechanism for events, except that events have a foreign key towards a chapter.

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
Chapters are groups of girls who have similar interests/motives. Chapters are supposed to provide a community for girls to interact, learn, and grow from and with. Chapters are meant to be a group of at least three girls. The group meets at a location of their discretion.

###Chapters Technical Overview
To create a chapter, a person must be registered as a user. 

###Events
Events belong to chapters.

###Events Technical Overview
(Technical overview here)

###Community
The site has basic message board functionality under a tab called Community. This was designed to provide smart girls users with a place to share ideas online and ask questions in a safe and positive environment. In the design phase of this project, posts had the ability to be 'starred' to promote the post to the top of the message board. We decided to hide this feature in order to prevent posts from enabling popularity contests among users. Instead, this star functionality will 'favorite' the post for the user only. The number of stars a post has received may also influence the ranking of posts on the back-end only. Currently, users are able to create posts, search for keywords within posts, and filter posts by clicking on tags.

###Community Technical Overview
The post is implemented using a Django ModelForm and may be found in ForumView called Thread. It may be beneficial to extend a Wagtail article for easier indexing, searching, and moderation by admins. Code is found in 'forum' folder. 

###Resources
(Resources overview here)

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

###Profile
* Need to implement

#Conclusion
We hope the site will provide Get Your Hair Wet the platform to empower girls worldwide. The site offers an abundance of resources to help the organization with its laudable mission. 
