## What Is The Hearth?
The Hearth is a blog website about the Blizzard video game Hearthstone. It features self-written articles about Hearthstone news, decks, and gameplay.

<img src="https://justin-diep.com/imgs/projects/the_hearth.png" height=350>
To access the website click the following link: https://the-hearth.herokuapp.com/

## How Does The Hearth Work?
The below sections describe how the different features of The Hearth work and are implemented.

### User Authentication
The Hearth uses user authentication to enable and disable certain features on the website depending on the user. This feature is implemented with the help of the flask_login library. 

Users who have no registered or are not logged in have the most restrictions placed on them. They are only able to view and read articles, as well as see comments but not post new ones. Users who are registered on the website and are logged are able to post unlimited comments on any of the articles they read.

Admin users, like regular users, are also able to comment on and read existing posts. However, they also have the additional ability to exclusively access certain protected routes that allow them to post new articles, update existing articles, and delete old articles.

Users register and log onto the website by providing a unique username along with a password. By default, newly registered users are not given admin permissions. When a user registers on The Hearth, the data about the user's account is then sent to a PostgreSQL database for storage and reference. In order to store users passwords in the database securely, passwords are encrypted by sending them through ten rounds of salting and hashing using a hash function provided by the werkzeug library.

### Post Management
CRUD operations for posts/articles are implemented using RESTful routing techniques. 

Creating new post is done by first sending a GET request to  the protected "/new-post" route. This retrieves a form page to create a new post. After filling out the details for a new post on the from, the form data is added to our PostgreSQL database using a POST request also a "/new-post".

Reading posts is done by sending a GET request to "/post/post-id" where "post-id" is replaced with the id of the post wanted. The data about the particular post is then retrieved from our database and displayed to the user as a webpage.
  
Updating posts is done by first sending a GET request to the protected "/edit-post/post-id" route where "post-id" is replaced with the id of the post to edit. Existing data about the post is then retrieved from the database and sent into a HTML form where users can now edit the post details. After editing, the edited post details are then posted to the database using a POST request.

Deleting posts id done by sending a GET request to the protected "/post/post-id" route where "post-id" is replaced with the id of the post to be deleted. If the post-id belongs to a post in the database, the post is removed from the database.

