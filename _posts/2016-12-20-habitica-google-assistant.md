---
layout: post
title: Google Assistant to Habitica To-Do List 
---

I've been using [Habitica](https://habitica.com) for a little over a year now and absolutely love it. It's basically just a complicated To-Do list with some different options around repeating tasks with a mix of gamification to keep me interested. Over the past couple of weeks there have been times when I have found myself having my hands full and not being able to manually add tasks when I wanted to. So the next obvious step is to figure out a way around that.

## Google Assistant

I recently got the Google Nexus and have been attempting to work my entire life around Google Assistant. My problem seemed like an obvious candidate to be solved using the voice commands with my phone, so I started investigating into the Assistant. Unfortunately I couldn't find any way of hooking up the Google Assistant directly to Habitica. So I figured I would need to add some sort of intermediary step between Google Assistant and Habitica.

## IFTTT and todoist and Maker

I've used [IFTTT](https://ifttt.com) for automating a few random things in my life, so checked out IFTTT first. Stumbled upon [todoist](https://todoist.com) as a great "this", it works perfectly with Google Assistant and seems to be easily configurable.

For the "that" section, I needed to be able to connect to Habitica. Habitica has a pretty decent [API](https://habitica.com/apidoc/), tested it out in Postman and seemed to fulfill my needs:

headers:
![Habitica Headers](/images/habitica-headers.jpg)

body:
![Habitica Body](/images/habitica-body.jpg)

I found a "that" section called "Maker" in IFTTT that allows you to send HTTP requests. The only problem with Maker is that it doesn't let you supply headers with the request, which obviously means that I wasn't going to be able hit Habitica directly from IFTTT.

## Intermediate Node.js App

Since I can still make HTTP requests from IFTTT, I decided to throw together a Node.js application that sits between IFTTT and Habitica. The simple app had the following requirements:

1. Can receive requests with everything in the URL.
2. Has some type of token authenication so that I can verify that only I can add tasks to my To-Do list
3. Has the ability to make requests to Habitica with my Habitica API credentials and a task.

[This](https://github.com/MattJGlick/habitica_todo_exchange) is what I was able to come up with. Super simple application that does some basic key checking for verification, then makes a request to Habitica with the required tokens and the task to be created. Most of the logic sits on the index.js file and is as follows:

```
    var express = require('express');
    var request = require('request');

    var app = express();

    app.get('/todo/:key/:task', function(req, res) {
        if(req.params.key == process.env.SECRET_KEY) {
            request({
                url: "https://habitica.com/api/v3/tasks/user",
                method: "POST",
                headers: {
                    "content-type": "application/json",  
                    "x-api-user": process.env.HABITICA_USER,
                    "x-api-key": process.env.HABITICA_KEY 
                },
                json: { 
                    "text": req.params.task, 
                    "type": "todo" 
                }
            }, function (error, response, body){
                if (error) {
                    console.log(error)
                }

                if (response.body.success) {
                    res.send("Successfully added " + req.params.task)
                } else {
                    res.send("Something broke...")
                }
            });
        } else {
            res.send("Bad key")
        }
    });

    app.get('*', function(req, res) {
        res.send("Correct path: /todo/:key/:task")

    });

    app.listen(process.env.PORT || 3000);
    console.log('Listening on port 3000...');
```

Once it was all good to go, I pushed it up to Heroku so I can access it from IFTTT. To utilize it, it's just a simple get request to "/todo/:key/:task", where `key` is the UUID that I created for the app and `task` is the new task to be added to my To-Do list.

## Wrapping Up

So the final workflow for the "task" is as follows:

1. I tell Google Assistant: "Note to self, mow the lawn"
2. Google Assitant adds the task to my todoist list
3. IFTTT polls my todoist lists for new tasks and picks it up
4. IFTTT triggers and calls my endpoint with the endpoint API key
5. My endpoint verifies the key and hits the Habitica API with my API user/token and the new task
6. Habitica adds my new task to my To-Do list.
    * *I probably procrastinate mowing the lawn anyway...*

It was a bit frustrating that Maker doesn't allow for headers, but was able to get around it with my quick app. Ideally long term the better solution would to be able to go right from Google Assistant to Habitica, but for now I have filled my needs!

If anyone has any suggestions or improvements feel free to shoot me an email.

