## Project Structure

The [first post](intro) established all my project objectives, so this post serves to give a bit more structure to the idea.

For this project, it is my personal preference to keep everything in the same repository, and well separate.

This is:

```bash
.
├── spiders_folder
├── data_science_folder 
└── any_other_folder

3 directories, 0 files

```

Luckily, I am going to use two frameworks that define what best practice is in each of them. I will be using [_Scrapy_](https://scrapy.org/) for the spidering,
and the [_Data Science Cookie Cutter_](https://drivendata.github.io/cookiecutter-data-science/) approach for the research I will do.

Both these tools provide a sort of _init_ method that creates the needed folders and files, and explains what they are used for.


```bash
.
├── fake_food_ds
└── fake_food_spider

2 directories, 0 files

```

Before any of this happens however, it is important to follow best practice when setting up your Python environment.

In my case, I followed the instructions to install [pyenv](https://github.com/pyenv/pyenv), [virtualenv](https://virtualenv.pypa.io/en/stable/),
and [virtualenv-wrapper](https://virtualenvwrapper.readthedocs.io/en/latest/).

The only thing you need to do is pay special attention to which python version you are using when installing all these things.
Errors pop up if you install `virtualenv-wrapper` and don't specify that it needs to use a python version different from your system's python.

With all this setup, it was easy to start the python environment I wanted to work in.
Just run the following commands:

```bash
$ mkdir fake-foods
$ cd fake-foods
$ pyenv install 3.6.2
$ pyenv local 3.6.2
$ mkvirtualenv fake-foods -a `pwd` -p `pyenv which python`
```

All this is pretty straightforward when you work with python. But in case you don't let me quickly explain what I did.

1. First I created a folder called fake-foods;
2. I moved into the created folder;
3. I used pyenv to install python, pyenv doesn't conflict with the system's python install;
4. I told pyenv that in that folder python 3.6.2 is to be used whenever the python command is used;
5. I created a virtual environment to install libraries that won't cause conflicts with the system's libraies;
  * _-a_ - This flag sets the current directory as the project folder, so if you use _workon fake-foods_ it will take you directly there
  * _-p_ - This flag tells the virtual environment to use the python version pyenv is using in that folder

When this is all done, you have your virtual environment ready, and you can start installing what you need.

```bash
(fake-foods) $ pip install scrapy
(fake-foods) $ scrapy startproject fake_food_spider . 
```

What happened here?
1. I installed scrapy in my virtual environment;
2. I started a scrapy project called fake_food_spider in the current folder

This initiates the files and folders needed for _scrapy_ so that we can start collecting data.


Best,
Jose 
