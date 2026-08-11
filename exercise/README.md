<h1>
  <span class="headline">Mongoose Relationships Lab</span>
  <span class="subhead">Exercise</span>
</h1>

# Open House Lab – Mongoose Relationships

## Objective

In this lab, We will build a system for a client that wants an AirBnb type application called Open House. 

---

# Scenario

Your client wants you to build the foundation for an Airbnb-style application called **Open House**.

They have provided the following requirements.

## Models

### User

* `username`
* `password`

---

### Listing

* `streetAddress`
* `city`
* `price`
* `size`
* `owner`
* `category`

- The `owner` field should reference the **User** model.
- The `category` field should reference the **Category** model.

---

### Review

* `reviewTitle`
* `reviewBody`
* `creator`

- The `creator` field should reference the **User** model.

---

### Category

* `categoryName`

# Relationship Requirements

The client has specified the following relationships:

### User → Listing

* A **User** can own **many Listings**.
* A **Listing** can have **only one Owner**.


---

### User → Review

* A **User** can write **many Reviews**.
* A **Review** belongs to **only one User**.


---


### Listing → Category
* A **Listing** belongs to **Only one Category**

# Part 1 - Database Planning

Before writing any code, create an **Entity Relationship Diagram (ERD)** that represents the application's data.

For the specifications provided by the client please create an ERD that we can present to the client to make sure it is to their liking and so we can get started building the system

Remember:

> REMEMBER we should ALWAYS plan before starting to code and create ERDs

- Save the ERD onto your computer. Add it to this project so it gets pushed to github

---

# Part 2 - Create the Project

- Use our [Starter Document](https://docs.google.com/document/d/1Skjcc3gQG1lPhW5qCw8wfAzoI5W1oYvjGt4KqD_fUr4/edit?usp=sharing) to set up a new application so we can start creating the app for the client

---

# Part 3 - Create the Models

Create the following Mongoose models based on what the client asked for:

- User
- Listing
- Review

Make sure that:

- Each model contains the fields the client asked for.
- The relationships use the correct `ObjectId` references.
- The `ref` values match the appropriate model names.


---

## Bonus Challenge

The client only specified the fields.

Improve the schemas by adding validation where appropriate.

Consider using:

* `required`
* `unique`
* `minLength`
* `maxLength`
* `min`
* `max`
* `default`

Think carefully about which fields should use each constraint.

---

# Part 4 - Test the Relationships

Open your `server.js` file.

Import all three models.

Create an asynchronous function called:

```javascript
testRelationships()
```

Inside this function:

### Step 1

Create a new **User**.

---

### Step 2

Create a new **Listing**.

Assign the newly created user's `_id` to the Listing's `owner` field.

---

### Checkpoint

Open MongoDB Compass and verify that:

* The User document was created.
* The Listing document was created.
* The Listing's `owner` field contains the User's ObjectId.

---

### Step 3

Erase all the code in the `testRelationships()` function

Instead, retrieve all Listings using:

```javascript
Listing.find()
```

Print the results using:

```javascript
console.log()
```

Notice that the `owner` field only contains an ObjectId.

---

### Step 4

Update your query to use Mongoose's:

```javascript
.populate()
```

Populate the `owner` field so that the entire User document is returned instead of only the ObjectId.

Compare the output before and after using `.populate()`.



# Bonus Lab

1. Create a categories model with name: String
2. Create the following routes and pages
**Categories**

| **HTTP method** |    **route**    |       **view**      |
|:---------------:|:---------------:|:-------------------:|
|       GET       | /categories/new | create-category.ejs |
|       POST      | /categories     | None                |
|       GET       | /categories     | all-categories.ejs  |




**Listings**

| **HTTP method** |      **route**     |      **view**      |
|:---------------:|:------------------:|:------------------:|
|       GET       | /listings/new      | create-listing.ejs |
|       POST      | /listings          | None               |
|       GET       | /listings          | all-listings.ejs   |
|       GET       | /listings/:id/edit | edit-lising.ejs    |
|       PUT       | /listings/:id      | None               |
|      DELETE     | /listings/:id      | None               |



2. Remember to get all the categories in the `/listings/new` route and pass it to the ejs.
3. When the user picks a category it should show them the category but post the `ObjectId`.
4. Remember also in `/listings` to populate the category


## BONUS 2:
1. create controller files for both categories and listings
2. Import the router from express in both of them and export it:
    ```js
    const router = require('express').Router()


    module.exports = router
    ```
3. import in your `server.js` file the controller you just exported and mount it using `app.use()`
4. Take all the relevant routes and put them in the controller file


# BONUS 3:
1. In the views folder create a `categories` folder and a `listings` and put all the relevant files in there. Now in each route make sure to add `listing/` or `categories/` before the view in `res.render()`


# BONUS 4:
1. Put all your functionality for your routes that communicate with the database in a `try catch` block. For now just `console.log()` the error


# BONUS 5:
1. It is bad practice to save the req.body in the database. instead of calling `.create(req.body)`. create a new object and add to it the fields you need from the `req.body`.
2. Look up object destructuring or ask Omar about it. You can get the key-value pairs out of the `req.body` object by destrucuring like so:
    ```js
    const {streetAddress, city, address} = req.body
    ```

