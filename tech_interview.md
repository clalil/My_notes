```rb
rails -v
$ rails _5.2.3_ new rails_demo --database=postgresql --skip-test --skip-bundle
**no bundle yet**
$ cd rails_demo

group :development, :test do
  gem 'rspec-rails'
  gem 'shoulda-matchers'
  gem 'factory_bot_rails'
end
#shoulda: test validations and associations w less code
#factory bot is essentially a fixture replacement

$ bundle install

#Run the RSpec generator to add the testing framework to your rails application
$ bundle exec rails generate rspec:install

# Why bundle exe ? That means it uses the gems specified in your Gemfile.

#spec/rails_helper.rb
Shoulda::Matchers.configure do |config|
  config.integrate do |with|
    with.test_framework :rspec
    with.library :rails 
  end
end

#avoid the generators to scaffold too many files:
#config/application.rb

class Application < Rails::Application
  # Disable generation of helpers, javascripts, CSS, and view, helper, routing and controller specs
  config.generators do |generate|
    generate.helper false
    generate.assets false
    generate.view_specs false
    generate.helper_specs false
    generate.routing_specs false
    generate.controller_specs false
  end
  # ...
end

#Open .rspec file
--format documentation

#run the command
$ bundle exec rspec

#Add cucumber-rails and database_cleaner gems to the test group of the Gemfile.
group :development, :test do
  [...]
  gem 'cucumber-rails', require: false
  gem 'database_cleaner'
end

#The database_cleaner gem is used to ensure a clean database state for testing
# This will generate Cucumber configuration files and set up the database for Cucumber tests.
$ bundle exec rails generate cucumber:install

#As a last step, you will need to create the database and run the migrate command (even if we have not created any tables and columns yet)
$ rails db:create --all
$ rails db:migrate

#Sanity check for cucumber
$ bundle exec cucumber

# Coveralls: Add the following gem to your Gemfile in the :development and :test group
group :development, :test do
  gem 'coveralls', require: false
end
#Bundle install!!!

#Next, we need to add coveralls to our testing suite. Add to top of file:
# spec/rails_helper.rb for RSpec
# features/support/env.rb for cucumber

require 'coveralls'
Coveralls.wear!('rails')

#We need to prevent coveralls from sending data right after running each test. Instead, we want to wait until coverage has been merged before we send it off.
#instead of 
Coveralls.wear!('rails')
#use
Change with Coveralls.wear_merged!('rails')

#Then create a custom rake task that will run all your test suites then submit coverage results to the coveralls website.

# Create a new file lib/tasks/ci.rake
unless Rails.env.production?
  require 'rspec/core/rake_task'
  require 'cucumber/rake/task'
  require 'coveralls/rake/task'

  Coveralls::RakeTask.new

  namespace :ci do
    desc 'Run all tests and generate a merged coverage report'
    task tests: [:spec, :cucumber, 'coveralls:push']
  end
end

#Now you can run:
$ bundle exec rails ci:tests

#API INSTEAD
$ rails _5.2.0_ new cooper_api --api --database=postgresql --skip-test --skip-bundle
#Make ApplicationController inherit from ActionController::API instead of ActionController::Base.

#Update gemfile
source 'https://rubygems.org'
git_source(:github) do |repo_name|
  repo_name = "#{repo_name}/#{repo_name}" unless repo_name.include?("/")
  "https://github.com/#{repo_name}.git"
end

ruby '2.4.1'

gem 'bootsnap', '>= 1.2', require: false
gem 'rails', '~> 5.2.0'
gem 'pg', '>= 0.18', '< 2.0'
gem 'puma', '~> 3.7'
gem 'jbuilder', '~> 2.5'

group :development, :test do
 gem 'pry-rails'
 gem 'pry-byebug'
end

group :development do
 gem 'listen', '~> 3.0.5'
 gem 'spring'
 gem 'spring-watcher-listen', '~> 2.0.0'
end

# We also want to add the rack-cors gem to allow external clients to access our application.
# Gemfile
# Use Rack CORS for handling Cross-Origin Resource Sharing (CORS),
# making cross-origin AJAX possible 
gem 'rack-cors', require: 'rack/cors'

# Add config/application.rb allow GET, POST, PUT and DELETE requests from any origin on any resource. This setting will also expose the appropriate headers and include them in the response, making it possible to authenticate users

# config/application.rb
module CooperApi
  class Application < Rails::Application
    # [...] other code...
    config.middleware.insert_before 0, Rack::Cors do
      allow do
        origins '*'
        resource '*', 
          headers: :any, 
          methods: %i[get post put delete],
          expose: %w(access-token expiry token-type uid client),
          max_age: 0
      end
    end
  end
end

# Update your Gemfile with the following gems,
group :development, :test do
  gem 'rspec-rails'
  gem 'shoulda-matchers'
  gem 'factory_bot_rails'
  # [...]
end

#Run rails generate rspec:install to install rspec for your rails project.
# spec/rails_helper.rb
ENV['RAILS_ENV'] ||= 'test'
require File.expand_path('../../config/environment', __FILE__)

abort('The Rails environment is running in production mode!') if Rails.env.production?
require 'spec_helper'
require 'rspec/rails'

ActiveRecord::Migration.maintain_test_schema!

Dir[Rails.root.join('spec/support/**/*.rb')].each { |f| require f }

RSpec.configure do |config|
  config.fixture_path = "#{::Rails.root}/spec/fixtures"
  config.use_transactional_fixtures = true
  config.infer_spec_type_from_file_location!
  config.filter_rails_from_backtrace!
end

# spec/spec_helper.rb
RSpec.configure do |config|
  config.expect_with :rspec do |expectations|
    expectations.include_chain_clauses_in_custom_matcher_descriptions = true
  end

  config.mock_with :rspec do |mocks|
    mocks.verify_partial_doubles = true
  end

  config.shared_context_metadata_behavior = :apply_to_host_groups
end

#.rspec
--color
--require rails_helper
--format documentation

# spec/support/factory_bot.rb
RSpec.configure do |config|
  config.include FactoryBot::Syntax::Methods
end

# spec/support/shoulda_matcher.rb
Shoulda::Matchers.configure do |config|
  config.integrate do |with|
    with.test_framework :rspec
    with.library :rails
  end
end

RSpec.configure do |config|
  config.include(Shoulda::Matchers::ActiveRecord, type: :model)
end

$ mkdir -p spec/requests/api/v0
```