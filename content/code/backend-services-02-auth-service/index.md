---
title: "Backend Services - Auth"
date: 2019-07-06

categories: ['Game Development', 'Backend']
tags: ['multiplayer', 'backend', 'auth']
author: "Emanuele Manzione"
noSummary: false

resizeImages: false
---
As I anticipated in the previous article, the first thing I would like to have in my backend is the Frontend Service. Just to recap, it can validate a request and then route it to the correct subservice.
In next articles I am going to describe how I am implementing it, explaining why I decided to do something in a specific way instead of another one. Of course I am opened to your feedback and comments, so be sure to let me know what you do think!

So let's apply a little bit the *"divide et impera"* approach. The Frontend Service has to perform:

- __requests authorization__: is the arrived request coming from an authenticated user? If the answer is "no", the request can be dropped and no additional resources should be spent
- __requests validation__: is the arrived request properly formed? I can include multiple checks here: header correctness, request's length boundaries, etc
- __requests routing__: can this service complete the request on its own? If the answer is "no", then it has to be pushed deeper in my architecture, to the correct subservice

### Requests authorization

The first block I want to build is certainly the __*Authentication Service*__: I will treat it in this article. Every request will need to be tested against it, in order to be further processed.
For the specific implementation I was thinking about a simple HTTP API, with simple functionalities:

- __login__: the user's session is started and initialized if the passed username and password are correct
