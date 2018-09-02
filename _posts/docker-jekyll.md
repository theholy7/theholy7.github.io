# Using Docker to run Jekyll

When I first started this blog, I found it quite tricky to have Jekyll up and running properly.
I followed the guide in Github and the guide in jekyll's own website, but kept having problems.
These problems were related to dependencies, the gems ruby uses, and installing them wasn't an easy task.

When you solve a problem, or get something working, do you ever feel "dirty"? Like the solution you
found wasn't ideal, and your environment is polluted? Or that strange feeling you get, when something works but you don't exactly know why?

*I absolutely hate that feeling...* And I felt that way, until I found [Docker](https://docker.com).

The typical thing your read is that Docker lets you _containarize_ your applications.
And you are like: "Cool. What is that?". And someone than explains that you get everything
packaged and isolated from your system - kind of like a Virtual Machine, but not really a Virtual Machine. It is lighter than a VM, therefore easier to spin up and kill.

So then you wonder: "How can I use that do develop my applications?" - and if you are like me,
you'll try to get Vim and everything installed into a Docker image, and use it just like a VM. Wrong approach...

I finally understood how to use Docker for development while doing [Udemy's Docker Mastery course](https://www.udemy.com/docker-mastery/).

Basically, you want to have your Docker container running a Jekyll server (all its dependencies isolated from your system and working properly) and then you mount your projects folder into the running container.

So you keep editing your files in your machine (with all the cool plugins you've installed in vim over time), and Docker is just reading those files and serving them! So how do we do this?

After installing Docker - follow the docs, they are awesome - you run the following command:

```bash
export JEKYLL_VERSION=3.8
docker container run --rm \
	--volume="$PWD:/srv/jekyll" \
	--p 4000:4000 \
	-it jekyll/jekyll:$JEKYLL_VERSION \
	jekyll serve
```

Lets understand the flags used:
1. --rm -> Remove container when it exits
2. --volume -> mount my current working directory into that container's folder
3. -p -> map port 4000 from localhost to 4000 from container
4. --it -> run in interactive mode (keep STDIN) and allocate a pseudo-TTY
5. jekyll/jekyll:3.8 -> Jekyll repo, jekyll version 3.8 image
6. jekyll serve -> the command that is ran inside the container

Thanks to point 2. it is possible for me to run a server that reads in real time the files that I amediting locally (like this post).

And thanks to point 3. I can access _localhost:4000_ and see those changes in real time!

I finally have a way of running Jekyll in a clean way that makes me happy!

Hope that this makes sense to anyone that reads it, and that you understand how to use Docker to develop apps locally - not just distribute them to others when you finish.

Best,

J
