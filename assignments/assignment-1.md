# IEMS5780 / IERG4080 Assignment 1

## Text Classification and Telegram Bot

* **Deadline**: 21st September, 2018 (Friday)

In this assignment, you will build a text classifier of movie reviews, and then deploy the text classifier as a **chatbot** on **Telegram** to allow other people to use it.

### Task 1 - Training a Text Classifier

We will use a randomly selected subset of data prepared by Xiang Zhang, described in the paper “Character-level Convolutional Networks for Text Classification” (https://arxiv.org/abs/1509.01626).

The dataset contains 110,000 articles assigned to 1 of the 14 classes listed below.
Company
Educational Institution
Artist
Athlete
Office Holder
Mean Of Transportation
Building
Natural Place
Village
Animal
Plant
Album
Film
Written Work

You will have to submit a Jupyter notebook that shows your steps of training and evaluating the text classification model. The notebook should contain the following:

Build a Naive Bayes classifier
Use the MultinomialNB class in scikit-learn
Compare the performance of using the CountVectorizer vs. the TfidfVectorizer for feature extraction, using 5-fold cross validation
Performance should be measured using accuracy_score
Pick the better approach, split the dataset and use 70% as training set and 30% as test set, and train a new model
Plot the confusion matrix and classification report of the new model’s performance on the test set
Save the model using scikit-learn’s joblib module
Build a fastText classifier
Use the fastText library from Facebook
Split the dataset and use 70% as training set and 30% as test set, and train a model
Plot the confusion matrix and classification report of the new model’s performance on the test set
Save the model using fastText’s save mechanism
Answer the following questions
Which two classes are most confusing for the two models you have built? (i.e the samples from these two classes are most likely to be wrongly classified into each other by the models)
Given the models above, you can classify an input text into one of the 14 classes. If you are also required to predict whether the input text does not belong to any of the 14 classes, what would you do?

Task 2 - Deploy Your Model as a Telegram Bot

By now you should have two models: 1) the MultinomialBN model, and 2) the fastText model. The next task is to deploy the models so that other people can use it. To skip the troubles of deploying a UI for the application, you will deploy the models as a Telegram bot.

Check the Telegram bot platform (https://telegram.org/blog/bot-revolution) and the Telegram Bot API (https://core.telegram.org/bots/api). Check also the Telepot framework for developing Telegram Bot in Python (https://github.com/nickoala/telepot).

Firstly, you should create a Telegram bot by following the instructions at https://core.telegram.org/bots#3-how-do-i-create-a-bot. This bot will be used in latter assignments as well.

You can easily develop a program that continuously consumes messages from a user on Telegram, process the messages, and sends back responses to the user. Below is an example bot, which will simply echo what was sent by the user.

import time
import telepot
from telepot.loop import MessageLoop


def handle(msg):
    """
    A function that will be invoked when a message is
    recevied by the bot
    """
    content_type, chat_type, chat_id = telepot.glance(msg)

    if content_type == "text":
        content = msg["text"]
        reply = "You said: {}".format(content)
        bot.sendMessage(chat_id, reply)


if __name__ == "__main__":
    
    # Provide your bot's token
    bot = telepot.Bot("YOUR_TELEGRAM_BOT_TOKEN")
    MessageLoop(bot, handle).run_as_thread()

    while True:
        time.sleep(10)

Your bot should fulfil the following requirements:
If the user sends a message that starts with “nb:”, then you should pass the rest of the message (by removing “nb:” from the input text) to the naive Bayes model to predict the category of the text, and send the category (e.g. “Company”) to the user
If the user sends a message that starts with “ft:”, then you should pass the rest of the message (by removing “ft:” from the input text) to the fastText model to predict the category of the text, and send the category to the user
If the user sends a message that neither starts with “nb:” or “ft:”, the bot should always reply with the following message: “Sends me a text message starts with either ‘nb:’ or ‘ft:’”.
Your bot should load all the models into memory in advance, before answering any message from the user.

What to Submit

You should prepare two files to be submitted for this assignment:
assignment1_task1.ipynb: the Jupyter notebook in which you have done Task 1, including all the source codes, results and figures
assignment1_task2.py: the script in which you implement the Telegram bot to perform text classification on user inputs

You should put these two files in a folder named <student_id>_assignment1 (e.g. 12345678_assignment1), and compress it into a zip file (e.g. 12345678_assignment1.zip). Submit the compressed file to Blackboard.
