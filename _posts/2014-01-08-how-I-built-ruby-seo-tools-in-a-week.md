---
layout:       post
title:        "How I Built Ruby SEO Tools in a Week"
description:  "Find out how I built Ruby SEO Tools, a fully functional web application, in under 50 hours."
date:         2015-01-08 12:00:00
tags:
  - hackathon
  - planning
  - project management
author:       George Banis
---

## TL;DR

Not long ago, I decided to combine everything I know about SEO with my web development skills into a web application. This is how [Ruby SEO Tools](http://rubyseotools.com) was born, a tool that helps marketers analyze how well their blog posts are optimized for SEO.

The first version of Ruby SEO Tools was built in just a handful of days&mdash;it could very well be the product of a hackathon. And since many friends of mine want to participate in a hackathon and aren't sure *how* to get organized, I decided I'd document my process in hopes that you could get an idea or two.

Keep reading to find out how I built a fully functional web application in under 50 hours.

## First, Lets Set a Few Things Straight...

1. Don't expect to produce an enterprise-level, feature-rich application in just a few hours.
1. Brainstorm as many features as you wish. Then select a single feature and implement it.
1. You should have a plan of action. If you don't you'll run in circles.
1. If you have a team, it helps if you all have different skills.
1. Try something out of the ordinary and have fun.

Now that we got these things out of the way, here's how I built the first version of [rubyseotools.com](rubyseotools.com)

## Before Starting to Code

### Inspiration for the Project

Coming up with an idea for your project is obviously the first thing on the list.

I had a few things in mind that I wanted to build but obviously when you are about to invest a good amout of time on something you want to make it count.

It obviously helps if:

- You have experience in the topic
- You know that there is pain involved and that you could aleviate some of that pain

Once I finalized the core idea, I started taking notes. I brainstormed, talked with friends and colleagues and put all my ideas (good and bad) in a document. This is not the time to decide whether they are good or bad. My main goal was to collect a good amount of ideas.

### The "Project Plan"

I created a Google Doc and put in it all the following:

#### About

Here's where I listed the name, logo, url and description of the project.

#### Features

In this section I went wild, literally. I wrote down as many ideas and features as I could.

Quickly I started realizing what my starting point should be:

> A tool where a marketer can provide the URL of his/her blog post and get a report with SEO recommendations.

#### User Experience

With the core idea in place, I started creating some basic user stories as well as the user flow from when a visitor arrives to the home page until they are done with the tool.

#### SEO Performance Metrics

By now, the idea has taken some shape and form. At this moment, I had to decide which metrics I should implement in this first version.

I had two main criteria:

1. How much value is the end-user going to get from the metric
2. How easy is it to implement this metric

With this in mind I gathered a set of about 15 metrics that I knew I could develop within a few quick hours. This was great starting point that I could then use to build on.

#### Database Architecture

Nothing out of the ordinary here. With all the information in hand I built my models. It's always a good idea to start simple and add complexity if necessary.

#### Technologies I Want to Use

Pretty obvious but I made a list of all the things I wanted to implement:

- Rails API for my back-end
- Angular.js for my front-end
- RSpec to test my business logic and models
- Code Climate for code review and test coverage
- Gemnasium to check dependencies
- Codeship for continuous integration
- Heroku to host Rails
- Github to host HTML/CSS/JS
- Nokogiri for HTML parsing

## Developing the Application

### Service Oriented Architecture

Naturally, the first thing once you have everything ready is setting up your environment and initializing your project.

For this project I used the following architecture:

![Ruby SEO Tools - Architecture](/assets/ruby-seo-tools-architecture.svg)

I knew I would have my front and back ends separate so two different local repos were in order.

These repos were then linked to their respective Github repos.

Back-end, I linked my GH repository to Gemnasium to make sure my gem dependencies were in good order. I set up Codeship to pull from Github, run the tests and push to Heroku if everything passed. And of course set up New Relic to monitor my Heroku server.

Front-end, I didn't write tests so I simply tested locally and pushed to a gh-pages branch when everything looked good. I added Google Analytics to keep an eye on traffic and got a custom domain which I routed through Cloudflare DNS. And of course, Angular chats with Rails through a RESTful API using AJAX.

### Setting Up Environments

You can start seeing how everything is coming along nicely.

Two folders, one for each end. In one, I initialized a Rails API application running Postgres. In the other, I created the boilerplate files and folders, including Angular and Bootstrap through Bower.

### Defining End-Points for my API

For each report that the end-user would like to generate I wanted to make a single call to the Rails server and get a pass response with the report data or a fail response.

Simple enough, right? That's my goal, given the limited amount of time.

### Developing the Back-end

Here's where the real coding begins.

Even though I had limited amount of time in hand I still wanted to do TDD so I decided to test my business logic and selectively test my controller and models.

So, as you can imagine I started writing tests for my SEO analysis and built a module that hosts all the methods that do that.

Once my server was consistently delivering a RESTful endpoint, I pushed it on Github and soon had it live on Heroku via Codeship.

Finally, I set a custom subdomain for my API server, api.rubyseotools.com, and now I was ready to start building my front-end.

### Workin on the Front-end

I wanted to try Angular Material but after spending a few hours on it, I realized that it would be more trouble than I thought.

So, I went with a combination of Angular.js and Boostrap which I was familiar with and could start developing immediately.

Nothing too special here, I put together a factory to communicate with my API and then designed a simple front-end UI that displays the information.

## Getting Past v0.0.1

With a first functioning version of my application, I started implementing more SEO metrics using the following process:

- Pick the metric
- Write the tests
- Write the code that makes the tests pass
- Expose it to the API
- Pull it and display it on the front end
- Make sure everything looks good and tests pass
- Push to production

## Polishing and Marketing

I consider this step is very important so I gave myself enough time to polish the front-end and make it look great everywhere (yep, I did do some cross-browser and cross-device testing).

I also took some time writing a few nice words and making gifs so that visitors have a delightful experience when they visit for the first time and know what to do when they get there.

## Final Thoughts

As you see, planning is equally as important as developing in my eyes. If you have a roadmap you'll have a *significantly* easier time building your project.

Also, many think that TDD takes up a lot of time but I really feel like it's much faster than manually testing everything all the time when you can simply run the tests.

Finally, hackathons and small projects like this one are lots of fun. So no matter what happens, make sure you enjoy yourself!

I hope this helps and would love to hear what your thoughts are in the commends below.





