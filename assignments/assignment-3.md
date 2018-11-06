# IEMS5780 / IERG4080 Assignment 3

## Movie Recommender System

* **Deadline**: 30th November, 2018 (Friday)
* **Total Marks**: 100

## Objectives

* To get familiar with building HTTP applications
* To get familiar with creating a Flask application in Python
* To get familiar with different basic concepts in recommender systems

## Tasks

In this assignment, you will build a movie recommender system using some memory-based recommendation algorithms. The system should be deployed as a Telegram bot and a Web application server.

Your recommender system should at least consists of two parts:
1. A python script `bot.py` that continues to receive user messages from Telegram. When a message from a user is received, it sends request(s) to the recommendation server, and formats a response to be sent back to the user via Telegram.
2. A python script `app.py` that implements an HTTP server using Flask. It should provide different routes to accept requests to different functions (see more details below).

The system should provide the following functions:
1. Accepts a new user identified by the `chat_id`
2. Returns a movie that has not yet been rated by a user so that the user can provide his/her rating on the movie
3. If enough ratings have been collected from a user, use the **user-based collaborative filtering** algorithm to generate recommended movies to the user

<center>
    <img src="assignment-3-system.png" width="90%"/>
</center>

More details about how the system should be implemented are described below.

### Dataset

We will use a dataset commonly used in recommender systems research, the MovieLens 100K movie ratings dataset created by GroupLens at the University of Minnesota. Check the Website [https://grouplens.org/datasets/movielens/](https://grouplens.org/datasets/movielens/), and read the section "recommended for education and development". We will use the **small** dataset with 100,000 ratings.

The dataset consists of 100,000 ratings on different movies by the users of the MovieLens recommender system:
- 100,000 ratings (1-5) from 600 users on 9,000 movies
- Each user has at least 20 movies
- Data about the movies and the users

You can read the README file here: [http://files.grouplens.org/datasets/movielens/ml-latest-small-README.html](http://files.grouplens.org/datasets/movielens/ml-latest-small-README.html)

### The Telegram Bot Script

The Telegram bot script `bot.py` is used to rely user input to the server, and the server's output back to the user. In this assignment, you do NOT have to use a separate thread to communicate with the server. You can handler messages **sequentially** (i.e. one after another).

For this assignment, create a new Telegram bot, and use the `\setcommands` function in the BotFather bot to create **three commands** for your bot (see [https://core.telegram.org/bots#6-botfather](https://core.telegram.org/bots#6-botfather)). The user can use these three commands to interact with your recommender system.

* `/start`
    - A command to register with the application. On receiving this command, the Telegram bot script should:
        1. Send a request to the server's "Start API" with the user's `chat_id`, to check whether the user is a new user or an existing user
        2. If user is new, reply "Welcome!", else reply "Welcome back!"
* `/rate`
    - A command to ask the application to present a movie for rating. On reciving this command, the Telegram bot script should:
        1. Send a request to the server's "Rate API" with the user's `chat_id`
        2. On receiving the movie information from the server, send the user two messages:
            - A message containing the name of the movie, and the URL to the movie's page on IMDB
            - A message asking for the user's rating on this movie, with a custom keyboard
    - Note that you should store the movie's ID in the callback data, such that you know which movie the user has rated when you receive the user's rating
    - An example is shown below

<center>
    <img src="assignment-3-rating.png" width="50%"/>
</center>

* `/recommend`
    - A command to ask the application to recommend a list of movies based on previous ratings. On receiving this command, the Telegram bot script shoud:
        1. Send a request to the server's "Recommend API" to ask for the **top 3** recommended movies for this user.
        2. Upone receiving the response from the server, format a message with the following information and send it to the user
            - Title of the movie
            - The URL to the movie's page on IMDB

### The Application Server



## What to Submit

You should prepare **two files** to be submitted for this assignment:
* **bot.py**: the script in which you implement the Telegram bot
* **app.py**: the script in which you implement the Flask application for movie recommendation

You should put these two files in a folder named <student_id>_assignment1 (e.g. 12345678_assignment3), and compress it into a zip file (e.g. 12345678_assignment3.zip). Submit the compressed file to Blackboard.
