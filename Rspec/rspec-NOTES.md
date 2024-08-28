

# [RSpec TDD - How To Unit Test Ruby On Rails 6 Apps For Absolute Beginners](https://www.youtube.com/watch?v=AAqPc0j_2bg&t=121s)
```

gem install rails -v 6.1.7.7

/bin/zsh --login
export PATH="/home/heidless/.rvm/gems/ruby-3.2.2/bin:$PATH"
rvm use --default 3.2.2

rails  _6.1.7.7_ new rails-test-0 -d postgresql

```

# [railsbytes: rails templates](https://railsbytes.com/)
```
rails new tested-app -t
cd tested-app

vi Gemfile
--
group :development do
  gem 'rspec-rails'
  ...
--

# add 'RSpec' Templates
# https://railsbytes.com/public/templates/z0gsLX
#
rails app:template LOCATION="https://railsbytes.com/script/z0gsLX"


vi Gemfile
--
gem 'devise'

--
bundle install

rails g devise:install
rails g devise:User   # create devise Users

rails db:migrate RAILS_ENV=test

rails spec

# generate minimal app as example to create tests
rails g scaffold posts title:string body:text user:references views:integer
*
vi db/migrate/*_create_posts
--
      t.integer :views, default: 0

--
rails db:migrate RAILS_ENV=test

rails spec




```





# Reference
## [The basic structure (describe/it)](https://rspec.info/features/3-12/rspec-core/example-groups/basic-structure/)
## [before and after hooks](https://rspec.info/features/3-12/rspec-core/hooks/before-and-after-hooks/)
## [Module: RSpec::Matchers](https://www.rubydoc.info/gems/rspec-expectations/RSpec/Matchers)

-----

# Tutorials
## [rspec: tutorial - udemy](https://www.udemy.com/course/testing-ruby-with-rspec/learn/lecture/12418070#overview)
## [RSpec Tutorial for Beginners](https://www.youtube.com/watch?v=-uhFA74eBG0)
## [deanin: RSpec TDD - How To Unit Test Ruby On Rails 6 Apps For Absolute Beginners](https://www.youtube.com/watch?v=AAqPc0j_2bg&t=121s)

# GIT
## [udeny-rspec](https://github.com/heidless-stillwater/udeny-rspec)

# admin
```
gem install rspec

```

# new project
```
rspec --init


```

# run tests
```
# runs all tests in 'spec' folder
rspec

# run specific file
rspec spec/card_spec.rb



```
