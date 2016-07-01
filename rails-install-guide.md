# The Ruby on Rails development environment

Ruby as well as Rails started out simple. Over the years however, the number of tools in use by the average Rails developer has grown steadily. 

Even though all of these tools serve a useful purpose, and together certainly make your life as a developer easier, it can be hard for people new to Rails to get everything up and running, and to understand how the different components interact.

This guide tries to help.

## The components

Ruby is a general purpose programming language. One of the nice things about Ruby is that it allows you to use multiple paradigms such as functional, object-oriented, and imperative programming.

Ruby on Rails, often referred to simply as “Rails”, is a web application framework written in Ruby. Rails is based on the Model-View-Controller architecture, comes with sensible defaults, and favors convention over configuration. This helps you get going quickly and can make it easier to understand and modify applications written by others.

RubyGems is a package manager for Ruby programs, frameworks, and libraries. An individual package is called a “Gem”. Gems are installed as part of your Ruby installation. Rails itself is distributed as a Gem.

Bundler is a tool that can install all the Gems a Rails application depends on by running a single command. This works by listing all dependencies in what’s called a “Gemfile” in the root directory of the Rails application.

Rbenv is a tool that allows you to set up and manage multiple separate Ruby installations. Rbenv makes it easy to use a different version of Ruby than the one that came pre-installed on your computer. It also allows you to use the exact same version of Ruby on your own computer during development as the one that’s running on your production server.

You can find more information and full documentation for each of these components on the web:

- Ruby: <http://ruby-doc.org>
- Rails: <http://rubyonrails.org/>
- RubyGems: <http://guides.rubygems.org>
- Bundler: <http://bundler.io>
- Rbenv: <https://github.com/rbenv/rbenv>


## Installation

This guide assumes you’re using a Mac running OS X 10.11 El Capitan. Most things should also work for earlier versions of OS X as well as on Linux. It also assumes you have a text editor (such as Atom, TextMate, or Sublime Text) and that you know how to run commands in the Terminal.

The purpose is not to provide the quickest way to get Rails running. Rather, this guide gives you the same setup as most developers who regularly work on Rails projects. It also helps you understand this setup and how to use and maintain it. Finally, this guide makes no permanent changes to your computer’s operating system installation by never requiring you to “sudo to root”.


### Homebrew

We’re going to use Homebrew to install Rbenv. Homebrew is a package manager that makes it easy to install open source command line tools on OS X.

First, make sure you have Xcode installed. You can get Xcode from the App Store.

Go to <http://brew.sh> and copy the installation command at the top of the page. Open the Terminal, paste the installation command, and run it.

You might get a message telling you that you haven’t yet agreed to the Xcode license. If that’s the case, open Xcode, agree to its license, and run the Homebrew installation command again.

### Use Homebrew to install Rbenv

Run the following commands in the Terminal to install Rbenv:

    $ brew update
    $ brew install rbenv ruby-build

Now open the configuration file of your shell in a text editor. This is `~/.bash_profile` assuming you’re using the default Bash shell on OS X. Add the following line at the bottom:

    eval "$(rbenv init -)"

Instead of `~/.bash_profile` on OS X, you’ll probably need to edit `~/.bashrc` if you’re on Linux, or `~/.zshrc` if you’re using Zsh.

Save your changes to the shell configuration file. Now close the Terminal, and re-open it to load the changed configuration. Run the following command:

    $ type rbenv

This should display “rbenv is a function” followed by some more output. If you only get something like “rbenv is /usr/local/bin/rbenv”, then you need to check your changes to the shell configuration file.

### A few more Homebrew commands

The following command updates Homebrew itself as well as the list of command line tools it can install for you:

    $ brew update

It’s a good idea to run this first when you’re about to install something with Homebrew.

You can upgrade all the tools you have installed with Homebrew to their latest versions using:

    $ brew upgrade

If you ever need a command line tool that’s not installed on OS X by default, then you can probably get it with Homebrew. Homebrew is also a nice way to install and use a more recent version of tools that come with OS X like Git or Subversion. 

For more information, see <http://git.io/vWHiz>

### Why not just use the Ruby that came with OS X?

The version of Ruby that Apple includes with OS X is a bit older than the current stable release. You can see this by running the following command in the Terminal:

    $ ruby -v 

Which should output something like:

    ruby 2.0.0p645 (2015-04-13 revision 50299) [universal.x86_64-darwin15]

Ruby 2.0.0 was released in early 2013 and is a few releases behind the current stable version of Ruby at the time of writing.

A more important argument against using the default Ruby installation that Apple has included on your Mac is that this requires you to install any additional Gems as the root user, and that doing so permanently changes the OS X system installation.

### Use Rbenv to install Ruby

Run the following command in the Terminal:

    $ rbenv install -l

This gives you a list of all the versions of Ruby that Rbenv can install for you. It’s a long list because it also includes alternative implementations of the Ruby language. Scroll up to see them all.

We’re now going to install the latest stable version of Ruby at the time of writing. Run the following command to do this:

    $ rbenv install 2.3.1

This compiles and installs version 2.3.1 of Ruby in your home directory at `~/.rbenv/versions/2.3.1/`

Now run:

    $ rbenv rehash

This makes sure all the command line tools provided by the version of Ruby you just installed can be found. 

You should always run `rbenv rehash` after you’ve installed a Gem that includes one or more command line tools. You can safely re-run this command at any time; it’s a good first step to do so when you’re trying to fix a problem.

### Set your global Ruby installation with Rbenv

You can get a list of all your Ruby installation with:

    $ rbenv versions

This should output something like:  

    * system (set by /Users/thijs/.rbenv/version)
      2.3.1

In this list, the version of Ruby that will be used when your run a Ruby command from the current directory is prefixed with an asterisk. This line also shows how this version was set.

Let’s change to the latest version of Ruby:

    $ rbenv global 2.3.1

Now Rbenv will give you this version of Ruby any time you run “ruby”, “irb”, “gem”, or any other Ruby command from the Terminal. If you run:

    $ ruby -v

It should now output something like:

    ruby 2.3.1p112 (2016-04-26 revision 54768) [x86_64-darwin15]

### Install Rails

Run the following command in the Terminal to install Rails:

    $ gem install rails

Now let’s make sure that Rails has been installed correctly:

    $ rails --version

You’ll probably get some kind of error message telling you that Rails is not currently installed. This happens because we haven’t run `rbenv rehash` yet. Let’s fix this:

    $ rbenv rehash

Let’s try again:

    $ rails --version

Now it should output something like:

    Rails Rails 4.2.6

To learn how to create a new Rails application, continue with the [Getting Started with Rails guide](http://guides.rubyonrails.org/getting_started.html).

### How to try Rails 5

The next major version of Rails will be released any day now. If you like, you can get the latest release candidate of Rails 5 with:

    $ gem install rails --prerelease

Keep in mind that almost all books and tutorials, including the official Rails Guides, currently still assume that you’ll be using Rails 4.2.6.

### Adding a Gem

If you’ve found a RubyGem you want to use in your Rails project, then you should list it in the `Gemfile` you can find in the root directory of your Rails project.

After you’ve added the declaration for the Gem you need, you should run the `bundle install` command to install this Gem and any of its dependencies.

Please make sure to remove any declarations for Gems you no longer use. This will prevent Rails from loading any libraries or frameworks you’re not using, and prevents others who run your application from installing stuff they don’t need.

### A note on making Gems install faster

By default, RubyGems generates documentation for every Gem it installs. Most developers never actually use this documentation, because they prefer to look up stuff on the web. This documentation can take some time to generate, especially if you’re installing a lot of gems at once using Bundler.

Disabling document generation can speed up Gem installation significantly. You can do this by adding a `~/.gemrc` file to your home directory that contains the following line:

    gem: --no-document

### Set a specific Ruby version with Rbenv

If you use features of the Ruby language that are only available in its more recent versions, or if you want to make sure everyone on your team uses the same version of Ruby, then it makes sense to set a local Ruby version specifically for your Rails application.

First make sure you’re in the root directory of your Rails application (you’ll probably need to enter a different path to your Rails project than the one listed below):

    $ cd ~/work/myapp/

Now you can set the Ruby version for the Rails application in this directory to `2.3.1` by running the following command in the Terminal:

    $ rbenv local 2.3.1

This creates a hidden `.ruby-version` file in the current directory containing the version of Ruby that Rbenv will use when you run a Ruby command from this directory, or any of its subdirectories.

If you now run:

    $ rbenv versions

You should get something like:

      system
    * 2.3.1 (set by /Users/thijs/work/myapp/.ruby-version)

When you try to run a Ruby command from a directory with a local Ruby version set that you don’t currently have installed, Rbenv will show you an error message such as:

    rbenv: version `2.3.0' is not installed

In that case, run `rbenv install` followed by the missing Ruby version number to install it.

### Getting an existing Rails application to run

Ideally, every Ruby on Rails project should include installation instructions in a README file in its root directory. 

However, most Rails applications only require the following steps to get them running:

First, install the required Gems:

    $ bundle install

Then create and initialize its database:

    $ rake db:setup

Now run the Rails application in development with:

    $ rails server

Things can get a bit more complication when a Rails application requires the PostreSQL or MySQL database server.

### Installing PostgreSQL with Homebrew

Some Rails applications require the PostgreSQL database server. Install it with:

    $ brew install postgresql

After you’ve installed PostgreSQL, you might have to run `gem install pg` or `bundle install` before your Rails application can connect to it.

You can start the PostgreSQL database server with:

    $ postgres -D /usr/local/var/postgres

### Installing MySQL with Homebrew

Some Rails applications require the MySQL database server. Install it with:

    $ brew install mysql

After this, you can start the MySQL database server with:

    $ mysql.server start

### The purpose of Gemfile.lock and when to delete it

When Bundler first installs the Gems listed in a `Gemfile`, it records the exact version of these Gems as well as all of their dependencies in a separate file named `Gemfile.lock`. When you run `bundle install` again, it will install the versions listed in `Gemfile.lock`, instead of trying to get the most recent version that matches the rules in the `Gemfile`.

The purpose of this “lockfile” is to make sure that all the developers on your team are using the exact same version of each Gem, and that the versions that get installed on your production server are the same as what you’ve been using during development.

There’s no reason to ever edit `Gemfile.lock` by hand. When you delete `Gemfile.lock`, it gets regenerated based on the most recent versions available for each Gem at that time. Normally, you don’t need to do this, but you might run into a situation where doing so can fix issues where `bundle install` failed because outdated Gems are no longer available, or because a Gem you added requires a newer version of a dependency.