---
layout: post
title: "Gitignore"
date: 2024-04-02 10:46:00 +0100
author: "Giulio Umbrella"
categories : git
---

In a repository not all files are part of the code base. For example, each directory in Mac contains a .DS_Store file, not relevant for the project. For a mac user, this is very tedious. Every time we check the git status, the .DS_Store appears listed. 

In this post, we'll see 3 different ways to make git **ignore** a file pattern

- .gitignore file
- global .gitignore file
- exclude file

Each solution serves a specific purpose, let's dive in and explore all of them.

## .gitignore

> Use local .gitignore file for project based exclusions.

In each repository we can add a `.gitignore` file to specify patterns of files and directories we do not want to version. Note that the .gitignore file is part of the code base and will pushed on the remote repository.

For a Mac/Linux user we can open a terminal in the repo directory and type the following: 

{% highlight bash %}
cd repo                       # move inside repository directory 
touch .gitignore              # create file
echo .DS_Store > .gitignore   # add string to file
{% endhighlight %}

The .DS_Store is now excluded from versioning, super-duper.

Now, shall we update the .gitignore for every project we create? And what about the remote repository? Why add configuration specific for our system? Why bother other users with not relevant lines of code?

Luckily, git offers a global solution which applies to **all** local repositories.

## .global gitignore

> Use global .gitignore for system specific files.

We can *define* a global .gitignore file and set exclude files once and for all. Each repository inherits such configuration and enforce it. Let's see how to do it

{% highlight bash %}
cd ~                                               # Move to home
touch .gitignore                                   # Create file
echo ".DS_Store" > .gitignore                      # Add settings
git config --global core.excludesfile ~/.gitignore # Set global option
{% endhighlight %}

In this example we follow in our previous solution, but first we place ourself in the **home** directory. Why the home? Well, it's not strictly necessarily, we can provide any kind of path. But it is a good practice to place all user configuration files in the home directory with the `.name` format to avoid accidental modifications.

Next we use git configuration commands `git config` to alter git behavior with the `--global` flag to enforce the setting in every repository. The last part of the command sets a global gitignore file.  

How can check our setting? Use the `git config -l` to print all the configuration details. It should list the .gitignore file.

Now all .DS_Store files will be ignored without the need to create a .gitignore file!

## Exclude

> Use exclude to suit specific local directory needs.

The .DS_Store nicely fits for a global configuration files. But how about specific files that we want to exclude? For example, we can decide to keep some private files for personal experiments in the repository. Once again, we do not want to alter the remote .gitignore as the configuration is specific for our local repository.

We can add the files to the global gitignore but it is not a good idea, as it is shared by every repository. It is a poor practice to enforce repository-specific settings into every repository.

In other words, we are looking for a **local** gitignore file which is **not** shared on the remote repository. Luckily, git comes with a nice feature for doing so. Inside the local repository, we can add in the `.git/info/exclude` file all the paths we want to exclude. The exclude file is local and will not be shared with others.

Let's give a practical example. Assume we have some executable files and we want to analyze and we create some scripts to do so. 

{:refdef: style="text-align: center;"}
![Repository](/assets/images/2024-04-02-gitignore/basic_structure.png)
{: refdef}

From a logical point of view, it makes sense to keep the executable and the related analysis scripts together. It is also wise to version the scripts to keep track of your work. However, the executables are immutable so there's no point in adding them to the repository. 

If we check the status, we can see that all the files are listed:

{:refdef: style="text-align: center;"}
![Before exclude](/index/assets/images/2024-04-02-gitignore/before_exclude.png)
{: refdef}

We can use the the exclude file to match all the file I want to **exclude**. The file is inside the local repository configuration directory:

{% highlight bash %}
cd repo                     # move inside repository directory
cd .git/info                # move in the configuration dir
echo mal_exec >> exclude    # add file name to exclude file
{% endhighlight %}

Check again the git status:

{:refdef: style="text-align: center;"}
![After exclude](/index/assets/images/2024-04-02-gitignore/after_exclude.png)
{: refdef}

Git is now ignoring the executable. 


## Conclusion

In this post we explored three different options to exclude file from versioning and when to use them:

1. Use local .gitignore for project based exclusions
2. Use global .gitignore for system specific files
3. Use exclude to suit specific directory needs

## Reference

- https://git-scm.com/docs/gitignore
- https://gist.github.com/subfuzion/db7f57fff2fb6998a16c