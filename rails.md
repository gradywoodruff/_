wip

# Rails

For a faulty schema.rb file

	db:migrate:reset


Other

	brew upgrade ruby-build
	rbenv install -l

	# Install the newest
	rbenv install 2.4.1
	rbenv global 2.4.1
	gem install rake rails bundler foreman mailcatcher  




	rails new project_title -d postgresql --skip-test-unit --skip-turbolinks




	rm -rf test




	# You should specify the ruby version
	ruby "2.4.1"

	source 'https://rubygems.org'

	git_source(:github) do |repo_name|
	  repo_name = "#{repo_name}/#{repo_name}" unless repo_name.include?("/")
	  "https://github.com/#{repo_name}.git"
	end


	# Bundle edge Rails instead: gem 'rails', github: 'rails/rails'
	gem 'rails', '~> 5.1.0'
	# Use postgresql as the database for Active Record
	gem 'pg', '~> 0.18'
	# Use Puma as the app server
	gem 'puma', '~> 3.7'
	# Use SCSS for stylesheets
	gem 'sass-rails', '~> 5.0'
	# Use Uglifier as compressor for JavaScript assets
	gem 'uglifier', '>= 1.3.0'
	# See https://github.com/rails/execjs#readme for more supported runtimes
	# gem 'therubyracer', platforms: :ruby

	# JSON
	gem 'active_model_serializers'

	# Processes
	gem 'foreman'
	gem 'sidekiq'

	# Heroku suggests the rails_12factor gem, but this should only
	# be used in production
	group :production do
	  gem 'rails_12factor'
	end

	# Kits
	gem 'authkit', git: 'https://github.com/jeffrafter/authkit'
	gem 'errorkit', git: 'https://github.com/jeffrafter/errorkit'
	gem 'notifykit', git: 'https://github.com/jeffrafter/notifykit'
	gem 'uikit', git: 'https://github.com/jeffrafter/uikit'

	# These are a couple of my favs, if I forget them I regret it
	gem 'strapless'
	gem 'awesome_print'

	# For tokens
	gem 'hashids'

	group :development, :test do
	  # Keeping the database fields in the models and specs makes things easier
	  gem 'annotate'
	  # Call 'byebug' anywhere in the code to stop execution and get a debugger console
	  gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
	  # Get specs involved in this process
	  gem 'rspec-rails', '>= 3.5.0'
	  gem 'shoulda-matchers', require: false
	  gem 'factory_girl_rails'
	end

	group :development do
	  # Access an IRB console on exception pages or by using <%= console %> anywhere in the code.
	  gem 'web-console', '>= 3.3.0'
	  gem 'listen', '>= 3.0.5', '< 3.2'
	  # Spring speeds up development by keeping your application running in the background. Read more: https://github.com/rails/spring
	  gem 'spring'
	  gem 'spring-watcher-listen', '~> 2.0.0'
	end

	group :test do
	  # Make our specs watchable with beautiful progress bar
	  gem 'guard-rspec', require: false
	  # Better formatting of rspec
	  gem 'fuubar'
	end




	bundle




	*.rbc
	*.sassc
	.sass-cache
	capybara-*.html
	.rspec
	/.bundle
	/vendor/bundle
	/coverage/
	/spec/tmp/*
	/public/assets

	# Ignore logs and temp files
	/log/*
	/tmp/*
	!/log/.keep
	!/tmp/.keep

	# Ignore Byebug command history file.
	.byebug_history

	# Ignore databases
	/db/*.sqlite3
	/db/*.sqlite3-journal

	# Ignore uploads
	/public/system/*

	# Ignore other junk that some crops up
	**.orig
	rerun.txt
	pickle-email-*.html

	# Ignore temp stuff
	designs
	samples
	TODO.md
	spec/examples.txt

	# Vagrant
	.vagrant

	# Ignore config (optional)
	config/application.yml

	# You may want to ignore .env if you are using DotEnv
	# If you do ignore, you should have a .env.example
	.env

	# In modern Rails you do not ignore database.yml
	# or secrets.yml by default. But if you store secrets in them
	# you must not check them in to the repository
	# config/database.yml
	# config/secrets.yml





	heroku login
	heroku create
	git push heroku master
	heroku rename project_title




	heroku run rake db:migrate