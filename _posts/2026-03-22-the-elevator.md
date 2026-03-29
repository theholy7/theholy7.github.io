---
layout: post
title: "The man and the elevator"
excerpt_separator:  <!--more-->
categories:
  - Life
tags:
  - Learning
  - Work
  - AI
---

_This is a post about "vibe coding"/"agentic engineering", and my mental journey
to come to terms with it._

Lately, I have had this image in my head of people that were face to
face with elevators for the first time. What was it like to be in that moment?
What were the feelings going through their heads? Excitement? Discomfort?

I wonder what I'd do if I were living in that period. Would I be taking the stairs
because that is what I am used to doing? Would I be jumping onto any elevator
because of how new that technology was?

I've been asking myself those questions, mostly about AI, LLMs, and their effect
on my work, my teams' work, and the company I am at. I'm not sure if I should be
worried, excited, or somewhere in between. And the truth is that the hype/doomsday
articles I read all over the web don't help.

It's been a journey to get into a different mental state, that allows me to use
it more, and do it more comfortably. So I want to share what that journey has
been like for me.<!--more-->

My biggest struggle was - to put it plainly - to feel ownership over the work
produced by the LLM, and feel like I can trust it. And the second struggle was
to not feel outdated and irrelevant. I want to touch on those two subjects for
those that are going through a similar challenge.

To really expose the inner gritty details of me questioning all of this, here
is a genuine prompt I wrote on Feb 19th.

```text
How can I improve my work flow with Claude?

At the moment I am lacking the confidence to delegate more and more work
and I still rely on validating things myself.

What is a good workflow that I can use to train myself to write better
prompts and context, and worry less about failures?

How can I then take responsibility for the code I did not write?

Claude is changing the paradigms of software development, and I am
struggling to adapt to those changes, at least mentally. I do code
with it, and debate ideas, but some colleagues seem to do everything
with claude.
```

What I am writing in this post is not the output of that prompt,
it's the output of talking with my developer friends and how they interact
with AI/LLMs day-to-day. And what I found is that probably the
average developer isn't as black or white, hype or doomsday, as all the people
that post online. We are all in different parts of our journey, but face
similar issues and questions.


## The mindset shift

First and foremost, don't let yourself be influenced when it seems like others
do everything with Claude and you're not. That's a matter of perception, hard to
define, hard to measure. They might spend all their day on Claude fighting a
single good quality prompt, they might spend all day writing bad prompts. Who
knows. What matters is that you have to build your own workflow, and be comfortable
with it.

In practice this means you have to start using AI. Think of that project you
haven't touched in years but would like to continue developing. Can you use AI
to help you get further?

This is a very low stakes way of getting started. You don't need to pay
anything. You can start with the limited free tiers of Codex or Gemini, or the
Claude Code Pro 30 day free trial. Is there a feature you want to develop, or
some tech debt you want to remove? Do it. Prompt it, look at the output,
evaluate it. And when the trial is over or the daily quota runs out, take
some time to be with your thoughts and understand what went right and wrong.
Then try again the next day. This will help you build your intuition about which
tasks you can do well with AI agents, and which ones you need to improve on.

Once you start to get the feel for your flow, you can bake it into your work.
And when you do so, you might ask yourself: how is it that I can trust this
output? How do I review it in detail? How can I be sure that *this* code is
fine?

This is the *core* of the mindset shift.

As engineers, we constantly trust other people's code. We have review processes
for that, we have tests for that. AI-code isn't any different - it's just like
having a tireless collaborator next to you. You guide it, and you review the
code, trusting both your engineering sense, and engineering best practices you
follow. You are the editor, not the author.

This is meaningfully different from delegating to a person. A human colleague
will push back if your requirements are unclear, ask clarifying questions, flag
when something feels wrong. There is a shared stake in the outcome. With AI
tools, none of that exists — they will confidently produce something wrong
without hesitation, filling gaps with plausible-sounding guesses. The
responsibility doesn't actually distribute. It stays entirely with you, just
disguised as delegation.

This means that delegating to AI requires *more* upfront clarity than
delegating to a person, not less. A good human collaborator compensates for a
vague brief. AI launders it into confident-looking output. The better mental
model isn't "I delegated this" — it's that you used a sophisticated tool, and
the full weight of ownership never left you.

Which brings us back to context. The AI only knows what you tell it - so it is
paramount to give it the right context. All your thinking is done ahead of the
prompt, otherwise it will make assumptions that sound correct but are wrong.
Don't think you are getting dumber, that you are offloading your thinking. You
are not thinking less. You are thinking first, and then letting the execution
happen.

Thankfully, when you do get it wrong, you can just *discard the code,
and start over*. The cost of code has lowered, so you can use what you learned
from the attempt, add context to the prompt, and try again. This is the new
paradigm of coding we need to adapt to.

So, to summarize:
* Try it in a low stakes environment, learn your flow, know your limitations
* Practice until you are comfortable, and bring it gently into work
* Review code as you normally do. Be critical, apply engineering best
  practices. Small PRs, tests written and passing. When it's not good enough you
  start over.
* Before prompting, write a short spec — even a paragraph. What should this do?
  What are the edge cases? What should it *not* do? Then review the output
  against your spec rather than reading it cold. You'll find review much easier
  because you have a framework, and over time this is how you build intuition
  for what context these tools need upfront. When it's wrong, start over with
  more context

## Fear of getting outdated

Do we all have this fear? I do. I have constantly oriented my career towards not
being outdated. I try to learn something new every day because of that fear. And
I wanted to work in data because of it. AI algorithms need data piped to them, I
used to say, so I'll always have a job.

As you can imagine, seeing a tool code so fast and so well, threw me off a lot.
I was thinking as an author, and not as an editor. With time to reflect on
these changes, I noted that my current success has never been because I was the
best or fastest coder. I have done well so far because I care about my
colleagues, my team, the business I am in, and the products we build. I think
there will always be space in the industry for those people. People who try to
reduce uncertainty, that want to deliver good quality products, people that
can own a roadmap and deliver end to end. These tools have come to give us even
more breadth of work.

We can now take a microservice that we are not very familiar with and understand
it faster. We can make a small PR to help another colleague, rather than just
adding to their plate. We can build proof of concepts quickly to improve
processes that are broken.

We, people that want to reach beyond our current role and have impact
everywhere, are useful to *any* business. We should feel empowered by these tools,
not replaceable.

If you have this fear, I encourage you to reflect on your career, and try to do
more of what has brought you your success. To break the boundaries that exist,
and to try to reach further. I am sure you will find your space, augmented by
what these tools provide.

## Closing notes

With this post, I don't want to be a hypeman for AI, nor a doomsday person. I
want to truly share what my journey was like, and how I think about my role now
with these tools out there.

As mentioned, a lot of my current thinking was shaped by great conversations I
had with my friends. I encourage you to do the same. Their opinions will inform
your own, and yours will inform them.

I hope your journey goes smoothly, but if it has bumps, don't worry, all good
journeys have ups and downs. Don't hesitate to reach out if my post resonates
with you, or you want to debate any of its ideas.

That's all for now!
