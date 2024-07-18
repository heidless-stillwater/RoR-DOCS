

# rails-test-deploy-0 : new APP from base repository
- ## GIT: setup
```
#######################################

APP_NAME=rails-test-deploy-0

git clone https://github.com/heidless-stillwater/rails-v6-1-7-base-0.git ${APP_NAME}

cd ${APP_NAME}

# re-create GitHub repository
rm -rf .git
git init

git branch -m master main
<Publish Repsitory>

#######################################
# replace all occurrences of 'rails-v6-1-7-base-0' for ${APP_NAME}

DB_PREFIX=`echo ${APP_NAME//[-]/_}`
echo ${DB_PREFIX}

psql
--
#CREATE DATABASE newdb WITH TEMPLATE originaldb OWNER dbuser;

CREATE DATABASE rails_test_deploy_0_development;
CREATE DATABASE rails_test_deploy_0_test;

--

#######################################
# reset credentials
rm config/credentials.yml.enc config/master.key

<APP specific credentials>

#######################################
# init DB contents
rails db:setup
rails db:migrate

#######################################
# run & test locally
rails s

```

# Deloy LIVE
```
#######################################
# define ENVIRONMAENT
vi config/.env-vars
``
export GCP_APP_NAME=rails-test-deploy-0

``
source config/.env-vars

echo ${GCP_APP_NAME}

<RoR-INSTALL-DEPLOY>

#######################################
### configure SENDGRID

# verify sender 
https://app.sendgrid.com/settings/sender_auth

Authenticate Domain   # allows validation of all single emails within that domain

# custom DOMAIN MAPPING
https://console.cloud.google.com/run/domains?authuser=0&project=heidless-ror-5



```








```


```



## [How To Set Up Ruby on Rails with Postgres](https://www.digitalocean.com/community/tutorials/how-to-set-up-ruby-on-rails-with-postgres)
```


```





- ## rails
```
#gem list rails
#gem install rails -v 6.1.7.7

rails  _6.1.7.7_ new rails-test-deploy-0 -d postgresql

```

- ## Gemfile
```
gem "dotenv-rails", "~> 2.8"
gem 'base64'
gem 'bigdecimal'
gem 'mutex_m'

group :production do
  gem 'rails_12factor'  
end

```
bundle install

rails db:setup
rails db:migrate

rails generate controller home index

config/routes.rb
--
root 'home#index'

--

# Authentications & Styling
## [init devise & bootstrap](https://www.udemy.com/course/the-complete-ruby-on-rails-developer-course/learn/lecture/3853536#reviews)
--
ISSUE & FIX: The asset "apple-touch-icon-144x144-precomposed.png" is not present in the asset pipeline.
FIX: add ':skip_pipeline'
I.E.: 
    <%= favicon_link_tag 'apple-touch-icon-precomposed.png', :rel => 'apple-touch-icon-precomposed', :type => 'image/png', :skip_pipeline => true %>

--

ISSUE: Upgrade to safe 'fsevents V2'
EXPLANATION: fsevents is Mac OS specific. Not required for other platforms.
FIX: make install optional ins package.json

npm i fsevents --save-optional

--
"optionalDependencies": {
    "fsevents": "^2.0.7"
}

--

# [test API KEY](https://www.twilio.com/docs/sendgrid/ui/account-and-settings/api-keys)
```
curl -i --request POST \
--url https://api.sendgrid.com/v3/mail/send \
--header 'Authorization: Bearer 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' \
--header 'Content-Type: application/json' \
--data '{"personalizations": [{"to": [{"email": "recipient@example.com"}]}],"from": {"email": "support@naught4profit.co.uk"},"subject": "Hello, World!","content": [{"type": "text/plain", "value": "Howdy!"}]}'


```






- ## init app
```
cd saas-app-0

#gem sources
#gem sources --add http://rubygems.org/

#sudo gem update --system

rails db:setup
rails db:migrate

sudo -u postgres psql
\l
ALTER USER heidless CREATEDB;
^D

bundle install

### babel config
# copy updated version of babel.config.js
###

# use SECRET credentials
vi config/databases.yml
--
production:
  <<: *default
  database: <%= ENV["PRODUCTION_DB_NAME"] %>
  username: <%= ENV["PRODUCTION_DB_USERNAME"] %>
  password: <%= Rails.application.credentials.gcp[:db_password] %>
  host: "<%= ENV.fetch("DB_SOCKET_DIR") { '/cloudsql' } %>/<%= ENV["CLOUD_SQL_CONNECTION_NAME"] %>"

--

```



#########################
# ieexcloud.io

## current
lockhart.r@gmail.com


## expired
heidlessemail05@gmail.com
$Ez4waZ2$w7Xjn#

#########################

# sendgrid
- enables email messaging 
- configure & deploy to local end gCloud


# devise
- rich user mgmt package
- configure & deploy to local end gCloud





# install env versions

- ## list all known ruby versions
```
#rvm list known
```

- ## ruby
```
#rvm pkg install openssl

/bin/zsh --login
rvm install 2.6.3 --with-openssl-dir=$HOME/.rvm/usr


/bin/zsh --login
export PATH="/home/heidless/.rvm/gems/ruby-2.6.3/bin:$PATH"
rvm use --default 2.6.3
rvm list
```
- ## node
```

nvm use --default 12.22.12
nvm list

npm -v 
--
8.19.2
--

npm install yarn
yarn -v
--
1.22.22
--
```

- ## bundler
```
gem install bundler -v 2.4.22
bundle update --bundler

gem install pg
bundle config set --local without 'production'
bundle install

```

# utils
```

#gem install webpacker # v5.4.4
--
#gem 'webpacker', '~> 5.4', '>= 5.4.4'
--

rm -rf node_modules yarn.lock
yarn install --check-files

--
rails generate controller welcome index

rails g resource UserStock user:references stock:references

rails routes --expanded | grep user_stocks

rails g migration add_first_last_name_to_users

rails g controller friendships create destroy


```

# devise
```
# add to TOP of Gemfile
gem "devise"

rm -rf node_modules Gemfile.lock yarn.lock
yarn install
bundle install --redownload # Forces a redownload of all gems on the gemfile, assigning them to the new bundler
bin/spring stop
rails generate devise:install

```



###############################################
################ history - REFERENCE ######################

nvm use --default 18.12.1
nvm list

rvm use --default 2.5.1
export PATH="/home/heidless/.rvm/gems/ruby-2.5.1/bin:$PATH"
rvm list

rvm use --default 3.1.4
rvm list

nvm use --default 21.7.3
nvm list

#rails _6.1.7.7_ new finance-tracker-proto

gem install bundler:1.16.5