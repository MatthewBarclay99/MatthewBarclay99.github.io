---
title: "Discord free food bot"
permalink: /Projects/Discord
#theme: jekyll-theme-cayman
id: discord
---

# Discord Free Food Bot

## Links

[Python Script Repo](https://github.com/MatthewBarclay99/Winner-Winner-Chicken-Dinner/tree/main)

[Discord Bot Docker Image Repo](https://github.com/MatthewBarclay99/DiscordChickenMessageBot)

## About

When I moved to Southern California, I noticed that most of the local sports teams had promotions in place depending on their performance. The first one I received was a free Chic-Fil-A sandwich from the Angels scoring 7 or more runs at a home game. After I got the first sandwich, I started tracking the Angels scores on my phone through the ESPN app and would alert my friends when the requirements were met. In order to claim the rewards, the app has to be opened before midnight, so there was always a time crunch to check nightly.

This inspired me to see if there were any sports score APIs that could be easily queried and compared to the reward requirements so that I would not have to manually check the scores. I started out with a simple Python script that would query a free API from www.thesportsdb.com. While this worked, the free API did not update their scores fast enough and therefore the script would not identify an available reward until the next day, too late for many of the rewards to be claimed. Therefore, I switched to an ESPN endpoint that I found from some Google searching and rewrote my API requests to fit this new API. The ESPN API updated almost instantly and was able to quickly check all of the local sports team's scores and their associated reward conditions.

Finally, I needed to host my script on an external server, as I could not just leave it running on my PC in the background and it would be offline whenever I turned it off for the night. I ended up picking up a little Raspberry Pi Zero 2W to self-host my Python script. In addition to this, I decided to build a Discord bot around the Python script to make the script interactive and to broadcast the available rewards message to my friends in an easily distributed method, just sending a message in the Discord channel where the bot is running. To accommodate these changes, I forked a simple timed message bot repo and added my Python script, while tuning the interactive features to fit the goal of my bot. I then built a Docker container and image of the Discord bot Python code and shared it with the Raspberry pi server via Docker Hub. While I attempted to use github actions to automate building the Docker image on the Raspberry pi itself every time I pushed a new version, the pi was just not powerful enough to build even my simple Docker image.

The final version of the bot is running 24/7 and will check the scores of each sport at 10:10pm PST, just late enough to have the games completed while early enough to collect rewards before midnight. The bot also listens on the Discord chat for commands, where it can change the time the daily message will be sent, blacklist certain days of the week, and check what possible rewards could be available today based on which teams are playing and are at home. Finally, it can also run the daily query ad-hoc if a game has ended earlier in the day.

This project was a lot of fun and very difficult, as I had not previously used APIs in Python, Docker, or a Raspberry pi. The Python script was the easiest part and I think my use of a dictionary to hold all aspects of a reward and the helper function used to check the reward conditions was a really smart way to organize it. Using Docker for the first time was tricky as I ran into issues with the Raspberry pi not being able to build the image and instead had to build a linux-based ARM64 image on my Windows PC. It was a great learning experience and I understand the processes behind Docker a lot better now. Finally, I have always wanted to play around with a Raspberry pi, so I'm glad this project gave me a good excuse to do so. It was fun to boot it up, customize the shell scripts to automate the Docker container composing, and setting it up for constant headless operation. It barely uses any power while adequately running the Python script. This was the biggest and most rewarding personal project that I have worked on, and I intend to continue improving it with methods to add rewards and conditions ad-hoc and more interactive features. I may also create other Discord bots in the future, as I can see a wide variety of use cases for my day-to-day life.


{{ site.github_badge }}