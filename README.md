
# Git

## Get set up

There are a bunch of options for git hosts - this "app" is on GitHub, so let's start there. You'll learn as you go, really hands-on. The first thing to know: `git` is a wildly popular distributed version control system.

1. Make a [GitHub](http://github.com) account
2. Download and install [git](https://git-scm.com/downloads)
3. Configure your username and email
```
git config --global user.name "<your_user_name>"
git config --global user.email "<your_email>"
```
4. Set up ssh (for authentication with GitHub)
	1.  Check for existing keys at `~/.ssh/id_rsa` and `~/.ssh/id_rsa.pub`
	2. Assuming you don't have those, generate a new pair: `ssh-keygen -t rsa -C "your_email@example.com"`
	3. Copy the public key to your clipboard: `pbcopy < ~/.ssh/id_rsa.pub`
	4. Add it to your GitHub account
		1. In GitHub, open the top right menu, and select "Settings"
		2. Go to "SSH and GPG keys"
		3. "New SSH key"
		4. Name your key (recommendation: what you call your computer)
		5. Paste in the public key under "Key"
		6. "Add SSH key"
	5. Test with `ssh -T git@github.com` (you should see a message like "You've authenticated, but Github does not provide shell access."

## Learn the basics

### Cloning

Cloning a repository (repo) makes a local copy of a repo from a remote source.  This can be done over HTTPS or SSH, but since we just set up keys (because GitHub requires it) we'll use SSH.  That command looks like:
```
git clone git@github.com:JMRosenberg/git-docker-demo.git
```
Using HTTPS would look more like:
```
git clone https://github.com/JMRosenberg/git-docker-demo.git
```
Either way, you're pointing to the host (github.com) and then specifying the repo (JMRosenberg/git-docker-demo.git).

By default, this will create a folder in your current working directory, and name it after the repo (e.g. `git-docker-demo`).  If you want the files someplace else, just add a path onto the command (e.g. `git clone git@github.com:JMRosenberg/git-docker-demo.git ./folder-with-different-name`)

### Getting around

Try the following, see what they do!  Add `--help` after any of these to get the `man` page with additional information.

* `git status`
* `git log`
	* try adding `--graph`
* `git branch`
* `git diff`

### Making your first change

Before actually making a change, a quick diversion...

Pretty much every project of notable size (and lots of small ones too!) use branches as part of their workflow.  In short, branches are a way to split off sets of changes, so they can get developed independently without blocking other workstreams.  There are other benefits, but I'll probably just link to sources on them, because they mostly come into play at scale.

Mostly for the sake of learning, we're going to use branches!  I'm going with something similar to ["GitHub flow"](https://guides.github.com/introduction/flow/), because it's easy, and it gets the job done.  It's also what I use at my day job, and haven't found myself needing anything more complicated.

The default branch has historically been called `master`, which has some, uh, baggage.  Many projects are changing to something like `main` instead, although you can use absolutely anything you want!  This project still uses `master`, because I haven't changed it from the default (yet).

Before fully diving in, the rough plan:
* Make a new branch
* Switch to that branch
* Make a change
* Stage, commit, and push your code (more details later!)
* Open a Merge Request
* Merge it

By the end of this, you will have your own changes on the `master` branch of the repo, where whoever comes along next can build on it.

#### Create a new branch

1. Check which branch you're on with `git branch` - it should highlight `master`
2. Create a new branch with `git branch <unique-descriptive-name>`
3. You're still on `master` (confirm with `git branch` again), so switch to your new branch with `git checkout <unique-descriptive-name>`
4. Confirm you're on the new branch with one last `git branch`

**Pro tip:** Adding the `-b` flag to `git checkout` will create a new branch and switch to it all in one!  `git checkout -b <new-branch-name>`

#### Make a change

At the bottom of this file is a "Contributors" section.  Add your name to the list - you've earned it!

#### Commit your change

This change was small, so you're pretty confident it's correct.  But if you really want to make sure, `git status` will tell you there's a changed file.  It would also tell you if there were new/deleted/moved files.

`git diff` was empty before, but now will show you your change!  Make sure it looks good before continuing.

Now you can stage your changes with:
```
git add .
```
Note the `.` at the end - that adds _all changes_ from your working directory (recursively!).  You can be more selective if you want, specifying a file or folder to `add`.  Executing `git add` multiple times will stage the changes from all of the files you give it.  You can also see that the color of that file has changed when you run `git status`.  To remove a file that you accidentally added (without reverting your changes) you can use `git reset <file>`.

And to lock in your change with a `commit`:
```
git commit -m '<descriptive message about your changes>'
```

Lots of places have standards around commit messages (we always do `<ticket number>: <descriptive message>`).  Take advantage of the low-effort documentation!

If you don't like your message, `git commit --amend` will let you change it, but you can play with that later.

Even before you've pushed your changes to GitHub, commits are really useful locally.  They'll let you easily go back in time to meaningful checkpoints, so you can attack even the most aggressive refactorings without fear of permanently losing something.  A good rule of thumb is to commit every time you get back to a working build - that means you have frequent checkpoints, and that no matter which commit you go back to (or try to deploy) it will at least _kinda_ work.

#### Contribute your change

Now you need to get your code back to GitHub, where your team can review it, approve it, run automation, and, eventually, merge it back in to `master`.  And even if it's not quite ready for review, pushing your branch will let others see it and pull it, which means they can help out or take over your partially completed work.

Pushing to GitHub is really easy, just:
```
git push origin <branch-name>
```

In this case `origin` just says "the place I originally cloned from".  But git is distributed, not centralized, so you can replace that with a different `remote` if you want!  If you want to permanently change your `origin`, use `git remote set-url origin <new-url>`.

Now you'll be able to see your branch in the GitHub UI, and open a Pull Request.  Do that, get feedback, update your code (change, `add`, `commit`, `push`, and it will automatically update your PR), and when your automation passes and the change is approved, merge it in!

At this point, `master` has your changes incorporated, so you can switch back to `master` locally (`git checkout master`) and pull the latest changes (`git pull`).  With current practices, a merge to `master` will usually kick off more automated testing, and often a deployment to a non-production environment.  But different companies/projects have different standards, so ask before merging!

It's also possible to merge locally instead of through GitHub, and there are tons of different flavors (e.g. fast-forward, or merge commit?) and different things that can "fail" (e.g. the dreaded merge conflict).

### More topics

I don't have time to write a thorough tutorial on all of these right now, but things to look into:
* Reverting changes
* Rebasing
* Resolving merge conflicts

# Docker

I don't have time to write a thorough tutorial for this either, so we'll do it live!  Write up instructions as you go through, and commit them here for future reference.

The really really short story on Docker:

Docker is virtualization, but instead of sharing a hypervisor and running a VM (with its own operating system and everything) Docker shares the linux kernel.  That means you can focus on just the application, and keeps images (and containers) super lightweight.  It has a big ecosystem of base images, so you don't need to deal with installing your framework yourself, and sophisticated layering that enables further sharing.

For example, at work we pull the dotnet core 3.1 image from Microsoft, create a new "base" image that has dependencies like New Relic installed, and then layer each application on top of _that_ in their own images.  That means updating a common dependency only happens a single time, and _all of our services_ get it _automatically_.  That's a huge time-saver.

The plan is to grab a super simple node app, make a Dockerfile, and run a container locally.  That's a bit contrived, but it means whoever wants to run your app can do it without installing node, much less the same version of node.

# Contributors
* Jake Rosenberg