railsFirstApp
=============

First rails app in git - based on http://ruby.railstutorial.org/

Running in http://railsfirstapproma.herokuapp.com/users

git and rails
$ git config --global user.name "Your Name"
$ git config --global user.email your.email@example.com

$ git config --global alias.co checkout   //just an alias called co from checkout.

git config --global core.editor "subl -w"  //a default editor

Inside the project
	git init
		git add .
	git commit -m “text
	git remote add origin https://github.com/romalopes/railsFirstApp.git
	git push -u origin master

	Branch
		$ git checkout -b New_Files
		$ git branch
		$ git branch -d New_Files  //to merge

Heroku and rails
	https://devcenter.heroku.com/articles/getting-started-with-ruby
	Heroku works with PostgresQL
		- add a the declarations in Gemfile to be like the following
			source 'https://rubygems.org'
			ruby '2.0.0'
			#ruby-gemset=railstutorial_rails_4_0

			gem 'rails', '4.0.0'

			group :development do
			  gem 'sqlite3', '1.3.8'
			end

			gem 'sass-rails', '4.0.1'
			gem 'uglifier', '2.1.1'
			gem 'coffee-rails', '4.0.1'
			gem 'jquery-rails', '3.0.4'
			gem 'turbolinks', '1.1.1'
			gem 'jbuilder', '1.0.2'

			group :doc do
			  gem 'sdoc', '0.3.20', require: false
			end

			group :production do
			  gem 'pg', '0.15.1'
			  gem 'rails_12factor', '0.0.2'
			end

$ bundle install --without production
$ bundle update
$ bundle install

The application:
rails new railsfirstapp

Model
	User: id:integer, name:string, email:string, password:string
	micropost: id:integer, content:string, user_id:integer
Creating Resources:
	Create a User scaffold.  Then, the attributes don’t need to be specified
	- $ rails generate scaffold User name:string email:string password:string
	- $ rails generate scaffold Micropost content:string user_id:integer
	What it do:
	Model(class User < ActiveRecord::Base)
		A variable @users is created in UsersController
		javascript
		html(of CRUD)
		json builder
		an empty helper
		test
		include -> resources :users and microposts in config/routes.rb
			resources :microposts
  			resources :users
		Controler(class UsersController < ApplicationController)
			as it is scaffold fill the file with many methods of REST/CRUD.
	
Validation
	class Micropost < ActiveRecord::Base
		belongs_to :user  # Database reference
	 	validates :content, length: { maximum: 140 }
	end
	class User < ActiveRecord::Base
		has_many :microposts  # Database reference
		validates :password, :presence => true,
	                       :confirmation => true,
	                       :length => {:within => 6..40},
	                       :on => :create
	  	validates :password, :confirmation => true,
	                       :length => {:within => 6..40},
	                       :allow_blank => true,
	                       :on => :update
	end



	$ bundle exec rake db:migrate OR JUST rake db:migrate

	$ rails s 

	$bundle exec rake -T db list of tasks related to db

MVC
http://ruby.railstutorial.org/images/figures/mvc_detailed.png
Problems of Scarffold:
	- No data validation
	- No authentication
	- No tests
	- No layout

Herroku
	$ heroku create
	$ git push heroku master
	$ heroku run rake db:migrate
	$ heroku open
	

The inheritances
	Model
		http://ruby.railstutorial.org/images/figures/demo_model_inheritance.png
	Controller
		http://ruby.railstutorial.org/images/figures/demo_controller_inheritance.png