Seasonings Team Group Project
===

# EzRecipe

## Table of Contents
1. [Overview](#Overview)
1. [Product Spec](#Product-Spec)
1. [Wireframes](#Wireframes)
2. [Schema](#Schema)

## Overview
### Description
Our app finds recipes that you can make using ingredients you already have, reducing waste.

### App Evaluation
- **Category:** Food & Drink
- **Mobile:** This app could be a website, but is better on mobile because the user will have a more seamless experience.
- **Story:** Many people hate throwing away food. And many people still do it. Why? Because they don't know what else to do with it. Our app solves this issue by giving them something to do with it.
- **Market:** It is a green app, because it reduces food waste. Also, it is great for home cooks or people looking to cook at home, especially in the pandemic.
- **Habit:** Using our app makes you feel good. You are helping the world and ejoying yourself while doing it.
- **Scope:** It is straight forward. We can apply many of the things we have done in previous labs and assignments such as TableView, using API, persistence, animations, etc.

## Product Spec

### 1. User Stories (Required and Optional)

**Required Must-have Stories**

* Something to enter your ingredients that you have
* API to get recipes online
* TableView showing the matching recipes

**Optional Nice-to-have Stories**

* Save recipes
* Grocery list
* Upload your own recipe
* Images
* Different filters

### 2. Screen Archetypes

* Loading Screen (for when its retrieving recipes)
* Launch Screen
* Screen that will show recipe matches
* Your pantry screen
* Grocery list & pantry if we make it to that

### 3. Navigation

**Tab Navigation** (Tab to Screen)

* Your Pantry
* Favorite Recipes

**Flow Navigation** (Screen to Screen)

* Recipe Matches

## Wireframes
## Schema 
### Models
#### Post

   | Property      | Type     | Description |
   | ------------- | -------- | ------------|
   | objectId      | String   | unique id for the user post (default field) |
   | author        | Pointer to User| image author |
   | image         | File     | image that user posts |
   | caption       | String   | image caption by author |
   | commentsCount | Number   | number of comments that has been posted to an image |
   | likesCount    | Number   | number of likes for the post |
   | createdAt     | DateTime | date when post is created (default field) |
   | updatedAt     | DateTime | date when post is last updated (default field) |
### Networking
#### List of network requests by screen
   - Home Feed Screen
      - (Read/GET) Query all posts where user is author
         ```swift
         let query = PFQuery(className:"Post")
         query.whereKey("author", equalTo: currentUser)
         query.order(byDescending: "createdAt")
         query.findObjectsInBackground { (posts: [PFObject]?, error: Error?) in
            if let error = error { 
               print(error.localizedDescription)
            } else if let posts = posts {
               print("Successfully retrieved \(posts.count) posts.")
           // TODO: Do something with posts...
            }
         }
         ```
      - (Create/POST) Create a new like on a post
      - (Delete) Delete existing like
      - (Create/POST) Create a new comment on a post
      - (Delete) Delete existing comment
   - Create Post Screen
      - (Create/POST) Create a new post object
   - Profile Screen
      - (Read/GET) Query logged in user object
      - (Update/PUT) Update user profile image
