# CircleCI Documentation [![CircleCI Build Status](https://circleci.com/gh/circleci/circleci-docs.svg?style=shield)](https://circleci.com/gh/circleci/circleci-docs) [![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/circleci/circleci-docs/master/LICENSE) [![CircleCi Community](https://img.shields.io/badge/community-CircleCI%20Discuss-343434.svg)](https://discuss.circleci.com)

This is the public repository of <https://circleci.com/docs/>, a static website 
generated by [Jekyll](https://jekyllrb.com/). If you find any errors or have 
documentation requests, please feel free to contribute by following the instructions below. 
Otherwise, you can always open an 
[Issue](https://github.com/circleci/circleci-docs/issues) on this project.

## Work on CircleCI Docs Locally
There are two good ways to run a development server locally:

1. **[Use Vagrant](#vagrant-setup)**. The easiest way to get going is to use Vagrant. This gives you a clean 
environment with all the right versions of everything we need. 

2. [Use your existing Ruby environment](#bare-setup). If you already have a Ruby environment you like (e.g. you have rvm set up and feel comfortable using it) and you feel comfortable installing dependencies with bundler and such, you can run it directly on your machine.


### Vagrant Setup

#### Prerequisites
If you're going the Vagrant route, the following software needs to be installed:

- Git: system version should be fine
- Vagrant: [download directly](https://www.vagrantup.com/downloads.html), use apt-get (`sudo apt-get install vagrant`), or use brew (`brew cask install vagrant`).
- VirtualBox: [download directly](https://www.virtualbox.org/wiki/Downloads), use apt-get (`sudo apt-get install virtualbox`), or use brew (`brew cask install virtualbox`). Best to use version 5.0+. Another Vagrant provider (such as Docker) could be used instead, but VirtualBox is the default.

#### First Run
To get a local copy of <circleci.com/docs/> up and running, you can run the 
following commands. NOTE: The first time you run `./jctl start`, Vagrant will provision the entire VM for 
you based on what's in `bootstrap.sh`. It'll then run Jekyll for you. The whole process can take a few minutes, but it's a one-time deal.

```
git clone https://github.com/circleci/circleci-docs.git
cd circleci-docs
./jctl start
```

Once this is complete, Jekyll will automatically start in the VM. Vagrant starts forwarding port 4040 for you. You can 
simply view the docs at http://localhost:4040/docs/ .

####  Editing Docs

All of the docs can be found in the `jekyll/_docs` directory. You can make any 
changes that you need there, then run `./jctl rebuild` to have Jekyll rebuild 
the site. How to use [**jctl**](#jekyll-controller-jctl) can be found below.

As an alternative to using JCTL, you can log into the VM directly to interact 
with Jekyll. Run `vagrant ssh` to enter the VM directly. `cd /vagrant/jekyll` 
will take you to where the repository files are in the VM. From there you could 
run standard Jekyll commands such as `jekyll server` with whatever flags you 
would like.

### Bare Setup

#### Prerequisites
Going the bare route, the following software need to be installed:

- Git - system version should be fine
- Ruby - the version of Ruby currently being used with this project will be noted in the Gemfile. If you need to manage multiple Ruby versions, we recommend RVM though there are similar solutions you can use.
- [Jekyll](https://jekyllrb.com/) - Jekyll version 3.
- [HTMLProofer](https://github.com/gjtorikian/html-proofer) - HTMLProofer is used for testing links, images, and the HTML. The docs site needs to pass the build and test to be deployed. You can use HTMLProofer to test things before you send changes up to GitHub.

You're welcome to also use Bundler to install the Gems needed. If you are using RVM (or similar), just make sure they all play nice together.

#### First Run
To get a local copy of circleci.com/docs/ up and running you can run the 
following commands:

```
git clone https://github.com/circleci/circleci-docs.git
cd circleci-docs/jekyll
jekyll serve
```

Jekyll will build the site and start a web server. It can be viewed in your 
browser at [](http://localhost:4000/docs/). To stop Jekyll and regain controll 
of your terminal, just type `CTRL-C`.

####  Editing Docs

All of the docs can be found in the `jekyll/_docs` directory. You can make any 
changes that you need there, then re-run `jekyll serve` to have Jekyll rebuild 
and serve the site.

## Jekyll Controller (JTCL)

This is a Bash wrapper script to talk to Jekyll & Vagrant.

- start: Starts Jekyll. Is Vagrant isn't running, starts Vagrant as well.
- rebuild: Tells Jekyll to rebuild the site.
- stop: Shuts down the entire VM (vagrant halt), including Jekyll.
- restart: Restarts the Vagrant machine. Basically an alias of stop then start.

## Jekyll Commands

`jekyll build` - this tells Jekyll to generate the static files for the site, 
and place them in the `jekyll/_site` directory. It does not serve the files.

`jekyll serve` - this first runs `jekyll build`, then starts up an included 
mini webserver to serve the files from the `'jekyll_site` directory. Listens to 
localhost:4000 by default.

`jekyll serve --detach` - this serves the site as before, but runs in the 
background so that you can still use the same terminal window. Jekyll will tell 
you which process ID belongs to it before it goes so you can use that to kill 
it when you want to stop Jekyll. `kill -9 P_ID`. If you lose the ID, you can 
run `pkill -f jekyll` to stop all Jekyll instances.

## License Information

Documentation (guides, references, and associated images) is licensed as 
Creative Commons Attribution-NonCommercial-ShareAlike CC BY-NC-SA. The full 
license can be found 
[here](http://creativecommons.org/licenses/by-nc-sa/4.0/legalcode), and the 
human-readable summary [here](http://creativecommons.org/licenses/by-nc-sa/4.0/).

Everything in this repository not covered above is licensed under the 
[included MIT license](LICENSE).
