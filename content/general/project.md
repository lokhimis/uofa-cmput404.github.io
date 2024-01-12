title: Project: Distributed Social Networking
date: 2024-01-06
tags: project, grading
authors: Hazel Victoria Campbell
status: published
summary: Distributed Social Networking (SocialDistribution)

----

# Description

The web is fundamentally interconnected and peer to peer. There's
no really great reason why we should all use facebook.com or
google+ or myspace or something like that. If these social networks
came up with an API you could probably link between them and use
the social network you wanted. Furthermore you might gain some
autonomy.

Thus in the spirit of diaspora https://diasporafoundation.org/ we
want to build something like diaspora but far far simpler.

This blogging/social network platform will allow the importing of
other sources of posts (github, twitter, etc.) as well allow the
distributing sharing of posts and content.

An author sitting on one server can aggregate the posts of their
friends on other servers.   

We are going to go with an inbox model where by you share posts to
your friends by sending them your posts. This is similar to
activity pub: https://www.w3.org/TR/activitypub/ Activity Pub is
great, but too complex for a class project.

We also won't be adding much in the way of encryption or security
to this platform. We're keeping it simple and restful.

Choose at least 3 other groups to work with

## Scenario 

I log into SocialDistribution. I see my stream which is filled with
posts that have arrived in my inbox. I browse them and I click like
on anything by friend Steph who is on another node.

When I click like, my node sends a like object to Steph's inbox
that references her post.

I then comment on Steph's post. This sends a comment object to
Steph's inbox that references her post.

Steph's node will process events at her inbox and record the
comments and likes appropriately.

Then I write a public post, a public service announcement (PSA)
about how public service announcements are pretentious performative
social media and you shouldn't make them. The irony is lost on me.
I make an unlisted image post that contains an image for the PSA
and reference it from my PSA post. Nonetheless my node records my
post and makes a URL for both posts and then proceeds to send my
public posts to the inboxes of everyone who follows me. My node
knows who follows me and thus can just send the public post to each
of those inboxes. Perhaps there will be a scaling problem in the
future.

Later I write a message to Steph, a post that is private to just her.
This post is sent to her inbox.

When Steph logs into her node she'll see her stream and my public
post will be on her stream. She should also see that I've liked and
commented her post.

## Scenario Summary

    All actions from authors are routed through the inbox of the
    receiving authors by the node itself.

    Nodes will store copies of posts because they receive them in the
    inbox.

    Likes, Comments, Public Posts, Friends Only posts, Private posts are
    all sent to the inbox of the author.

## Project Parts 

- Part 0 - sign up a repo
- Part 1 - 1/2 way implementation
- Part 2 - Connect with Groups
- Part 3 - Finish it off!

# Collaboration
   
- You may consult with others but the submission should be your
  own team's source code.
- You may work with 5 other students (groups of 5)
- Work will be submitted together
- Collaboration must be documented in the README.md file
- Any external source code must be referenced and documented in
  the README.md file
- You make collaborate/consult with other groups in order to get
  your webservices to integrate with each other

# User Stories
   
   - As an author, I want to make public posts.
   - As an author, I want to edit public posts.
   - As an author, posts I create can link to images.
   - As an author, posts I create can be images.
   - As a server admin, images can be hosted on my server.
   - As an author, posts I create can be private to another author
   - As an author, posts I create can be private to my friends
   - As an author, I can share other author's public posts
   - As an author, I can re-share other author's friend posts to my friends
   - As an author, posts I make can be in simple plain text
   - As an author, posts I make can be in CommonMark
   - As an author, I want a consistent identity per server
   - As a server admin, I want to host multiple authors on my server
   - As a server admin, I want to share public images with users
     on other servers.
   - As an author, I want to pull in my github activity to my "stream"
   - As an author, I want to post posts to my "stream"
   - As an author, I want to delete my own public posts.
   - As an author, I want to befriend local authors
   - As an author, I want to befriend remote authors
   - As an author, I want to feel safe about sharing images and posts
     with my friends -- images shared to friends should only be
     visible to friends. [public images are public]
   - As an author, when someone sends me a friends only-post I want to
     see the likes.
   - As an author, comments on friend posts are private only to me the
     original author.
   - As an author, I want un-befriend local and remote authors
   - As an author, I want to be able to use my web-browser to manage
     my profile
   - As an author, I want to be able to use my web-browser to manage/author
     my posts
   - As a server admin, I want to be able add, modify, and remove
     authors.
   - As a server admin, I want to OPTIONALLY be able allow users to sign up but
     require my OK to finally be on my server
   - As a server admin, I don't want to do heavy setup to get the
     posts of my author's friends.
   - As a server admin, I want a restful interface for most operations
   - As an author, other authors cannot modify my public post
   - As an author, other authors cannot modify my shared to friends post.
   - As an author, I want to comment on posts that I can access
   - As an author, I want to like posts that I can access
   - As an author, my server will know about my friends
   - As an author, When I befriend someone (they accept my friend request) I follow them, only when
     the other author befriends me do I count as a real friend -- a bi-directional follow is a true friend.
   - As an author, I want to know if I have friend requests.
   - As an author, I should be able to browse the public posts of everyone
   - As a server admin, I want to be able to add nodes to share with
   - As a server admin, I want to be able to remove nodes and stop
     sharing with them.
   - As a server admin, I can limit nodes connecting to me via
     authentication.
   - As a server admin, node to node connections can be authenticated
     with HTTP Basic Auth
   - As a server admin, I can disable the node to node interfaces for
     connections that are not authenticated!
   - As an author, I want to be able to make posts that are unlisted,
     that are publicly shareable by URI alone (or for embedding images)

# Main Concepts

   - Author
     - makes posts
     - makes friends
     - befriends other authors
     - likes posts
     - comments on posts
     - a generally nice person
   - Server Admin
     - manages a node
     - allows people to sign up
     - responsible for private data :(
   - Follow
     - Friend another author and they accept the friend request
     - They will send their posts to your inbox
   - Friend
     - Someone who follows you.
   - True Friend
     - Bidirectional friendship.
   - Real Friend
     - True friend
   - Server
     - a host that hosts authors and vouches for them
   - Restful service
     - The model of the service and its API
   - UI
     - The HTML/CSS/JS coated version user interface 
   - Public Post
     - this is a post that will show up publicly. 
     - it has a public URL
     - anyone can see it
     - Public posts can be liked
     - public posts can have comments from friends
   - Friend Post
     - this is a post that is shared to friends (followers)
     - since it is sent, it is a message and not changeable
     - Friend posts can be liked
     - Friend posts can have comments sent back to the author via the author's inbox
   - Inbox
     - This is what a READER or USER of the social network has. They make friends, and friends send objects to their inbox.
     - This forms the backbone of the timeline of the social media user.
     - This receives likes and comments.
   - Remote
     - A node to node connection. Requests from another node. HTTP Basic Auth authenticated.
   - Local
     - A local user accessing the REST API. Likely will use their cookie-auth, basic auth, or token auth. Local usually implies you check whether or not the user should have access. For instance local API access to the inbox should be limited to only that authenticated authors---don't snoop!

** Authentication
   - Remote node authentication is global between nodes. It requires an admin to allow node to node access.
   - Remote node authentication is done solely with HTTP basic auth
   - Local auth uses your frameworks local auth mechanisms (cookies, tokens, basic auth).   - Local refers to local access to the restful API. This is useful for frameworks like react, vue, or angular to get access to data, and enable a more client heavy UI.

** Pagination
   - If something is paginated it has query options:
     - page - how many pages of objects have been delivered
     - size - how big is a page
     - Page 4 of objects http://service/author/{author_id}/posts/{post_id}/comments?page=4
     - Page 4 of objects but 40 per page http://service/author/{author_id}/posts/{post_id}/comments?page=4&size=40
     - 1 based indexing. First page is 1.
** Objects
   - HTTP Methods not explicitly listed are not allowed methods
   - Most HTTP methods are local only, and provided for local node use.
*** Authors
    - URL: ://service/authors/
      - GET [local, remote]: retrieve all profiles on the server (paginated)
         - page: how many pages
         - size: how big is a page
    - Example query: GET ://service/authors?page=10&size=5 
      - Gets the 5 authors, authors 45 to 49.
    - Example: GET ://service/authors/
      #+BEGIN_SRC json
      {
          "type": "authors",      
          "items":[
              {
                  "type":"author",
                  "id":"http://127.0.0.1:5454/authors/1d698d25ff008f7538453c120f581471",
                  "url":"http://127.0.0.1:5454/authors/1d698d25ff008f7538453c120f581471",
                  "host":"http://127.0.0.1:5454/",
                  "displayName":"Greg Johnson",
                  "github": "http://github.com/gjohnson",
                  "profileImage": "https://i.imgur.com/k7XVwpB.jpeg"
              },
              {
                  "type":"author",
                  "id":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
                  "host":"http://127.0.0.1:5454/",
                  "displayName":"Lara Croft",
                  "url":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
                  "github": "http://github.com/laracroft",
                  "profileImage": "https://i.imgur.com/k7XVwpB.jpeg"
              }
          ]
      }
      #+END_SRC

*** Single Author
    - URL: ://service/authors/{AUTHOR_ID}/
      - GET [local, remote]: retrieve AUTHOR_ID's profile
      - POST [local]: update AUTHOR_ID's profile
    - Example Format:
      #+BEGIN_SRC json
      {
          "type":"author",
          # ID of the Author
          "id":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
          # the home host of the author
          "host":"http://127.0.0.1:5454/",
          # the display name of the author
          "displayName":"Lara Croft",
          # url to the authors profile
          "url":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
          # HATEOS url for Github API
          "github": "http://github.com/laracroft",
          # Image from a public domain
          "profileImage": "https://i.imgur.com/k7XVwpB.jpeg"
      }
      #+END_SRC
*** Followers
    - URL: ://service/authors/{AUTHOR_ID}/followers
      - GET [local, remote]: get a list of authors who are AUTHOR_ID's followers
    - URL: ://service/authors/{AUTHOR_ID}/followers/{FOREIGN_AUTHOR_ID}
      - DELETE [local]: remove FOREIGN_AUTHOR_ID as a follower of AUTHOR_ID
      - PUT [local]: Add FOREIGN_AUTHOR_ID as a follower of AUTHOR_ID (must be authenticated)
      - GET [local, remote] check if FOREIGN_AUTHOR_ID is a follower of AUTHOR_ID
    - Example: GET ://service/authors/{AUTHOR_ID}/followers
      #+BEGIN_SRC json
      {
          "type": "followers",      
          "items":[
              {
                  "type":"author",
                  "id":"http://127.0.0.1:5454/authors/1d698d25ff008f7538453c120f581471",
                  "url":"http://127.0.0.1:5454/authors/1d698d25ff008f7538453c120f581471",
                  "host":"http://127.0.0.1:5454/",
                  "displayName":"Greg Johnson",
                  "github": "http://github.com/gjohnson",
                  "profileImage": "https://i.imgur.com/k7XVwpB.jpeg"
              },
              {
                  "type":"author",
                  "id":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
                  "host":"http://127.0.0.1:5454/",
                  "displayName":"Lara Croft",
                  "url":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
                  "github": "http://github.com/laracroft",
                  "profileImage": "https://i.imgur.com/k7XVwpB.jpeg"
              }
          ]
      }
      #+END_SRC
   
*** Friend/Follow Request
    - This allows you to follow someone you, so they can send you their post.
    - If the recipient accepts the Friend Request then you are friends
    - If the recipient folows you, you are true friends
    - Sent to inbox of "object" 
    - Example format:
      #+BEGIN_SRC json
      {
          "type": "Follow",      
          "summary":"Greg wants to follow Lara",
          "actor":{
              "type":"author",
              "id":"http://127.0.0.1:5454/authors/1d698d25ff008f7538453c120f581471",
              "url":"http://127.0.0.1:5454/authors/1d698d25ff008f7538453c120f581471",
              "host":"http://127.0.0.1:5454/",
              "displayName":"Greg Johnson",
              "github": "http://github.com/gjohnson",
              "profileImage": "https://i.imgur.com/k7XVwpB.jpeg"
          },
          "object":{
              "type":"author",
              # ID of the Author
              "id":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
              # the home host of the author
              "host":"http://127.0.0.1:5454/",
              # the display name of the author
              "displayName":"Lara Croft",
              # url to the authors profile
              "url":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
              # HATEOS url for Github API
              "github": "http://github.com/laracroft",
              # Image from a public domain
              "profileImage": "https://i.imgur.com/k7XVwpB.jpeg"
          }
      }
      #+END_SRC

*** Post    
    - URL: ://service/authors/{AUTHOR_ID}/posts/{POST_ID}
      - GET [local, remote] get the public post whose id is POST_ID
      - POST [local] update the post whose id is POST_ID (must be authenticated)
      - DELETE [local] remove the post whose id is POST_ID
      - PUT [local] create a post where its id is POST_ID
    - Creation URL ://service/authors/{AUTHOR_ID}/posts/
      - GET [local, remote] get the recent posts from author AUTHOR_ID (paginated)
      - POST [local] create a new post but generate a new id
    - Be aware that Posts can be images that need base64 decoding.
      - posts can also hyperlink to images that are public
    - Example Format:
      #+BEGIN_SRC json
      {
          "type":"post",
          # title of a post
          "title":"A post title about a post about web dev",
          # id of the post
          "id":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e/posts/764efa883dda1e11db47671c4a3bbd9e"
          # where did you get this post from?
          "source":"http://lastplaceigotthisfrom.com/posts/yyyyy",
          # where is it actually from
          "origin":"http://whereitcamefrom.com/posts/zzzzz",
          # a brief description of the post
          "description":"This post discusses stuff -- brief",
          # The content type of the post
          # assume either
          # text/markdown -- common mark
          # text/plain -- UTF-8
          # application/base64
          # image/png;base64 # this is an embedded png -- images are POSTS. So you might have a user make 2 posts if a post includes an image!
          # image/jpeg;base64 # this is an embedded jpeg
          # for HTML you will want to strip tags before displaying
          "contentType":"text/plain",
          "content":"Þā wæs on burgum Bēowulf Scyldinga, lēof lēod-cyning, longe þrāge folcum gefrǣge (fæder ellor hwearf, aldor of earde), oð þæt him eft onwōc hēah Healfdene; hēold þenden lifde, gamol and gūð-rēow, glæde Scyldingas. Þǣm fēower bearn forð-gerīmed in worold wōcun, weoroda rǣswan, Heorogār and Hrōðgār and Hālga til; hȳrde ic, þat Elan cwēn Ongenþēowes wæs Heaðoscilfinges heals-gebedde. Þā wæs Hrōðgāre here-spēd gyfen, wīges weorð-mynd, þæt him his wine-māgas georne hȳrdon, oð þæt sēo geogoð gewēox, mago-driht micel. Him on mōd bearn, þæt heal-reced hātan wolde, medo-ærn micel men gewyrcean, þone yldo bearn ǣfre gefrūnon, and þǣr on innan eall gedǣlan geongum and ealdum, swylc him god sealde, būton folc-scare and feorum gumena. Þā ic wīde gefrægn weorc gebannan manigre mǣgðe geond þisne middan-geard, folc-stede frætwan. Him on fyrste gelomp ǣdre mid yldum, þæt hit wearð eal gearo, heal-ærna mǣst; scōp him Heort naman, sē þe his wordes geweald wīde hæfde. Hē bēot ne ālēh, bēagas dǣlde, sinc æt symle. Sele hlīfade hēah and horn-gēap: heaðo-wylma bād, lāðan līges; ne wæs hit lenge þā gēn þæt se ecg-hete āðum-swerian 85 æfter wæl-nīðe wæcnan scolde. Þā se ellen-gǣst earfoðlīce þrāge geþolode, sē þe in þȳstrum bād, þæt hē dōgora gehwām drēam gehȳrde hlūdne in healle; þǣr wæs hearpan swēg, swutol sang scopes. Sægde sē þe cūðe frum-sceaft fīra feorran reccan",
          # the author has an ID where by authors can be disambiguated
          "author":{
                "type":"author",
                # ID of the Author
                "id":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
                # the home host of the author
                "host":"http://127.0.0.1:5454/",
                # the display name of the author
                "displayName":"Lara Croft",
                # url to the authors profile
                "url":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
                # HATEOS url for Github API
                "github": "http://github.com/laracroft",
                # Image from a public domain (optional, can be missing)
                "profileImage": "https://i.imgur.com/k7XVwpB.jpeg"
          },
          # categories this post fits into (a list of strings
          "categories":["web","tutorial"],
          # comments about the post
          # return a maximum number of comments
          # total number of comments for this post
          "count": 1023,
          # the first page of comments
          "comments":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e/posts/de305d54-75b4-431b-adb2-eb6b9e546013/comments"
          # commentsSrc is OPTIONAL and can be missing
          # You should return ~ 5 comments per post.
          # should be sorted newest(first) to oldest(last)
          # this is to reduce API call counts
          "commentsSrc":{
              "type":"comments",
              "page":1,
              "size":5,
              "post":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e/posts/764efa883dda1e11db47671c4a3bbd9e"
              "id":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e/posts/de305d54-75b4-431b-adb2-eb6b9e546013/comments"
              "comments":[
                  {
                      "type":"comment",
                      "author":{
                          "type":"author",
                          # ID of the Author (UUID)
                          "id":"http://127.0.0.1:5454/authors/1d698d25ff008f7538453c120f581471",
                          # url to the authors information
                          "url":"http://127.0.0.1:5454/authors/1d698d25ff008f7538453c120f581471",
                          "host":"http://127.0.0.1:5454/",
                          "displayName":"Greg Johnson",
                          # HATEOS url for Github API
                          "github": "http://github.com/gjohnson",
                          # Image from a public domain
                          "profileImage": "https://i.imgur.com/k7XVwpB.jpeg"
                      },
                      "comment":"Sick Olde English",
                      "contentType":"text/markdown",
                      # ISO 8601 TIMESTAMP
                      "published":"2015-03-09T13:07:04+00:00",
                      # ID of the Comment (UUID)
                      "id":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e/posts/de305d54-75b4-431b-adb2-eb6b9e546013/comments/f6255bb01c648fe967714d52a89e8e9c",
                  }
              ]
          }
          # ISO 8601 TIMESTAMP
          "published":"2015-03-09T13:07:04+00:00",
          # visibility ["PUBLIC","FRIENDS"]
          "visibility":"PUBLIC",
          # for visibility PUBLIC means it is open to the wild web
          # FRIENDS means if we're direct friends I can see the post
          # FRIENDS should've already been sent the post so they don't need this
          "unlisted":false
          # unlisted means it is public if you know the post name -- use this for images, it's so images don't show up in timelines
      }
      #+END_SRC

*** Image Posts
    Image Posts are just posts that are images. But they are encoded as base64 data.
    You can inline an image post using a data url or you can use this 
    shortcut to get the image if authenticated to see it.
    - URL: ://service/authors/{AUTHOR_ID}/posts/{POST_ID}/image
      - GET [local, remote] get the public post converted to binary as an iamge
        - return 404 if not an image
    - This end point decodes image posts as images. This allows the use of
      image tags in markdown.
    - You can use this to proxy or cache images.

*** Comments
    - URL: ://service/authors/{AUTHOR_ID}/posts/{POST_ID}/comments
      - GET [local, remote] get the list of comments of the post whose id is POST_ID (paginated)
      - POST [local] if you post an object of "type":"comment", it will add your comment to the post whose id is POST_ID
    - example comment from ://service/authors/{AUTHOR_ID}/posts/{POST_ID}/comments
      #+BEGIN_SRC json
      {
          "type":"comment",
          "author":{
              "type":"author",
              # ID of the Author (UUID)
              "id":"http://127.0.0.1:5454/authors/1d698d25ff008f7538453c120f581471",
              # url to the authors information
              "url":"http://127.0.0.1:5454/authors/1d698d25ff008f7538453c120f581471",
              "host":"http://127.0.0.1:5454/",
              "displayName":"Greg Johnson",
              # HATEOS url for Github API
              "github": "http://github.com/gjohnson",
              # Image from a public domain
              "profileImage": "https://i.imgur.com/k7XVwpB.jpeg"
          }
          "comment":"Sick Olde English",
          "contentType":"text/markdown",
          # ISO 8601 TIMESTAMP
          "published":"2015-03-09T13:07:04+00:00",
          # ID of the Comment (UUID)
          "id":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e/posts/de305d54-75b4-431b-adb2-eb6b9e546013/comments/f6255bb01c648fe967714d52a89e8e9c",
      }
      #+END_SRC
    - example comments from a post
      #+BEGIN_SRC json
      {
          "type":"comments",
          "page":1,
          "size":5,
          "post":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e/posts/764efa883dda1e11db47671c4a3bbd9e"
          "id":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e/posts/de305d54-75b4-431b-adb2-eb6b9e546013/comments"
          "comments":[
              {
                  "type":"comment",
                  "author":{
                      "type":"author",
                      # ID of the Author (UUID)
                      "id":"http://127.0.0.1:5454/authors/1d698d25ff008f7538453c120f581471",
                      # url to the authors information
                      "url":"http://127.0.0.1:5454/authors/1d698d25ff008f7538453c120f581471",
                      "host":"http://127.0.0.1:5454/",
                      "displayName":"Greg Johnson",
                      # HATEOS url for Github API
                      "github": "http://github.com/gjohnson",
                      # Image from a public domain
                      "profileImage": "https://i.imgur.com/k7XVwpB.jpeg"
                  },
                  "comment":"Sick Olde English",
                  "contentType":"text/markdown",
                  # ISO 8601 TIMESTAMP
                  "published":"2015-03-09T13:07:04+00:00",
                  # ID of the Comment (UUID)
                  "id":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e/posts/de305d54-75b4-431b-adb2-eb6b9e546013/comments/f6255bb01c648fe967714d52a89e8e9c",
              }
          ]
      }
      #+END_SRC


*** Likes
    - You can like posts and comments
    - Send them to the inbox of the author of the post or comment
    - URL: ://service/authors/{AUTHOR_ID}/inbox/
      - POST [local, remote]: send a like object to AUTHOR_ID
    - URL: ://service/authors/{AUTHOR_ID}/posts/{POST_ID}/likes
      - GET [local, remote] a list of likes from other authors on AUTHOR_ID's post POST_ID
    - URL: ://service/authors/{AUTHOR_ID}/posts/{POST_ID}/comments/{COMMENT_ID}/likes
      - GET [local, remote] a list of likes from other authors on AUTHOR_ID's post POST_ID comment COMMENT_ID
    - Example like object:
      #+BEGIN_SRC json
      {
          "@context": "https://www.w3.org/ns/activitystreams",
          "summary": "Lara Croft Likes your post",         
          "type": "Like",
          "author":{
              "type":"author",
              "id":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
              "host":"http://127.0.0.1:5454/",
              "displayName":"Lara Croft",
              "url":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
              "github":"http://github.com/laracroft",
              "profileImage": "https://i.imgur.com/k7XVwpB.jpeg"
          },
          "object":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e/posts/764efa883dda1e11db47671c4a3bbd9e"
     }
     #+END_SRC
*** Liked
    - URL: ://service/authors/{AUTHOR_ID}/liked
      - GET [local, remote] list what public things AUTHOR_ID liked.
        - It's a list of of likes originating from this author
        - Note: be careful here private information could be disclosed.
    - Example liked object:
      #+BEGIN_SRC json
      {
          "type":"liked",
          "items":[
              {
                  "@context": "https://www.w3.org/ns/activitystreams",
                  "summary": "Lara Croft Likes your post",         
                  "type": "Like",
                  "author":{
                      "type":"author",
                      "id":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
                      "host":"http://127.0.0.1:5454/",
                      "displayName":"Lara Croft",
                      "url":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
                      "github":"http://github.com/laracroft",
                      "profileImage": "https://i.imgur.com/k7XVwpB.jpeg"
                  },
                  "object":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e/posts/764efa883dda1e11db47671c4a3bbd9e"
              }
          ]
      }
      #+END_SRC

*** Inbox
    - The inbox is all the new posts from who you follow
    - URL: ://service/authors/{AUTHOR_ID}/inbox
      - GET [local]: if authenticated get a list of posts sent to AUTHOR_ID (paginated)
      - POST [local, remote]: send a post to the author
        - if the type is "post" then add that post to AUTHOR_ID's inbox
        - if the type is "Follow" then add that follow is added to AUTHOR_ID's inbox to approve later
        - if the type is "Like" then add that like to AUTHOR_ID's inbox
        - if the type is "comment" then add that comment to AUTHOR_ID's inbox
      - DELETE [local]: clear the inbox
    - Example, retrieving an inbox
      #+BEGIN_SRC json
      {
          "type":"inbox",
          "author":"http://127.0.0.1:5454/authors/c1e3db8ccea4541a0f3d7e5c75feb3fb",
          "items":[
              {
                  "type":"post",
                  "title":"A Friendly post title about a post about web dev",
                  "id":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e/posts/764efa883dda1e11db47671c4a3bbd9e"
                  "source":"http://lastplaceigotthisfrom.com/authors/xxxxxx/posts/yyyyy",
                  "origin":"http://whereitcamefrom.com/authors/yyyyyy/posts/zzzzz",
                  "description":"This post discusses stuff -- brief",
                  "contentType":"text/plain",
                  "content":"Þā wæs on burgum Bēowulf Scyldinga, lēof lēod-cyning, longe þrāge folcum gefrǣge (fæder ellor hwearf, aldor of earde), oð þæt him eft onwōc hēah Healfdene; hēold þenden lifde, gamol and gūð-rēow, glæde Scyldingas. Þǣm fēower bearn forð-gerīmed in worold wōcun, weoroda rǣswan, Heorogār and Hrōðgār and Hālga til; hȳrde ic, þat Elan cwēn Ongenþēowes wæs Heaðoscilfinges heals-gebedde. Þā wæs Hrōðgāre here-spēd gyfen, wīges weorð-mynd, þæt him his wine-māgas georne hȳrdon, oð þæt sēo geogoð gewēox, mago-driht micel. Him on mōd bearn, þæt heal-reced hātan wolde, medo-ærn micel men gewyrcean, þone yldo bearn ǣfre gefrūnon, and þǣr on innan eall gedǣlan geongum and ealdum, swylc him god sealde, būton folc-scare and feorum gumena. Þā ic wīde gefrægn weorc gebannan manigre mǣgðe geond þisne middan-geard, folc-stede frætwan. Him on fyrste gelomp ǣdre mid yldum, þæt hit wearð eal gearo, heal-ærna mǣst; scōp him Heort naman, sē þe his wordes geweald wīde hæfde. Hē bēot ne ālēh, bēagas dǣlde, sinc æt symle. Sele hlīfade hēah and horn-gēap: heaðo-wylma bād, lāðan līges; ne wæs hit lenge þā gēn þæt se ecg-hete āðum-swerian 85 æfter wæl-nīðe wæcnan scolde. Þā se ellen-gǣst earfoðlīce þrāge geþolode, sē þe in þȳstrum bād, þæt hē dōgora gehwām drēam gehȳrde hlūdne in healle; þǣr wæs hearpan swēg, swutol sang scopes. Sægde sē þe cūðe frum-sceaft fīra feorran reccan",
                  "author":{
                        "type":"author",
                        "id":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
                        "host":"http://127.0.0.1:5454/",
                        "displayName":"Lara Croft",
                        "url":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
                        "github": "http://github.com/laracroft",
                        "profileImage": "https://i.imgur.com/k7XVwpB.jpeg"
                  },
                  "categories":["web","tutorial"],
                  "comments":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e/posts/de305d54-75b4-431b-adb2-eb6b9e546013/comments"
                  "published":"2015-03-09T13:07:04+00:00",
                  "visibility":"FRIENDS",
                  "unlisted":false
              },
              {
                  "type":"post",
                  "title":"DID YOU READ MY POST YET?",
                  "id":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e/posts/999999983dda1e11db47671c4a3bbd9e",
                  "source":"http://lastplaceigotthisfrom.com/authors/xxxxxx/posts/yyyyy",
                  "origin":"http://whereitcamefrom.com/authors/wwwwww/posts/zzzzz",
                  "description":"Whatever",
                  "contentType":"text/plain",
                  "content":"Are you even reading my posts Arjun?",
                  "author":{
                        "type":"author",
                        "id":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
                        "host":"http://127.0.0.1:5454/",
                        "displayName":"Lara Croft",
                        "url":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e",
                        "github": "http://github.com/laracroft",
                        "profileImage": "https://i.imgur.com/k7XVwpB.jpeg"
                  },
                  "categories":["web","tutorial"],
                  "comments":"http://127.0.0.1:5454/authors/9de17f29c12e8f97bcbbd34cc908f1baba40658e/posts/de305d54-75b4-431b-adb2-eb6b9e546013/comments"
                  "published":"2015-03-09T13:07:04+00:00",
                  "visibility":"FRIENDS",
                  "unlisted":false
              }
          ]
      }
      #+END_SRC


** Requirements

   - WARNING: Check this over again
   - [ ] Implement the webservice as described in the user stories
   - [ ] Provide a webservice interface that is restful
   - [ ] Provide a web UI interface that is usable
   - [ ] Prove your project by connecting with at least 1 clone of your project.
   - [ ] Prove your project by connecting with at least 2 other groups.
   - [ ] Prove your project by connecting with at least 3 other groups.
   - [ ] Make a video demo of your blog (desktop-recorder is ok) 
      - Your video may not be a part of your presentation.
   - [ ] Make a presentation about your blog 
   - [ ] Follow the guidelines in the project.org for URLs and services
   - [ ] Allow users to accept or reject friend requests
   - [ ] Images get the same protection that posts get as they are POSTS   

** Take-aways
   - [ ] 1 Working Website
   - [ ] 1 Github git repo
   - [ ] 1 Presentation
      - May not include the video
   - [ ] 1 OpenAPI (formally 'Swagger') specification for your API 
   - [ ] 1 Video
 
** Restrictions
   - [ ] Use Python 3.6+ (otherwise get approval)
   - [ ] Use Django or Flask (otherwise get approval)
   - [ ] Must run on one of the following:
     - [ ] provided VMs
     - [ ] Heroku
   - [ ] License your code properly (use an OSI approved license)
     - Put your name (or some representation of you like GeneralHuxFan768) on it!

** API Guidelines
   
   When building your API, try to adhere to these rules for easy compatibility with other groups:
   
   - REST API calls may be prefixed. ie. http://service_address/api/authors/{AUTHOR_ID}/posts/
   - Document your service address, port, hostname, prefix(if used), and the username/password for HTTP
    Basic Auth(if used) in your README so that HTTP clients can connect to your API.

** Submission Instructions
   - Fork my repository from github
      https://github.com/abramhindle/CMPUT404-project-socialdistribution
   - Share your repo in part 0
** Warning!!!!
   
   This spec is subject to change!

** Marking
*** Project Part 0
    - 1 mark
    - [ ] 4-5 CCIDs
    - [ ] 1 Github repo with a README and LICENSE
*** Project Part 1
    - 7 Marks
    - Total Project
      - Excellent 7: Excellent effort. Relatively consistent. At least ½
        of the project implemented. Clean code. 1/2 includes both UI and webservice.
      - Good 6: Good quality. Some inconsistency. About ½ of
        the project implemented
      - Satisfactory 5: Codebase in places. Passes some tests. Some
        parts run
      - Unsatisfactory 3: Effort exists, it's missing lots of components but something is there.
      - Failure 0: Missing. No attempted. Not complete enough to evaluate.
    - Code Base 
      - Excellent : Excellent effort. Relatively consistent. At least ½
        of the project implemented. Clean code
      - Good : Good quality. Some inconsistency. About ½ of
        the project implemented
      - Satisfactory : Codebase in places. Passes some tests. Some
        parts run
      - Unsatisfactory : Does not meet Satisfactory level
    - Test Cases 
      - Excellent: System is well tested
      - Good: System has some blind spots for testing
      - Satisfactory: Effort was placed on testing but it is inconsistent.
      - Unsatisfactory: test cases are inappropriate but exist.
      - Failure: Missing test cases
    - UI 2
      - Excellent: UI Exists and is coherent. Shows evidence of
        planning.
      - Good: UI Exists. Some issues
      - Satisfactory: UI Exists, it's not good. It has issues.
      - Unsatisfactory: A UI was attempted, a UI exists.
      - Failure: No UI, or what was attempted is not substantial.
    - Tool Use
      - Excellent: Use of at least Git is Evidence and Obvious
      - Good: Frequent but inconsistent use of Git, etc.
      - Satisfactory: Uses Git, etc.
      - Unsatisfactory: Limited of tool use
      - Failure: Used filesharing and email attachments instead of git
    - TA Demo
      - Excellent: Coherent demo, shows off features. Limited snags.
      - Good: Coherent demo, shows off features. Some snags.
      - Satisfactory: Lots of snags. Can demo it.
      - Unsatifactory: Unfinished, hard to demo.
      - Failure: no demo or unable to demo.
    - Web Service API & Documentation
      - Excellent: Documented, adheres to requirements to augments
        them with compatibility. Open API specification exists, has clear descriptions,
        and has example requests and responses from your API. 
      - Good: Documented, exists, tries to adhere to requirements. Open API specification exists,
        and has some descriptions and a few example requests and responses.
      - Satisfactory: Some of the webservice exists. Open API specification exists, but no descriptions
        or example requests and responses.
      - Unsatisfactory: Well you tried right? Open API specification does not exist.
      - Failure: Ok you didn't try. 
    - Design
      - Excellent: Adheres to standards, well designed
      - Good: Adheres to standards somewhat, some awkward parts
      - Satisfactory: Some good parts, some nasty parts
      - Unsatisfactory: Little effort went into documenting and
        designing the project
      - Failure: failure to learn from the class and apply concepts even remedially
*** Project Part 2: The web service 
    - 5 Marks
    - Total Project
      - Excellent 5: Excellent effort. Coordinates and connects fine with 2 or more groups.
      - Good 4: Some issues, not quite excellent but definitely fixable and functional with 1 or more groups
      - Satisfactory 3: There are issues, it does run, it does coordinate with 1 or more groups.
      - Unsatisfactory 2: Well you tried, but it's hardly working.
      - Failure 0: Missing. No attempted. Not complete enough to evaluate.
    - Web Service API & Documentation
      - Excellent: Documented, adheres to requirements to augments
        them with compatibility.  Open API specification exists, has clear descriptions,
        and has example requests and responses from your API. 
      - Good: Documented, exists, tries to adhere to requirements.  Open API specification exists,
        and has some descriptions and a few example requests and responses.
      - Satisfactory: Some of the webservice exists. Open API specification exists, but no descriptions
        or example requests and responses.
      - Unsatisfactory: Webservice exists, barely. Open API specification does not exist.
      - Failure: it is not usable.
    - Web Service Coordination
      - Excellent: Web service coordinates with 2+ other group
        projects successfully. Most interoperation requirements met.
      - Good: Web service coordinates with 1+ other group
        projects successfully. Most interoperation requirements met.
        Some snags.
      - Satisfactory: The basics of coordination are covered.
        Probably many snags.
      - Unsatisfactory 0: Coordination barely works.
      - Failure: failure to coordinate
    - Design 
      - Excellent: Adheres to standards, well designed
      - Good: Adheres to standards somewhat, some awkward parts
      - Satisfactory: Some good parts, some nasty parts
      - Unsatisfactory: Little effort went into documenting and
        designing the project
      - Failure: failure to apply what was learned in class        
*** Project Part 3
    - 20 Marks
    - Total Project
      - Excellent 20: Excellent effort. Coordinates and connects fine. Good demo. Clear application of what was learned in class. 3 or more groups connected. Posts with embedded images are visible. Image posts are visible.
      - Good 17: Some issues, not quite excellent but definitely operational and functional. 2 or more groups connected. Posts with embedded images are visible. Image posts are visible.
      - Satisfactory 14: There are issues, it does run, it does coordinate. Meets satisfactory aspects of rubric. 2 or more group connected. Image posts are visible.
      - Unsatisfactory 10: Well you tried, but it's hardly working. Meets unsatisfactory aspects of rubric. 1 or more group connected.
      - Failure 0: Missing. No attempted. Not complete enough to evaluate. Often hits failure aspects of rubric.
    - Note: these are ordered by importance, but you need to meet all these parts and we care about the final quality.
    - Code Base
      - Excellent: Excellent effort. Relatively consistent. At least 90%
        of requirements implemented. Clean code
      - Good: Good quality. Some inconsistency. About 90% of
        requirements implemented.
      - Satisfactory: Codebase in places. Passes some tests. Some
        parts run
      - Unsatisfactory: Does not meet Satisfactory level
    - UI 3
      - Excellent: UI Exists and works well. Shows evidence of
        planning. Looks great.
      - Good: UI Exists.  Looks good
      - Satisfactory: UI exists. Looks poor.
      - Unsatisfactory: UI exists. Doesn't work well. Worse than poor.
      - Failure: Missing or unusable.
    - Web Service Coordination
      - Excellent: Web service coordinates with 2+ other group
        projects successfully. Most interoperation requirements met.
      - Good: Web service coordinates with 2+ other group
        projects successfully. Most interoperation requirements met.
        Some snags.
      - Satisfactory: The basics of coordination are covered.
        Probably many snags.
      - Unsatisfactory: Coordination doesn't work or barely works.
    - Web Service API & Documentation
      - Excellent: Documented, adheres to requirements to augments
        them with compatibility.  Open API specification exists, has clear descriptions,
        and has example requests and responses from your API. 
      - Good: Documented, exists, tries to adhere to requirements.  Open API specification exists,
        and has some descriptions and a few example requests and responses.
      - Satisfactory: Some of the webservice exists. Open API specification exists,
        and has a few example requests and responses.
      - Unsatisfactory: Effort taken but incomplete. Open API specification exists, but no descriptions
        or example requests and responses.
      - Failure: API or Documentation Missing. Open API specification does not exist.
    - Test Cases
      - Excellent: System is well tested
      - Good: System has some tests
      - Unsatisfactory: test cases are inappropriate
      - Failure: Missing test cases
    - Tool Use
      - Excellent: Use of at least Git is Evidence and Obvious
      - Good: Frequent but inconsistent use of Git, etc.
      - Satisfactory: Infrequent use of Git, etc.
      - Unsatisfactory: Limited tool use
      - Failure: lack of tool use
    - Design
      - Excellent: Adheres to standards, well designed
      - Good: Adheres to standards somewhat, some awkward parts
      - Satisfactory: Some good parts, some nasty parts
      - Unsatisfactory: Little effort went into documenting and
        designing the project
      - Failure: clear lack of design
    - Adhering to Standards
      - Excellent: Excellent attempt at making a standards
        compliant website. Most things are compliant.
      - Good: An attempt at making a standards
        compliant website. Some not compliant.
      - Satisfactory: Inconsistent.
      - Unsatisfactory: poor attempt to meet standards.
      - Failure: failed to apply what was learned in class
    - Addressing Feedback:
      - Excellent: TAs suggestions were implemented, TA approves of
        implementation set.
      - Good: The good TA suggestions were implemented ;)
      - Satisfactory: Feedback ignored mostly, but some followed.
      - Unsatisfactory: Majority of Feedback ignored.
      - Failure: Feedback ignored.
    - Presentation:
      - Excellent: Presentation within time, shows teamwork,
        promotes the application, uses the live application to show functionality.
      - Good: Presentation nearly within time, some team works,
        reasonable presentation.
      - Satisfactory: Presentation exists but has problems.
      - Unsatisfactory: Missing or terrible presentation (lack of
        practice, lack of preparation, irrelevant) OR presentation includes video.
      - Failure: no presentation
    - Video Demo:
      - Excellent: Video is well presented and not boring, less
        than 2 minutes.
      - Good: Video presents the functionality and is less than 2
        minutes.
      - Satisfactory: Video is longer than 2 minutes, or doesn't
        accurately present the project.
      - Unsatisfactory: A video exists and it is a demo.
      - Failure: lack of video, failure to make a video.
    - AJAX
      - Excellent: Uses AJAX appropriately and well (documented)
      - Good: Uses some AJAX (documented)
      - Satisfactory: AJAX not really used
      - Unsatisfactory: An attempt was made.
      - Failure: No AJAX

** License

   - Parts of this document are derived from the W3C Documentation for Activity Pub
   - Copyright © 2018 W3C® (MIT, ERCIM, Keio, Beihang). W3C liability, trademark and permissive document license rules apply. 
   - https://www.w3.org/Consortium/Legal/2015/copyright-software-and-document
     #+BEGIN_SRC plain
     License
     
     By obtaining and/or copying this work, you (the licensee) agree that you have read, understood, and will comply with the following terms and conditions.
     
     Permission to copy, modify, and distribute this work, with or without modification, for any purpose and without fee or royalty is hereby granted, provided that you include the following on ALL copies of the work or portions thereof, including modifications:
     
         The full text of this NOTICE in a location viewable to users of the redistributed or derivative work.
         Any pre-existing intellectual property disclaimers, notices, or terms and conditions. If none exist, the W3C Software and Document Short Notice should be included.
         Notice of any changes or modifications, through a copyright statement on the new code or document such as "This software or document includes material copied from or derived from [title and URI of the W3C document]. Copyright © [YEAR] W3C® (MIT, ERCIM, Keio, Beihang)." 
     
     Disclaimers
     
     THIS WORK IS PROVIDED "AS IS," AND COPYRIGHT HOLDERS MAKE NO REPRESENTATIONS OR WARRANTIES, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO, WARRANTIES OF MERCHANTABILITY OR FITNESS FOR ANY PARTICULAR PURPOSE OR THAT THE USE OF THE SOFTWARE OR DOCUMENT WILL NOT INFRINGE ANY THIRD PARTY PATENTS, COPYRIGHTS, TRADEMARKS OR OTHER RIGHTS.
     
     COPYRIGHT HOLDERS WILL NOT BE LIABLE FOR ANY DIRECT, INDIRECT, SPECIAL OR CONSEQUENTIAL DAMAGES ARISING OUT OF ANY USE OF THE SOFTWARE OR DOCUMENT.
     
     The name and trademarks of copyright holders may NOT be used in advertising or publicity pertaining to the work without specific, written prior permission. Title to copyright in this work will at all times remain with copyright holders.
     #+END_SRC