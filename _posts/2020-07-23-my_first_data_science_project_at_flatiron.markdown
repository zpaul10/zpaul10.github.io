---
layout: post
title:      "My First Data Science Project at Flatiron"
date:       2020-07-24 02:56:32 +0000
permalink:  my_first_data_science_project_at_flatiron
---



Come up with a list of successful types of movies. That was basically the prompt for my first project, which on its surface seemed like it would be very easy. All I'd have to do is check IMDBs interface, download whatever .csv they have, and get to work. I should've known it wouldn't have been as easy as that.

My first roadblock was that I didn't have access to any budget or profit information from IMDBs interface. So I had to scrape it from a different site. Luckily, the-numbers.com had revenue information for thousands of movies all organized in an easy to scrape table. I scraped that information very easily but I quickly ran into a second problem. The movie titles from the scraped site weren't all unique; some movies have the same names. Fixing that also wasn't a huge issue, I had release dates for the films in both datasets so I could match up the years in addition to titles. 

By this point I had the data I was looking for. I had the genre of each film, when it was released, how much it made and how much it cost (I had a lot more than that, but for the purposes of this I'm going to focus on the genre.) All I had to do here was make some plots, and draw some conclusions. Again this seems like such a simple task to do, I could make a plot taking the mean profits for each genre made in the last 20 years. But that's not going to give me terribly useful information, some genres are more successful at different parts of the year, and I would have to consider that maybe a film released in February would do much better if that same film were to be released in June instead. So I need to break it down a little bit more, how does each genre of film do depending on what month it was released. I found that summer and winter are where the big hits typically are released and those hits are usually action or adventure films, while spring and fall have less success. 

So I want to release a movie in the summer, and I want it to be an action or adventure film. That was the furthest I took this particular project, but if I were to continue on with it, I would then go a step further and determine who I want working on it. Simple enough, create a list of living actors, directors, producers, find the ones who've been in very profitable action/adventure films, and add them to my list. 

I know this project has flaws in its design and execution but I do want to have something I can look back on and see what I did wrong so that I can say that I've improved and learned something about data science between now and then. 

-Zach
