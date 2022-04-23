---
title: "A (Not So) Brief Overview Of This Site's Setup"
date: 2017-11-14T22:40:00-06:00
lastmod: 2022-04-23T11:25:55-06:00
draft: false
---
> Editor's Note: This was originally posted on my previous blog platform. While building that site was a great personal learning experience, it wasn't totally practical to maintain and has since been replaced.


It seems only fitting to have the first post of a self-built blog to be about, well, the blog! I'll list the technologies I used and why I chose them. In a later post I'll cover details on how I put them together.
## The Stack
- Digital Ocean VPS Running Ubuntu 16.04
- Docker (Using Docker-Compose)
  - Web server (frontend/backend)
  - PostgreSQL
- Go (Backend)
  - dgrijalva/jwt-go (Auth)
      <li>gorilla/mux (HTTP Routing)
      <li>jinzhu/gorm (ORM/DB Interface)
  
  <li>React(Frontend)
      <li>Mobx (state)
      <li>SCSS (styling)
  
## Frontend&nbsp;
The frontend consists of React (w/ Babel), and Mobx for state management. Styling is done with the ever-wonderful SCSS, a variant of Sass. I'm using a few plugins, including the excellent [react-rte](https://github.com/sstur/react-rte) package which makes editing content on this site a breeze. The client/server interface is handled by my own API wrapper, but I plan to switch to something more robust like Backbone.
Using React for this site was an easy choice. After wrangling with manually generated HTML inside Javascript for years, the recent influx of better client-side tooling has been more than welcome. Even before this project I've had my eyes on Angular 2/4, Vue.JS, [Mithril.js](https://mithril.js.org) and React. Soon after deciding on Angular 2 (and then 4) as my frontend tool of choice, I became interested in alternatives. I test drove both Vue.JS and Mithril, but ultimately settled on React.
Initially, I had stayed away from React in part because the JSX within the components seemed awkward. The inline markup reminded me of manually generating HTML in Javascript, so I had Angular which used a more familiar (if somewhat quirky) template system. However my initial fears of an overly-crowded component turned out to be unjustified. By combining concise CSS, reusable components, and though-out state management, it's not hard to have very manageable components in React.
SCSS was by far the easiest technology chose I made for this site. Variables, imports, mixins and nested rules are incredibly useful when trying to build consistent style, all while being able to tweak things easily. The features are easy to learn, but valid CSS is inherently valid SCSS, so mixing it in (pun intended) is easy-breezy.

## Backend
Most of the web-based applications I've built and worked on over the past few years have been [Django](https://www.djangoproject.com/) projects. The Django framework is fantastic for form-driven applications, and applications with complex data models. The ORM layer is an absolute dream, the built-in authentication models are powerful, and the auto-generated admin site is a huge productivity booster. I could go on singing Django's praises, but all of Django's benefits are exactly why I was itching to try something new. That, coupled with a lack of a native Restful API integration and frustration with available plugins* to add such features fueled my search for something new.
So at this point, I knew I wanted to write the frontend in React, and I wanted a supporting backend. I liked Django's ORM, but I could do without the friction I had experienced between a React-style app and Django's Auth framework. Learning a new language sounded fun too, so I added that to the mental list of requirements.

Thus, my list of not-too-technical requirements was born:

  - Not Django
  - A language I don't have much experience with
  - React-friendly API, likely REST
  - Sane Authentication
  - Snazzy ORM

From this point I was off to explore options that somewhat fit those requirements.

**Option 0: Django with GraphQL**
Ok, so not really straying from Django, but this would be using a plugin to provide a GraphQL service that could be consumed by Relay Modern on the client. That kind of setup really seems nice. However, after initially setting up a dummy project to play around with React/Relay Modern + Django/Graphene I quickly hit a sore spot. Graphene (at the time, possibly still today) wasn't totally compatible with Relay Modern. Combined with it still being Django (see above) I scraped this idea and moved along.

**Option 1: Node/Express**
This one seemed clear, despite my experience with Javascript. Since I'd be writing the frontend in Javascript, why not the backend too? I actually initially settled on this stack, and began stubbing out a skeleton for this site. I chose MongoDB + Mongoose for persistence, and Passport.js for authentication. This stack stack seemed great, and I set about adding basic CRUD functionality -- until a yearning for learning a new language nagged at me again. <em>"I've done this before" nagged the voice in my head. I had, but don't they say practice make perfect? Maybe, but that gets boring! &nbsp;So I went back to the drawing board...
_Note: If this was a commercial website, collaborative project , or almost any other type of website, there's a strong chance I would have continued to use this stack. It's common, supportable, and each of the projects I mentioned have a pretty substantial developer/user-base. So really, the only reason I decided against a Node/Express stack was familiarity!_

**Option 2: .NET Core 2.0 + Entity Framework Core**
This setup was a strong contender. As above, it doesn't check off box #2, but I had hope! After having used .NET Core 2.0 with Entity Framework Core as a basic data store for a Chrome Extension, I was impressed. Database drivers for MySQL and PostgreSQL were first-class and quality 3rd party, respectively. After spinning up a starter project with local authentication, it really seemed to be good to go. However, after attempting to combine .NET Core's native Rest API components and native authentication system, I ran into issues -- not unlike my attempt to shoehorn Django's built-in auth framework into something React-friendly (don't do it). Luckily there was a 3rd party package that could help with REST API authentication. It seemed great, until I read through some of the open issues and found that the project only supported .NET Core 1.x, with no real word on 2.x support. Coupling that with some relatively high memory usage I was seeing for my very simple Chrome Extension REST API service, I figured I'd look for something else.
_At this point (or even before!) you may have the urge to call me crazy, bonkers, or mildly insane for hopscotching from one stack to another. That's totally fair. Please leave your insults in the comments -- if I ever get around to adding them.__

**Option 3: Ruby/RoR**
While RoR is used in a lot of projects and would have fit nearly all of my arbitrary requirements, I ultimately decided against it. Firstly because Ruby has never really piqued my interest, namely because of my (**certainly biased, probably incorrect**) assertion that _"Ruby is like Python, but not as good."_ Couple that with a number of RoR's direct similarities with Django, and I wondered how far out of my comfort zone I'd actually be.

**Option 4: PHP**
Writing this site in PHP would have been a throwback to my first days of making server-side web ~~abominations~~ applications. My slight distaste the actual language aside, it seemed only logical to consider using PHP. Plus, I hadn't used modern (&gt;~5.6) PHP it couldn't hurt to give it another go. In terms of frameworks, I'd heard of Laravel and Symfony before. After a little searching, I went ahead and spent a couple hours with Laravel. I was very impressed with the built-in features, with many of them seeming to parallel those found in Django. However, because of those parallels and my initial preference to avoid PHP &nbsp;led me to look at more alternatives for this particular project. That said, I've got some ideas of what I may use Laravel for in the future.
_Now, I can only hope I've riled you up, insulted your favorite language and given some weak reasons for not using a great stack. Who knows, maybe that was my plan. Perhaps I actually wrote this all in Elm and Haskell** and this is me bashing everything else. 😀&nbsp;_

**Option 5: Rust/Swift**
Ok, so am I actually _verifiably_ insane? Err...maybe. But these really were contenders and I'd say my final choice isn't too different. For Rust there's [AreWeWebYet?](http://www.arewewebyet.org/) tracking the viability of using Rust for web applications. For what I needed I could have probably used it, and Swift also seemed to have some fairly decent packages equipping it for server-side use. While I didn't chose Swift or Rust (despite glowing reviews about Rust from by buddy, [sfuller](https://samfullerstudios.com/), the idea of a natively-compiled strongly-typed backend language really intrigued me. That let me to my final and chosen option...

**Option 6: [Go](https://golang.org/) (Golang)**
I chose one -- took long enough! This is the language this site is actually served via. As mentioned above, I thought it would be interesting to use a strongly-typed language on the server, specifically one without a runtime à la Java or C#. Although this wasn't a technical requirement (because only my RESTful API requirement was), it certainly sounded fun.


## My Setup
Out of the box Go has good support for working with JSON, it has built-in HTTP Server (and client) packages, and even some SQL database support. But in a very differing philosophy from that of Django, I've replaced and added a number of the core components of my server. &nbsp;Here are the external packages I'm including:

  - [github.com/dgrijalva/jwt-go](http://github.com/dgrijalva/jwt-go) While researching the Node/Express stack I came across JWTs and had to know more. By the I had settled on Go as the language, I already knew I wanted to be using JWTs with whatever language I picked. The claims section in particular (when used correctly!) makes displaying &nbsp;relevant data easy in a client/server setup. Plus, outside of the web, JWTs are perfect for native, mobile, or desktop apps.
  - [github.com/gorilla/mux](http://github.com/gorilla/mux) Mux is a URL router, somewhat similar to Django's, but even nicer (and I like Django's). It's not feature-for-feature equivalent, but it's great.
  - [golang.org/x/crypto/bcrypt](http://golang.org/x/crypto/bcrypt) Go's `bcrypt` module does _exactly what you'd expect™️_ -- it hashes passwords (or, currently, the password).
  - [github.com/jinzhu/gorm](http://github.com/jinzhu/gorm) Gorm is a Go ORM (see what they did there?). At times Gorm leaves me really missing the power + elegance of Django's ORM, but for this site it really hasn't been a problem. Plus, if I were in a situation where I needed a more optimized SQL query for something, it cleanly steps out of the way and lets you do just that.

In the future I'd say I'm really likely to use this setup again. I haven't found any of the pieces of this stack to be nagging at me to replace them, and the ease of adding features has been great.
If you have any thoughts or questions, or if you find any errors, please let me know in the comments (~~coming soon!~~ EDIT: now up!). I'd be delighted to hear about your experience using any of the stacks I've listed, and as well as ones I've left out. What do you like about them, what would you change?


*I've been using Django Rest Framework for a few months on a different project. While it's pretty solid project, I find some very common tasks to take considerably more effort than I would like.
** No, I didn't. At least, not yet.