---
layout: post
title: My highlights from The Phoenix Project
excerpt_separator:  <!--more-->
categories:
  - Books
tags:
  - Learning
  - DevOps
  - Continuous Delivery
  - Continuous Integration
---
I am 6 years late to the party. The first edition of _The Phoenix Project_ came out in 2013, and I only got it now.
I don't remember the last time I picked up a book, and could *absolutely not* put it down until I was done with it.
If you haven't yet read _The Phoenix Project_, I highly recommend you get yourself a copy and start.
In my opinion this is a book that every struggling developeri, IT department, or business leader, should pick up.
I am very aware that I am not the first to say any of these things, but bear with me. I write my findings to make sure I don't forget them.

_The Phoenix Project_ explores the life of Bill Palmer after a sudden promotion from Director of Midrange Technology Operations to VP of IT Operations.
Coaxed by his CEO into accepting the position, Bill now has to save the company's failing project, whilst firefighting IT issues to keep the company moving.
Bill faces many issues during his first few days, but reacts accordingly. He sets up a team, tries to understand how he can better manage the reocurring issues,
and tries to reorganise work.

Things get worse before they get better, but with the help of Erik he finds his footing and comes out the other side victorious.
Erik has some lessons for Bill throughout the whole book, which I will try to list, and explore. Keep on reading. <!--more-->

## Interesting quotes and lessons learned

### Finding and solving problems
"The payroll run faiure is like a crime scene and we're Scotland Yard."

This is how I feel everyday. As a developer, finding bugs and solutions to them, feels like being a detective. I really connected with this quote.

### Find the best way to work
"How can we manage production if we don't know what the demand, priorities, status of work in process, and resource availability are?"
"How big is that list and how do things [tasks] get on it?"

The two questions posted above are really important. I know that a mistake that I usually make is that I think about tasks individually.
A good developer needs to do more than just code/architect good solutions. He needs to be reliable and understand how his time can be applied best.
What I mean is that the commitments we make every week should be defined regarding all other tasks our team is doing. Do we have time to help a colleague?
Do we have to help upskill a junior? Do we have to document our solutions?

It matters more that the whole team moves fast (even if you move slower), because you accomplish more things and bring more value. Be cautious, cause it is better to plan for the worst,
and you never know how much unplanned work might jump onto your lap...

### Visibility, knowledge sharing
"(...) I'm guessing Brent is even more behind than ever.
He complains that he had to spend a bunch of time training and heloping the new guys, and he is now stretched thinner than ever.
And he's still in the middle of everything."

I touched before on helping a junior, or documenting a solution. I kinda knew it was important when I started working, but I have a whole lot more appreciation for it after reading
_The Phoenix Project_. Brent is a great developer, but he is part of the issue. By building an infrastructure that only he knows how to operate, and fixing bugs without telling people how he did it
 he is grinding the company a halt.

The solution is simple. Make sure that your best developers are good because they do all their work (and are creative), but also share their knowledge with others. Understand, automate. If things are
standardized then there is less probability of them going wrong, _i.e._ everyone spins up VM's the same way, or everyone deployes the same way a.k.a. things become operations and remove guesswork.

### The four types of work

#### Business projects
Projects to directly deliver value to the customer.

#### Internal IT projects
Infrastructure and operations projects, internal improvements. Never stop getting better or making things easier/automated.

#### Changes
Fixed, changes, improvements. A little smaller than an internal project.

#### Unplanned work
Chaos, and incidents. Unplanned work stops you from doing planned work.

### The three ways
  * First Way: Work always flows in one direction – downstream.
  * Second Way: Create, shorten and amplify feedback loops.
  * Third Way: Continued experimentation, in order to learn from mistakes, and achieve mastery.

Repetition and practice are the prerequisites to mastery.

### Improvements not at the constraint are an illusion
"But of course, now everyone knows that you don't release work based on the availability of the first station.
Instead it should be based on the tempo of how quickly the bottleneck resource can consume the work."

### Dealing with people
"There's a chain of command: gripes go up, not down."

Best, Jose :)
