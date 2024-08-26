+++
title = "Comparing carsharing prices in Berlin"
date = 2024-08-25
weight = "20"
meta = "false"
+++

## Introduction

Riding from one place to another in Berlin can be time-consuming. The city is vast, buses & tram are only available in either part of the city and you mostly end up with 45+ min trips from one central place to another. Carsharing is your other option and what can I say: guilty. My partner and I very much enjoy the liberty of taking a car from one place to another and just leaving it there without worrying about taking the ride back. Nevertheless, it is not cheap and price sensitivity kicks in.  

## What we did in the past

Doing the math in our head. There are four major carsharing providers in Berlin (ShareNow, Miles & Sixt Share), which are also integrated within FreeNow, the Mobility-as-a-Software app of choice, plus Bolt as a standalone. Based on the different pay-as-you-go prices and the help of Google Maps, you somewhat try to estimate the total price at the end of the ride.

I had some time to spare and wanted to work on a first frontend project so here is a high-level description of how to have a better overview of carsharing prices in Berlin.

## Initial requirements

Requirements were simple:

- Be platform agnostic, i.e. a webpage
- Take an end location as input (eventually a changing starting point)
- Calculate an initial route to get there from a set starting point
- Visualize this route
- Show the different prices for the respective vehicles of all providers

I had some personal additional requirements for tools & stack:
- No upfront costs for APIs or tooling
- App is in Typescript


## Development Process

### Initial plans

Given that I do not have any prior experience with any frontend work but Flask, a Typescript walkthrough was a first step. Classes are a very nice concept, although not so much needed as part of this first MVP.

The app needed a map as a background, one of the major providers for hobbyists is Mapbox, which does not require any payment for the first calls. Google Maps might be more elegant, especially for route planning later on but is quite expensive.

I first wanted to fetch the positions of the cars and show them with the respective prices in the app. Given my previous experience at Tier, I thought you could easily fetch the respective vehicles from the OpenAPI integration. In the end, not possible without work through MiM & Charles, thus (still) relying on some manual work here.

The same counts for the prices of all vehicles, which have to be saved within the service rather than fetched with each request. I therefore have to update the prices for each provider, should they change their pricing structure.

### Building & asking for a fundament

As I still had very limited knowledge of Typescript, I wanted to come up with the base through prompts & engaging with Claude. I simply chose Claude for more convenience in project structure & wanted to test their Opus model.

What can I say, either my prompts were genius or Claude knew exactly what I was up to. It took me a couple of iterations to adjust the files based on the first trials with provider APIs and then leave them out. In the end, the app worked and is able to take an end position & calculate the prices.

### How are the routes calculated?

The missing piece of the puzzle is the route calculation & display. How would you select a destination & a name?

[Mapbox Directions API](https://docs.mapbox.com/api/navigation/directions/) offers the possibility to calculate the time & distance between two locations based on average driving patterns. This comes in handy, as a sole provider for all calls is needed. 

The only thing to add to the code is the conversion of street names & locations to lat/long coordinates, which is also a function within [Mapbox Geocoding](https://docs.mapbox.com/api/search/geocoding-v5/). 


## The Look

At this early stage, I set up the repository & deployed it with Vercel. This worked great and is therefore accessible through a public URL. 

{{< figure src="/carsharing.png" class="mid"  caption="First deployment of the app, looking for a way to get to a Restaurant in Berlin. In this case, Bolt is by far the cheapest option, followed by Miles." >}}

There is no active development going at this stage, as I am happy with the utility at this point, although points of improvement already popped up.

## Moving forward

Some QoL improvements are already planned in the near future:
- Allow destination suggestions, as you have to sometimes enter the postal code to get the right location
- Set up multi-stop routes in case you want to pick up friends along the way
- Ask for location requests to make a more precise route calculation
- Include multi-modal paths: Using the perfect blend of public transport & carsharing to reach your destination. Google does not do a great job at this and might be worth a shot.

There is no concrete timeline at this point, although I am curious whether this is something others would benefit from. Shoot me a message, happy to share the link to the page for testing!