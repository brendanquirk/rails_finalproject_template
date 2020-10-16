# Ruby on Rails Contacts API Template

## Description

A single model full CRUD API using Ruby on Rails.

### Contacts Properties

|Property  | Type  | Default  |
|---|---|---|
| id | integer | assigned by db |
| name | string | n/a |
| age | integer | n/a |




## Install

<details><summary>rbenv</summary>
# Ruby - Environment

Your computer (Mac) already comes with a version of Ruby. Each one of you may or may not have the same version.

When you work on a project, all of your team members have to have the same version of Ruby.

Installing and uninstalling ruby every time you need to change which project you are working on would be a pain.

`rbenv` is a ruby environment manager. It can let you easily change between ruby versions.

## &#x26A0; Uninstall rvm


RVM is an alternative ruby environment manager.

If you have RVM already set up you will need to decide whether you want to continue using RVM or if you'd prefer to switch to `rbenv`. We won't be supporting RVM.

To check if you have RVM installed simply run the command `rvm`. If it is not installed you'll see the message `command not found: rvm`

To uninstall follow these instructions: [uninstall rvm](https://richonrails.com/articles/uninstalling-rvm)

RVM and RBENV do NOT work well together, so having both installed will cause _weirdness_ .

## Homebrew

1. See if brew is already installed (type `brew` and hit enter to see if it is). You should get a message about example usage, etc.

1. If you haven't install Homebrew, do so by going to http://brew.sh/
	- copy and paste this into the terminal `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"` and hit return


1. If brew is installed, run `brew upgrade` to upgrade to the latest version of homebrew
	* Might take a while, might upgrade stuff for postgres, node, heroku, etc.
1. Run `brew update` to update the list of installable programs by homebrew
	* Might say Already up-to-date

## Install rbenv

rbenv is a version manager for Ruby. We don't want to use our system Ruby (the one that does things with our operating system) because we don't want to inadvertently break our operating system. Instead, let's get an up to date version of Ruby that is safe to mess with.

1. Check if rbenv already installed: `rbenv`
1. If already exists, upgrade with `brew upgrade rbenv ruby-build`

Otherwise

1. `$ brew install rbenv ruby-build`
</details>

<details><summary>Ruby</summary>
## View Possible Ruby Versions
**See which versions of Ruby you can download**

1. `$ rbenv install --list`

There will be stuff like `rbx` and `jruby`, we are only interested in the ones that start with numbers.

## Install Latest Ruby
**Install the latest version of Ruby**

Get the version of Ruby before `-dev`

1. `$ rbenv install 2.6.3`

* There is no way within rbenv just to get the latest stable version
* You **must** install Ruby 2.2.2 or greater for Rails 5.
* Install might take a long time -- Terminal could just look like it's hanging

> ruby-build: use readline from homebrew
>
> Installed ruby-2.6.3 to /usr/local/var/rbenv/versions/2.6.3

## View Installed Versions of Ruby

1. Run `rbenv versions`

![](https://i.imgur.com/k4F34DP.png)

* system is your system Ruby
* asterisk is next to the version that you are using

## View Currently Running Version of Ruby

1. Run `rbenv version`

## Switch RBENV to a different Version of Ruby

1. `$ rbenv global 2.6.3`
	* Check with `rbenv versions`. Asterisk should be next to 2.6.3
1. `$ rbenv rehash` to tell computer we've switch versions of ruby
	* Confirm switch again with `rbenv versions` `* 2.6.3`


**CLOSE AND RESTART TERMINAL**

## Update Environment to use new Ruby

1. Run `ruby -v` and confirm ruby version _now in use by the system_ is `2.6.3p111` or somesuch

IF NOT

1. `$ echo 'eval "$(rbenv init -)"' >> ~/.bash_profile`
	* (replace `.bash_profile` with `.zshrc` if you're using zsh)
1. `$ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile`
	* (replace `.bash_profile` with `.zshrc` if you're using zsh)
1. Run `ruby -v` and confirm ruby version _now in use by the system_ is `2.6.3p301` or somesuch

## Install a gem

Gems are like NPM packages for Ruby, but they're installed globally, as opposed to multiple times for each application that you build

1. List gems with `gem list`
1. Run `gem install pry` to install a gem called pry.  It's a ruby REPL command
1. Run `rbenv rehash` to tell computer we've installed a new gem
1. List gems with `gem list` look for `pry`
1. Rub `pry` to start pry command
1. Inside pry type `2 + 2`
1. If that works, type quit

Note: Might need to update the gem manager with `gem update --system`

</details>

<details><summary>Rails</summary>
## Install Rails 5.2.3

1. Run `gem install rails` to install the rails commands
2. `rbenv rehash`
3. `rails -v`

Note: if Rails already installed, might need to run `bundle update rails`

## Test Rails
1. Run `rails new rails_project` to create a new app
1. `cd rails_project`
1. Run `rails s` to start the server
1. Go to `http://localhost:3000`
1. `rm -rf rails_project`, this was just a test and we won't go back to this.
</details>

<details><summary>Postgres With Rails</summary>
Open a new terminal tab:

```
psql -l
```

## Rails with Postgres

```
cd ../
rails new blog_project -d postgresql
```

This will error, so:

```
sudo gem install pg
```

if that doesn't work:

```
sudo env ARCHFLAGS="-arch x86_64" gem install pg
```

or install [postgress.app](https://postgresapp.com/) and

```
gem install pg -- --with-pg-config=/Applications/Postgres.app/Contents/Versions/latest/bin/pg_config
```

and possibly

```
gem install pg -- --with-pg-include='/Applications/Postgres.app/Contents/Versions/latest/include/'
```

finally:

```
rails new blog_project -d postgresql
cd blog_project
rails s
```

check: http://localhost:3000.  You should get an error:

```
^c
rails db:create
```

check: http://localhost:3000

```
rails generate scaffold Post name:string title:string content:text
rails db:migrate
rails s
```

go to http://localhost:3000/posts and create some posts

In `psql` tab

```
psql -l
```

You should see `blog_project_development` and `blog_project_test` databases available

```
psql blog_project_development
SELECT * FROM posts;
```
</details>

## Local Setup

### In Your Browser

1. Fork this repo to your account.

## In terminal

1. Clone YOUR forked version of the repo somewhere that is not a git repo already.
1. ```cd``` into the repo.
1. run ```bundle install``` to install any required ruby gems.
1. Create the psql database by running ```rails:dbcreate```
1. There will be a migration file you need to run by running ```rails db:migrate```
1. You may now run ```rails s``` to boot the app up at ```localhost:3000```
  - You should see something like this
  - ![](https://i.imgur.com/j7HJ7mG.png)
1. Insert a piece of data by doing ```rails c``` in a new terminal tab and once in the rails console do ```Person.create(name: "Tim", age: 30)```
1. Go to ```localhost:3000/people```
  - You should see this
  - ![](https://i.imgur.com/nvtY2Sy.png)


### Heroku Deployment

## Set a Root

Do this in your Rails api project directory (This example is from a "Noticeboard" API).

Make a controller with a method that you can use as the root of your project:

```bash
rails generate controller welcome
```

This will make `app/controllers/welcome_controller.rb`

![](https://i.imgur.com/obbUkh8.png)

If you don't set a root, Heroku will get confused. Let's make it so our app will root to the index method of the welcome controller:

In `config/routes.rb`

```
    root 'welcome#index'
```

![](https://i.imgur.com/bg7F7rz.png)

In the welcome controller file, let's just send some stuff from the index method:

```
  def index
    render json: { status: 200, message: "Noticeboard API" }
  end
```

![](https://i.imgur.com/14nBStv.png)


**Open your Rails API in the browser to check that the root works**

* Add, commit and push your welcome and root stuff to Github in preparation for pushing to Heroku

<br>

## Set up Heroku and Push

In the directory of your own desktop copy of the Rails noticeboard api, create and deploy a heroku app with the following commands:

* `heroku create <name_of_app>`

Example from a books app:

![](https://i.imgur.com/hf6oZlz.png)

* `git push heroku master`

If it works, you should be able to open your live API with

* `heroku open`

![](https://i.imgur.com/h83oezN.png)

## Production database

Set up your database:

* `heroku run rails db:migrate`

![](https://i.imgur.com/oxx83gd.png)

If you have seed data:

* `heroku run rails db:seed`

You can run rails on heroku commands with `heroku run <rails command>`

* `heroku run rails c`

![](https://i.imgur.com/0Coz9K6.png)

Note that this is your **production database**, you should not run any commands to drop or reset. `heroku run rails db:reset` will raise an error.
