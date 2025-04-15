---
layout: post
title: Docker and DBT starter template
excerpt_separator:  <!--more-->
categories:
  - Random Code
tags:
  - Learning
  - Python
  - PostgreSQL
  - Docker
---

TL;DR: [Docker and DBT starter template](https://github.com/theholy7/docker-dbt-starter-template)

I am currently revising some data modeling concepts, and in the course I am doing they use [Pentaho](https://www.pentaho.com/).
However, the lecturer clearly states that Pentaho is just the tool, and the course is generic enough that you
can use any tool you want.

At Cable, we used [DBT (data build tool)](https://www.getdbt.com/) to build our data models and run them on BigQuery.
I became a big fan of DBT, and really wanted to use it during my course. So, to make my life easier, I created a starter template for Docker and DBT.

You can check out the GitHub repository [here](https://github.com/theholy7/docker-dbt-starter-template).
All files should be self-explanatory, but open an issue if you have any questions.

**Motivation**

1. I did not want to setup a Python environment - I have been using Poetry and it feels clunky to me
1. I already had Docker installed on my machine, so I thought that I could have a similar workflow to VSCode's devcontainers
1. I still wanted to use Zed as my editor - so I wanted to make sure that the changes in my host machine were reflected in the container
1. I also wanted to be able to generate and access the docs that DBT creates
1. And finally I knew I could just use docker-compose to run the dbt container and the Postgres container easily together

I hope this helps you get started with Docker and DBT.
