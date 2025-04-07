# Assignment Three
## Purpose
The purpose of this assignment is to get comfortable working with a NoSQL database (MongoDB). 

For this assignment you will create a Users collection to store users for your signup and signin methods.  You will pass Username, Name and Password as part of signup.  To get a token you will call SingIn with username and password only.  The token should include the Name and UserName (not password)

You will also create Movies collection to store information about movies.  All endpoints will be protected with the JWT token received by a signin call. 

## Requirements
Create a collection in MongoDB to hold information about movies
- Each entry should contain the following
    - title (string, required, index)
    - releaseDate
    - genre (Action, Adventure, Comedy, Drama, Fantasy, Horror, Mystery, Thriller, Western, Science Fiction)
    - Array of three actors that were in the film
        - actorName
        - characterName
    - The movie collection should have at least five movies
- Create a NodeJS Web API to interact with your database
    - Follow best practices (e.g. /movies collection)
    - Your API should support all CRUD operations (through HTTP POST, PUT, DELETE, GET)
    - Ensure incoming entities contain the necessary information.  For example if the movie does not contain actors, the entity should not be created and an error should be returned 
- All endpoints should be protected with a JWT token (implement signup, and signin)
    - For this assignment you must implement a User database in Mongo
        - name
        - username 
        - password (should be hashed)
    - If username exists the endpoint should return an error that the user already exists
    - JWT secret needs to be stored in an environment variable
- Update the Pre-React CSC3916_REACT placeholder project to support /signup and /signin methods.  The React Single Page App should use your Assignment 3 API to support those two operations.

## Submissions
- All source code should be stored on github (remember .gitignore for node_modules)
- API needs to be deployed to heroku or render
- React Website that allows user to signup and singin (we did this in class)
- PostMan test collection that 
    - Signs Up a user (create a random user name and random password in your pre-test)
    - SignIn a User – parse token and store in postman environment variable
    - A separate call for each endpoint (save a movie, update a movie, delete a movie and get a movie)
    - Test error conditions (user already exists)
        - SignUp (user already exist)
        - Save Movie (missing information like actors (must be at least three), title, year or Genre)

- Create a readme.md at the root of your github repository with the embedded (markdown) to your test collection
    - Within the collection click the (…), share collection -> Embed
    - Static Button
    - Click update link
    - Include your environment settings
    - Copy to clipboard 
- Submit the Url to canvas with the REPO CSC_3916
- Note: All tests should be testing against your Heroku or Render endpoint

| Route | GET | POST | PUT | DELETE |
| --- | --- | --- | --- | --- |
| movies | Return all movies| save a single movie | FAIL | FAIL |
| movies/:movieparameter | Return a specific movie based on the :movieparameter | FAIL | Update the specific movie based on the :movieparameter in your case it's the title | Delete the specific movie based on the :movieparamters your case it's the title |*

* If Query String (Later Homework) reviews=true aggregate in reviews |

## Rubic
- -5 for missing REACT site (-2 if you are not able to signup or signin on the react site) that is all we implemented
- -1 for MovieSchema missing any of the attributes (array of actors, genre, year released or title)
- -2 for missing routes for /movies (POST/PUT/DELETE/GET)
- -1 for missing authentication on routes
- -2 for not deployed on Heroku/Render
- -1 missing Test error conditions
- -1 missing PostMan tests (signup, signin, separate call for each route)

## Resources
- https://www.mongodb.com/cloud/atlas
- Create a Free Subscription *Amazon
- https://render.com/docs/deploy-create-react-app **important: Environment Variable for https://github.com/AliceNN-ucdenver/CSC3916_REACT env.REACT_APP_API_URL, this weekend I will look at changes (I believe only 1 change in the actions)

## Setup Instructions

### Prerequisites
- Node.js and npm installed
- MongoDB Atlas account (or local MongoDB instance)

### Installation
1. Clone the repository
2. Install dependencies:
   ```
   npm install
   ```
3. Create a `.env` file in the root directory with the following variables:
   ```
   DB=mongodb+srv://<username>:<password>@<cluster>.mongodb.net/<dbname>
   SECRET_KEY=your_secret_key_for_jwt
   ```
   Replace the MongoDB connection string with your own and set a secure secret key.

4. Seed the database with sample movies:
   ```
   node seed.js
   ```
5. Start the server:
   ```
   node server.js
   ```

### API Endpoints

#### Authentication
- `POST /signup` - Register a new user
  - Required fields: `name`, `username`, `password`
- `POST /signin` - Login and get JWT token
  - Required fields: `username`, `password`

#### Movies
All movie endpoints require authentication with JWT token in the Authorization header.

- `GET /movies` - Get all movies
- `POST /movies` - Create a new movie
  - Required fields: `title`, `releaseDate`, `genre`, `actors` (array with at least one actor)
- `GET /movies/:id` - Get a specific movie by ID
- `PUT /movies/:id` - Update a specific movie
  - Required fields: same as POST
- `DELETE /movies/:id` - Delete a specific movie

### Example Requests

#### Signup
```
POST /signup
{
  "name": "John Doe",
  "username": "john123",
  "password": "password123"
}
```

#### Signin
```
POST /signin
{
  "username": "john123",
  "password": "password123"
}
```

#### Create Movie
```
POST /movies
{
  "title": "Example Movie",
  "releaseDate": 2023,
  "genre": "Action",
  "actors": [
    {
      "actorName": "Actor 1",
      "characterName": "Character 1"
    },
    {
      "actorName": "Actor 2",
      "characterName": "Character 2"
    }
  ]
}
```
[<img src="https://run.pstmn.io/button.svg" alt="Run In Postman" style="width: 128px; height: 32px;">](https://app.getpostman.com/run-collection/41738630-1c376a35-0e56-449a-b066-5c9c7f4c98b8?action=collection%2Ffork&source=rip_markdown&collection-url=entityId%3D41738630-1c376a35-0e56-449a-b066-5c9c7f4c98b8%26entityType%3Dcollection%26workspaceId%3D77c36a26-bf1f-4213-a6de-4ea208f5bdf5#?env%5BThongDang-HW3%5D=W3sia2V5IjoiYmFzZV91cmwiLCJ2YWx1ZSI6Imh0dHBzOi8vY3NjaTM5MTYtdGhvbmdkYW5nLWh3My5vbnJlbmRlci5jb20iLCJlbmFibGVkIjp0cnVlLCJzZXNzaW9uVmFsdWUiOiJodHRwczovL2NzY2kzOTE2LXRob25nZGFuZy1odzMub25yZW5kZXIuY29tIiwiY29tcGxldGVTZXNzaW9uVmFsdWUiOiJodHRwczovL2NzY2kzOTE2LXRob25nZGFuZy1odzMub25yZW5kZXIuY29tIiwic2Vzc2lvbkluZGV4IjowfSx7ImtleSI6ImF1dGhfdG9rZW4iLCJ2YWx1ZSI6IiIsImVuYWJsZWQiOnRydWUsInNlc3Npb25WYWx1ZSI6IkpXVC4uLiIsImNvbXBsZXRlU2Vzc2lvblZhbHVlIjoiSldUIGV5SmhiR2NpT2lKSVV6STFOaUlzSW5SNWNDSTZJa3BYVkNKOS5leUpwWkNJNklqWTNaak14WW1JNE1EUTFPREpoTjJGak56TTRZekl6WWlJc0luVnpaWEp1WVcxbElqb2lkWE5sY2pFM05ETTVPRFUxT1RJM016bEFaWGhoYlhCc1pTNWpiMjBpTENKcFlYUWlPakUzTkRNNU9EVTFPVFVzSW1WNGNDSTZNVGMwTXprNE9URTVOWDAuczNHSmpvdlBfZjk3UWc1NnhVVzNiTlRVaG9uLVJQN29HQU1teTBlOGJUOCIsInNlc3Npb25JbmRleCI6MX0seyJrZXkiOiJ0ZXN0X3VzZXJuYW1lIiwidmFsdWUiOiIiLCJlbmFibGVkIjp0cnVlLCJzZXNzaW9uVmFsdWUiOiJ1c2VyMTc0Mzk4NTU5MjczOUBleGFtcGxlLmNvbSIsImNvbXBsZXRlU2Vzc2lvblZhbHVlIjoidXNlcjE3NDM5ODU1OTI3MzlAZXhhbXBsZS5jb20iLCJzZXNzaW9uSW5kZXgiOjJ9LHsia2V5IjoidGVzdF9wYXNzd29yZCIsInZhbHVlIjoiIiwiZW5hYmxlZCI6dHJ1ZSwic2Vzc2lvblZhbHVlIjoicGFzc3dvcmQxNzQzOTg1NTkyNzM5IiwiY29tcGxldGVTZXNzaW9uVmFsdWUiOiJwYXNzd29yZDE3NDM5ODU1OTI3MzkiLCJzZXNzaW9uSW5kZXgiOjN9LHsia2V5IjoidGVzdF9uYW1lIiwidmFsdWUiOiIiLCJlbmFibGVkIjp0cnVlLCJzZXNzaW9uVmFsdWUiOiJVc2VyIDE3NDM5ODU1OTI3MzkiLCJjb21wbGV0ZVNlc3Npb25WYWx1ZSI6IlVzZXIgMTc0Mzk4NTU5MjczOSIsInNlc3Npb25JbmRleCI6NH0seyJrZXkiOiJtb3ZpZV9pZCIsInZhbHVlIjoiIiwiZW5hYmxlZCI6dHJ1ZSwic2Vzc2lvblZhbHVlIjoiNjdmMzFiYmYwNDU4MmE3YWM3MzhjMjQxIiwiY29tcGxldGVTZXNzaW9uVmFsdWUiOiI2N2YzMWJiZjA0NTgyYTdhYzczOGMyNDEiLCJzZXNzaW9uSW5kZXgiOjV9XQ==)

React app deployment: https://csc3916-react19-sxrl.onrender.com

Github React link: https://github.com/ThongDang251999/CSC3916_REACT19.git
