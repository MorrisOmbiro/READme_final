# Not Reddit

 - - - # Plan A

## Group Members
> Morris Ombiro   
> Hassan Ali  
> Webster Wing  

## Live Application link 
> ##### [Heroku Link](https://not-reddit-4131.herokuapp.com/)    
https://not-reddit-4131.herokuapp.com/    
## Github Repo. Link 
> https://github.umn.edu/ombir002/final_project_4131
## List of Technologies/API's used
> miniature.IO (main API used) - to convert links into thumbnails  
> Bootstrap - Twitter feel   
> Python/Flask - Handling controller, views, forms, database access       
>HTML/CSS - General UI   
>Javascript - Event handling on upvote/downvote   
>SQLAlchemy - Database management  
> FLask Login plugin - Handle user session  
> Bcrypt - password protection hashing algorithm  
> WTforms - Generate forms  

## Detailed Description of the project 
   The idea of our web application was to create a remake of Reddit. To be specific, we are creating a remake of the old reddit. There are some ommissions (from original old reddit) such as specifying subreddits, or being able to rank posts by any other means other than the date posted. We also allow users to be able to register and login to their profile accounts. In the view, we allow users to be able to post links to items that they choose to share with all other users (images, website links). We also allow the users to communicate through comments on a specific post. The logged in users are able to see who is commenting and what time a comment was sent on a post. The users are also able to go to each other's profile to see the posts that user has made. They may also be able to upvote/downvote the post from the other user's profile, through the main feed, or through the comment section view. All of the above actions only apply if the user is logged in. Notice that if the user is not logged in, they are able to see the posts from all the users, but they are not allowed to comment, upvote/downvote or view another user's profile.

   Because old reddit used thumbnails to display their content rather than displaying full on images, we used a thumbnailer api (miniature.io) to transform all our links into thumbnails. The user may then either click on the thumbnail or the title (required when user is posting) to go to the link. In the comment section we opted to choose a list based comment section compared to a chained based comment section to reduce database complexity (as reddit does it).  
  
   Reddit is a database based application, therefore most of the controls happen around our sqlalchemy database. We are be able to manage and load the comments, posts, number of upvotes, and users all from the database. The python, javascript, html and css only act as a skin around our application. The main profile page is also displays the total number of upvotes a user has.

##### Application Layout/How to use the application
   There are four views (main feed, comment section, post section, profile section). The first view
when you land on our website, is a view of the current posts from all the users; main feed. At this view, you have options to register with our website or login if you've already registered. Once registered, you are redirected to the login page where you can use the same registration credentials to login. Once logged in (redirected to main feed again), you have the options to either logout, post an item or view your profile all on the top navbar. We have examples of posts and user profiles already to act as an example of our app's potential.

## List of controllers and their short description (<50words for each controller)
> /login
```sh
Redirects user to the login view. It accounts for GET and POST requests. 
It validates user using wtfforms and checks password-username validity.
The password is also hashed for further security, it renders template with a form
argument passed to login.html. Uses login_user to start user session. 
```
> /logout
```sh
Redirects user to the logout view. It accounts for GET and POST requests.
It validates that the user was first logged in before using logout_user
to end their session. If successful, redirects to main page with the user logged 
out. 
```
> /register
```sh
Redirects user to the register view. The user can then create a new username
with matching password and confirm-password fields. Verified using wtfforms.
Also accounts for GET and POST requests. Sends new user to SQLalchemy database.
Checks database for username re-use and rejects it too. Redirects to url_for('login').
```
> /comments/<int:post_id>
```sh
This directs the logged in user to the comment section of a specific post targeted by
a post_id number. Joins User, Comment and Post tables for ease of access. It accounts for 
GET and POST requests. Sends comments attached to user to the comments database. Redirects
to itself. 
```
> /post
```sh
Redirects the logged in user to the post view. Accounts for GET and POST requests. 
Checks for validity of the post by verifying the url and checking that the title was 
provided too, it redirects to comments.html with an attached post_id. If validation fails 
it renders back to post.html. 
```
> /profile/<int:user_id>
```sh
Redirects to profile based on user_id. Accounts for GET and POST requests. Sends info from
posts and users tables to be accessed in profile view. renders profile.html. 
```
## List of views and their short description (<50 words for each view)
> main.html
```sh
This is the first page that the user sees when they get to the website. 
It contains redirections to signup or login if user is not logged in, 
then logout, post and user profile links once user is logged in. The page 
consists of all posts from all users. 
```
> post.html
```sh
This is the page where the user can go (only if logged in) to post content.
The content is posted with a url and a title (both required) as part of the 
form. 
```
> comments.html 
```sh
This is the view where the user who is logged in may be able to leave a comment
on a post. The view also contains comments left by other users. It also shows 
a thumbnail and a title of the post on top. 
```
> profile.html 
```sh
This is the view that shows the user profile page. The view contains the user name,
how many upvotes they have contributed and a list of the posts they have submitted. 
```
## Views for user management (not counted)
>login.html
```sh
Just a very simple wtfform to manage user login
```
>signup.html
```sh
Also a very simple wtfform to manage user registration to the database 
```
## List of tables, their structure and short description 
> Comments 
```sh
Database table that holds
id:  Unique ID for comments relation
message: Message the comment has
user_id: Foreign key to the User ID of the user who commented
post_id: Foreign key to the Post ID of the post it is referring to
date_posted: date the comment was posted 
```
> Users
```sh
Database table that holds
id:  Unique ID for users relation
username: Username of the user
image_file: Profile image of the user
password: Password of the user
posts: Posts this user has posted
comments: Comments this user has commented 
```
> Posts 
```sh
Database table that holds
id: Unique ID for post relation
title: Title of the post
date_posted: Time post was posted
content: Body of the post
user_id: Foreign key to user who posted the post
comments: comments associated with the post
```
> Votes
```sh
Database table that holds
user_id: Foreign key to User ID who upvoted on post
post_id: Foreign key to Post ID that the upvote is associated with
like: An enum of whether it is an upvote or downvote
```
## References/Resources
> Bootdey.com - for some bootstrap templates  
> O'REILLY Flask Web Development by Miguel Grinberg  
> Bootstrap glyphicon components for arrow icons 
