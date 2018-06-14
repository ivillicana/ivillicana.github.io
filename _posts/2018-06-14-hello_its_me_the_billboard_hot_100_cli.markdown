---
layout: post
title:      "'Hello, it's me...': The Billboard Hot 100 CLI"
date:       2018-06-14 18:41:41 -0400
permalink:  hello_its_me_the_billboard_hot_100_cli
---


I knew it was coming up. 500 feet, 100 feet, 5 feet… “This is going to be a piece of cake. Triple chocolate cake with cream cheese frosting!”, I said to myself when I finally had arrived at my first major portfolio project: the CLI Data Gem. I had spent some time preparing mentally for it. I had a basic idea of what I wanted to do and how I was going to accomplish it. 

But I was still overwhelmed. Not so much because I didn’t know how to do it. After all, I had finished many labs and mini-projects before. But reading the instructions made me feel like it was going to much to handle. The “Impostor Syndrome” is real! I had much confidence in my skills. But now I was afraid others would expose me as a fraud. So, I put off the project for a month (to be fair, my wedding day was imminent, as well as a much needed honeymoon).

In fact, when I returned to my normal daily routine, I still couldn’t start my project. I actually skipped ahead and started working on SQL, ActiveRecord, and Rack before I came back to the CLI project. But now I was determined.

To say that getting started was a challenge is a severe understatement. I had to review some Ruby code, as well as the Nokogiri gem. I began to watch some of the walkthroughs. I read various materials. I even skimmed through other persons project’s code to build an idea of what I wanted. 

My idea was to build a CLI gem that would use Nokogiri to scrape the Billboard Hot 100 chart. I doodled, with pen and paper, a basic application structure. Then I began to code. I had read a few suggestions from a blog that stated the KISS principle: “Keep it simple, stupid”. Yes indeed. So rather than starting with 100 songs, or objects, I decide to keep it simple with only 10. Still scraped with Nokogiri.

Bundler was used to build the gem and all its eventual dependencies. I built a Song class that was tasked with scraping the data and then creating objects for each song in the Billboard chart. Those objects would then be pushed into an array that is accessible to the CLI class. The CLI class is responsible for the actual interface of the application. It provides the messages, options, and selections that will provided to the user. 

Once I had an initial working version of the application, I expanded its features by including all 100 items in the Billboard chart, organized those items into 10 ranges, and included a main menu that a user can always return to. Expanding the application features became tricky at times. And this was the most challenging aspect of the project, where most of my errors, and consequently, hair ripping occurred. But jumping those hurdled was oddly satisfying. Those errors taught me new things, intricacies of the Ruby language, and motivated me to go out and research how to solve the error.

Finally, I had a fully functioning application. Of course, throughout this project, I was pushing countless commits to my GitHub repository. Once I was sure that the application was working, I recorded a brief walkthrough in which I narrated how a user can use the application. And I even went as far as letting my wife test it out. Also, I published the gem to rubygems.org, which was a first for me. 

I learned much about Ruby, object-oriented programming, errors, and yes, how low the standard is to make it into the Billboard Hot 100 chart. But the most important thing I learned was about myself. I can do it! I am not an impostor! I’m renewed with excitement and enthusiasm to learn more about programming and web development.

![](https://i.imgur.com/Uk8VEF1.jpg?1)



