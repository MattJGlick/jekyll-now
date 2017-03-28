---
layout: post
title: Office Quotes Twitter Bot
---

I am absolutely obsessed with the TV show, The Office. My friends and I are constantly quoting the
show. So much so that I decided to make a twitter bot that randomly tweets out quotes! I was hoping
to be able to find a database or an API with a substantial amount of quotes, unfortunately I haven't
found anything like this. So this is where my work began.

# Office Quotes RESTful API

I started out building an RESTful API with Node.js app, express framework and a postgres database. 
The source code for the API is up on [github](https://github.com/MattJGlick/office_quotes_api/tree/develop) 
The API has the following endpoints:

- /quotes GET: returns all of the quotes in the database
- /quote GET: returns a single random quote
- /quote POST: inserts a single quote with a "quote" and an "author"
- /api_key POST: creates a new API key for a user 

I have a middleware set up to require an API key that allows me to verify the user using the API. 
As of now the API key is required for both creating and viewing the quotes. I think I might later
open it up such that the API key is only required for creating quotes.

The postgres database is up on heroku, which is where I also am running the API. This allows some
seamless integration in terms of connecting and authentication.

Finally I integrated [swagger](http://swagger.io/) to make using and testing the API easier. Since
the app is up on Heroku I can access the docs [here](https://officequotes.herokuapp.com/docs/#/)

Overall the API is working really well. The hardest part from here on out is adding quotes!

## Ideas to improve:

- Keep a count of the randomly returned quote such that least used quotes are used first.
- Add for a bulk upload of quotes
- Add endpoints for retrieving quotes by specific characters
- Rate limits on the endpoints

# Office Quotes Twitter Bot

Now that I had the API written, I just needed to integrate a Twitter account. I snagged the name
"OfficeQuotesBot" and changed the picture to a good photo of my favorite character Michael Scott

![Michael Scott](/images/michael.jpg)

Then I set up a Node.js app that will also sit up on heroku and using the twitter API and my API,
tweet out different office quotes. Originally I had planned on using a cron job like Node package 
called node-cron. Then I found out that heroku has a built in scheduler. This would allow me to have
heroku do all of the leg work in terms of scheduling the tweets.

The best option was to use their one hour scheduler. 

![heroku cron](/images/heroku-cron.png)

However, I didn't want to have it tweet every single hour. I wouldn't be able to keep up with the
need for new quotes constantly. So every hour it has a 30% chance of tweeting (Update, this was pulled into an 
env var to allow for easier updating). Which adds a nice bit of randomization to the bot.

Once the tweeting on a random interval was handled, it was good to go! It's now live at 
[https://twitter.com/OfficeQuotesBot](https://twitter.com/OfficeQuotesBot). Now I just need to amass
some twitter followers!

## Ideas to improve
- ~~Pull the randomization at which it tweets out into an env var.~~ Implemented
