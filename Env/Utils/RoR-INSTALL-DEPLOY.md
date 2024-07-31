
# Utils

- ## [Fix Rails Blocked Host Error with Docker](https://danielabaron.me/blog/rails-blocked-host-docker-fix/)

- ## [production ready rails/docker - docker-rails-example](https://github.com/nickjj/docker-rails-example)

- ## [Running Rails on Google Cloud](https://cloud.google.com/ruby/rails)
    - ### [Running Rails on the Cloud Run environment ](https://cloud.google.com/ruby/rails/run)
    - ### - [Quickstart: Deploy a Ruby service to Cloud Run](https://cloud.google.com/run/docs/quickstarts/build-and-deploy/deploy-ruby-service)

# [Running Rails on the Cloud Run environment ](https://cloud.google.com/ruby/rails/run)

### Cloning the Rails app
```
#git clone https://github.com/GoogleCloudPlatform/ruby-docs-samples.git

#cd ruby-docs-samples/run/rails

git clone https://github.com/heidless-stillwater/rails-cat-album-gcloud-deploy.git

cd rails-cat-album-gcloud-deploy/run/rails

cd gcloud-run-ruby-proto/run/cat-photo-album

bundle install
```

## Generate RAILS_MASTER_KEY - If REQUESTED
```
# refreshes 'config/master.key' & 'config/credentials.enc' 
EDITOR='subl --wait' ./bin/rails credentials:edit
```

## dotenv environment
### [Setting up Dotenv in Rails](https://onlyoneaman.medium.com/setting-up-dotenv-in-rails-a8ce1c69e03d)
```
# initialise .env
touch .env

```

##############################################
########### setup & deploy app ###############
##############################################

## create SQL instance

### [instances](https://console.cloud.google.com/sql/instances?project=heidless-pfolio-deploy-5)

### USEFUL IF NEEDED
```
# enable/disable deletion protection
gcloud sql instances patch cat-photo-album-0 \
    --deletion-protection

```

## prep OS
```
<!-- cd ./run/cat-photo-album
yarnpkg add -W caniuse-lite
sudo npm install -g n
sudo n latest
npx update-browserslist-db@latest
sudo apt install apt-utils -->


# prep OS
sudo apt install apt-utils
```

# initialise app
```
gcloud init

```

#######################################################
#######################################################


# Database

### [gcp: Create a DATABASE](https://console.cloud.google.com/sql/instances/blog-demo-instance-1/databases?project=heidless-pfolio-deploy-5)

```
#gcloud alpha sql tiers list

#gcloud sql instances patch alpha-blog-0-instance-0 \
#    --no-deletion-protection

#########
# set env

# fin-track
/bin/zsh --login
export PATH="/home/heidless/.rvm/gems/ruby-2.6.3/bin:$PATH"
rvm use --default 2.6.3


/bin/zsh --login
export PATH="/home/heidless/.rvm/gems/ruby-3.2.2/bin:$PATH"
rvm use --default 3.2.2

/bin/zsh --login
export PATH="/home/heidless/.rvm/gems/ruby-3.3.2/bin:$PATH"
rvm use --default 3.3.2

/bin/zsh --login
export PATH="/home/heidless/.rvm/gems/ruby-3.3.3/bin:$PATH"
rvm use --default 3.3.3
  

# all other apps
/bin/zsh --login
export PATH="/home/heidless/.rvm/gems/ruby-3.3.4/bin:$PATH"
rvm use --default 3.3.4

source ./config/.env-vars

gcloud init

create_instance_dir='../../../RoR-DOCS/Env/Utils/RoR-CREATE-INSTANCE'
ls ${create_instance_dir}
zsh ${create_instance_dir}

# initialise Cloud Run - generates service account
#Cloud Run->Create Service->Select->Demo Containers->hello

# initialise Cloud Buld - generates service account
#Cloud Buld->Enable API

#########

echo GCP_INSTANCE: ${GCP_INSTANCE}
echo GCP_PROJECT: ${GCP_PROJECT}
echo ' '
gcloud sql instances delete ${GCP_INSTANCE} \
--project=${GCP_PROJECT}

```

## create Instance
```
echo INSTANCE: $GCP_INSTANCE
echo PROJECT: $GCP_PROJECT_NAME
echo DB_VERSION: $GCP_DB_VERSION
echo REGION: $GCP_REGION
echo ' '
gcloud sql instances create $GCP_INSTANCE \
    --project $GCP_PROJECT_NAME \
    --database-version $GCP_DB_VERSION \
    --tier db-f1-micro \
    --region $GCP_REGION 


# public instance IP
echo INSTANCE: $GCP_INSTANCE
echo PROJECT: $GCP_PROJECT_NAME
echo ' '
gcloud sql instances describe $GCP_INSTANCE \
--project=$GCP_PROJECT_NAME | grep ipAddress:

--
35.197.255.67
--
```

## set password on 'postgres' user
```
echo INSTANCE: $GCP_INSTANCE
echo ' '
gcloud sql users set-password postgres \
--instance=$GCP_INSTANCE \
--password=postgres

```

## create DB
```
gcloud sql databases delete $GCP_DB_NAME \
    --instance $GCP_INSTANCE

echo 'create DB'
echo DB: $GCP_DB_NAME
echo INSTANCE: $GCP_INSTANCE
echo ' '
gcloud sql databases create $GCP_DB_NAME \
    --instance $GCP_INSTANCE

```

### create USER
### [gcp: create user](https://console.cloud.google.com/sql/instances/blog-demo-instance-1/users?project=heidless-pfolio-deploy-5)
```
# generate password to 'dbpassword'.
# in PRODUCTION USE 'dbpassword'. 

cat /dev/urandom | LC_ALL=C tr -dc '[:alpha:]'| fold -w 50 | head -n1 > dbpassword

---
echo DB_USER: $GCP_DB_USER
echo INSTANCE: $GCP_INSTANCE
echo ' '
gcloud sql users create $GCP_DB_USER \
   --instance=$GCP_INSTANCE --password=$(cat dbpassword)

```

## Set up a Cloud Storage bucket
### [storage bucket](https://console.cloud.google.com/storage/browser?referrer=search&project=heidless-pfolio-deploy-5&prefix=&forceOnBucketsSortingFiltering=true)

```
echo BUCKET: ${GCP_BUCKET}
export bucket_path='gs://'${GCP_BUCKET}
echo $bucket_path

gsutil mb -l ${GCP_REGION} ${bucket_path}

```

### [bucket permissions]()
```
gsutil iam ch allUsers:objectViewer $bucket_path

```

## configure Credential
### Create encrypted credentials file and store key as Secret Manager secret

### install sublime - IF NEEDED
```
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/sublimehq-archive.gpg > /dev/null

echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list

sudo apt-get update
```

### ubuntu window - if NEEDED
```
sudo apt-get install sublime-text
```

### setup gcp:credentials
### sets up encryped crtedentials for use in live

```

# IF WONT START:
#   - remove Gemfile.lock
#   - bundle install

---
# get password from './dbpassword'

---
--

SAAS_APP_PWD: CAfYgPFFHaKBjszefpkSMrVmQZRJVNBoEEHslUZIuMKYviOovw

RAILS-TEST-DEPLOY-PWD: wVICYjmSfrnrZzeyHbCxImRpavdjyqBirvJusLqcbgDhBscugY
RAILS-TEST-DEPLOY-DOMAIN: lockhartarts.com

S3_BUCKET: heidless-pdf-ninja
S3_BUCKET: heidless-photoappimages

ACTIVE-STORAGE-TST-PWD: wYTStfqZIHJzOrqbqYvxeRwTGHtSBIZnVIyEhuCItahZbmyLcZ
ACTIVE-STORAGE-TST-DOMAIN: ????

ACTIVE-STORAGE-TST-2-PWD: sERSjGXFpFPGoORaNHZlwybhfceRfkFBXOLuRlTXumpdDHykdB
ACTIVE-STORAGE-TST-2-DOMAIN: ????

PHOTO_APP_PWD: LtJfjdjUZMrKigjnasuSozQCEdSmxpIuTgtnusJFPbHXcqjcyY
PHOTO_APP_DOMAIN: fundingcloud.co.uk
PHOTO_APP_API:
--
  user_name: apikey
  api_key_secret: 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

--

ALPHA_BLOG_PWD: zfpKxOEhNmNwMmZlaGXsbhDQtAWbTSjwRJWUgGGQwBoLYszrMT
ALPHA_BLOG_DOMAIN: heidless.co.uk

FIN_TRACK_PWD: VFHuZyCAfafqNfxqvLszQwHWraHYqBBNdICIZcBZGzWWNpouIH
FIN_TRACK_DOMAIN: heidless.co.uk

CAT_PHOTO_PWD: IpbXXpOEFNOcFpDQOFglMrFNUhkjUIoxENJxBCERUTUmWYuOvp
CAT_PHOTO_DOMAIN: heidless.co.uk

RAILS-PDF-NINJA-PWD: RZkdECZnICBPqPSbDhlGYRboqJNxCRIQKWXfzkMqGaIxzoYAax
RAILS-PDF-NINJA-DOMAIN: fundingcloud.com

RAILS-V6-1-7-BASE-PWD: seGgomNdejNgIUIdtxRwQVEslQnsrHropJNQZLgGxlSlRJXaxb
RAILS-V6-1-7-BASE-DOMAIN: naught4profit.co.uk
RAILS-V6-1-7-BASE-API:
--
    apikey_rails_v6
    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

    apikey-test-1
    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

--

BULLET-TRAIN-TEST-0:  qMMCnXvLNwmluQyeSCYoPeXpPwDnVcuSZaqzgXQHQddHubFeXm

RAILS-7-TEST-0:  uAEEewUNkOojDVRHYVFWbEVPFJfecnhiciBgaHOKZvRTiqEiGK

rails-pdf-test-0-instance-0:  uAEEewUNkOojDVRHYVFWbEVPFJfecnhiciBgaHOKZvRTiqEiGK

rails-7-trial-0-instance-0: kEPZSUMoRGdstKuMLkIVWKzMGeNtSPIBdeZDNNFHoOMXFfcJDZ

bullet-test-0-instance-0: qMMCnXvLNwmluQyeSCYoPeXpPwDnVcuSZaqzgXQHQddHubFeXm

bullet-test-1-instance-0: qMMCnXvLNwmluQyeSCYoPeXpPwDnVcuSZaqzgXQHQddHubFeXm

bullet-train-0-instance-0: qMMCnXvLNwmluQyeSCYoPeXpPwDnVcuSZaqzgXQHQddHubFeXm

# make sure to delete previous config/credentials.yml.enc
rm config/credentials.yml.enc config/master.key

---
# password value in file config/credentials.yml.enc
#EDITOR='subl --wait' ./bin/rails credentials:edit 

EDITOR='subl --wait' ./bin/rails credentials:edit

gcp:
  db_password: qMMCnXvLNwmluQyeSCYoPeXpPwDnVcuSZaqzgXQHQddHubFeXm
  db_database: bullet-train-0-db-0
  db_username: bullet-train-0-user-0
  db_instance_host: heidless-ror-6:europe-west1:bullet-train-0-instance-0
aws_credentials:
  S3_ACCESS_KEY: AKIAYUPGERUW63AOF5TE
  S3_SECRET_KEY: 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
  S3_BUCKET: heidless-photoappimages
  AWS_REGION: eu-west-2   
iex_client:
  api_key: pk_808439936a93476fb7558256a9b6da5c
  secret_api_key: sk_7de5c9cf9cb74ec3ad57523bc62cc986
stripe:
  test_publishable_key: pk_test_51PLjRQGNOeNKBTc3wA60vBCW1bdhLVc4Y8wP4NX5E1cXiAh2TNYYgGThPvkcEYakAoOS6VNjFlKEBeweZsRnfQ1E009yKKEh2B
  test_secret_key: sk_test_51PLjRQGNOeNKBTc3eZKbQPlaUWyanXsmwNlHyHkiCUL0AmaG69zx6h2TOOxvXHm6XphlGbQTgr2ML9gzyEmj9mS600VMH0777F 
sendgrid_mailer:
  user_name: apikey
  api_key_secret: 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
  domain_svc: photo-app-0-svc-d57dc7eqba-ew.a.run.app
  mail_sender: support@heidless.co.uk
  domain: heidless.co.uk
  auth_token: f6817edca25a334e5e49bf7fb77d8451
  user_login: lockhart.r@gmail.com
  user_sid: USac89b5bfb4ac2f1c924169bae9cf7a22
  account_sid: AC333bf50a85d1069799c79865221e9406

# Used as the base secret for all MessageVerifiers in Rails, including the one protecting cookies.
secret_key_base: 0d8cb44bdd6a27f074151e3d4b2f489c13fcbf1a4662c04958f7fd615db15a60ba3e07552c4932dd8b2fae0260f03f5285e0ac61df52a981c85c3fe188e99d21

```

```
# utils - IF NEEDED
echo SECRET: ${GCP_SECRET_NAME}
echo ' '
gcloud secrets delete ${GCP_SECRET_NAME}

```

## create 'secret'
```
echo SECRET: ${GCP_SECRET_NAME}
echo ' '
gcloud secrets create ${GCP_SECRET_NAME} --data-file config/master.key

```

### describe Secret
```
echo SECRET: $GCP_SECRET_NAME
gcloud secrets describe $GCP_SECRET_NAME

gcloud secrets versions access latest --secret $GCP_SECRET_NAME

---
38f6c4c4cb1e5edc0c6b32c65ff677ed

```

## setup gcp: secret access permissions

```
# CLOUD COMPUTE access to secrets
echo SECRET: $GCP_SECRET_NAME
echo PROJECT_ID: $GCP_PROJECT_ID
echo ' '

gcloud secrets add-iam-policy-binding $GCP_SECRET_NAME \
    --member serviceAccount:$GCP_PROJECT_ID-compute@developer.gserviceaccount.com \
    --role roles/secretmanager.secretAccessor

## CLOUD BUILD access to secrets
#echo PROJECT: $GCP_SECRET_NAME
#echo PROJECT_ID: $GCP_PROJECT_ID
#echo ' '

#gcloud secrets add-iam-policy-binding $GCP_SECRET_NAME \
#    --member serviceAccount:$GCP_PROJECT_ID@cloudbuild.gserviceaccount.com \
#    --role roles/secretmanager.secretAccessor

```

## Connect Rails app to production database and storage
### .env
```
cd PROJECT_ROOT
touch .env
---
echo ' '
echo "PRODUCTION_DB_NAME: $GCP_DB_NAME" > .env
echo "GOOGLE_PROJECT_ID: $GCP_PROJECT_ID" >> .env
echo "CLOUD_SQL_CONNECTION_NAME: $GCP_PROJECT:$GCP_REGION:$GCP_INSTANCE" >> .env
echo "PRODUCTION_DB_USERNAME: $GCP_DB_USER" >> .env
echo "STORAGE_BUCKET_NAME: $GCP_BUCKET" >> .env

#echo "AWS_ACCESS_KEY_ID: ${AWS_ACCESS_KEY_ID}" >> .env
#echo "AWS_SECRET_ACCESS_KEY: ${AWS_SECRET_ACCESS_KEY}" >> .env
#echo "AWS_S3_BUCKET: ${AWS_S3_BUCKET}" >> .env
#echo "AWS_S3_REGION: ${AWS_S3_REGION}" >> .env

echo "SENDGRID_API_KEY: $GCP_SENDGRID_API_KEY" >> .env
more .env

```

### Grant Cloud Build access to Cloud SQL
```
echo GCP_SECRET_NAME: $GCP_SECRET_NAME
echo GCP_PROJECT: $GCP_PROJECT
echo GCP_PROJECT_ID: $GCP_PROJECT_ID
echo ' '
gcloud projects add-iam-policy-binding $GCP_PROJECT \
    --member serviceAccount:$GCP_PROJECT_ID@cloudbuild.gserviceaccount.com \
    --role roles/cloudsql.client

```

################################################################
# Deploying the app to Cloud Run
```
## ensure gem "dotenv-rails", "~> 2.8" is available
```

```
/bin/zsh --login
export PATH="/home/heidless/.rvm/gems/ruby-3.3.2/bin:$PATH"
rvm use --default 3.3.


```
echo ' '
echo GCP_SERVICE_NAME: ${GCP_SERVICE_NAME}
echo GCP_INSTANCE: ${GCP_INSTANCE}
echo GCP_REGION: ${GCP_REGION}
echo GCP_SECRET_NAME: ${GCP_SECRET_NAME}
echo ' '

gcloud builds submit --config cloudbuild.yaml \
    --substitutions _SERVICE_NAME=${GCP_SERVICE_NAME},_INSTANCE_NAME=${GCP_INSTANCE},_REGION=${GCP_REGION},_SECRET_NAME=${GCP_SECRET_NAME} 


---
echo ' '
echo GCP_SERVICE_NAME: ${GCP_SERVICE_NAME}
echo GCP_REGION: ${GCP_REGION}
echo GCP_PROJECT: ${GCP_PROJECT}
echo GCP_INSTANCE: ${GCP_INSTANCE}
echo GCP_SECRET_NAME: ${GCP_SECRET_NAME}
echo ' '

gcloud run deploy ${GCP_SERVICE_NAME} \
     --platform managed \
     --region ${GCP_REGION} \
     --image gcr.io/${GCP_PROJECT}/${GCP_SERVICE_NAME} \
     --add-cloudsql-instances ${GCP_PROJECT}:${GCP_REGION}:${GCP_INSTANCE} \
     --allow-unauthenticated


#############################
## CLOUD RUN: domain mappings
gcloud domains list-user-verifiedls


DOMAIN=westgreenconnection.co.uk
echo DOMAIN: ${DOMAIN}
echo GCP_SERVICE_NAME: ${GCP_SERVICE_NAME}
gcloud beta run domain-mappings create --service ${GCP_SERVICE_NAME} --domain ${DOMAIN} --force-override

---

```
####################################################
# cloud-sql-proxy 
## if needed...
####################################################

## start proxy
##curl -o cloud-sql-proxy https://storage.googleapis.com/cloud-sql-connectors/cloud-sql-proxy/v2.11.0/cloud-sql-proxy.linux.amd64
##chmod +x cloud-sql-proxy

#./cloud-sql-proxy -instances=$GCP_PROJECT_ID:$GCP_REGION:$GCP_INSTANCE=tcp:3306 -credential_file=heidless-ror-0-658f2b5978e6 &

```
#export GOOGLE_CLOUD_PROJECT=heidless-ror-0
#export USE_CLOUD_SQL_AUTH_PROXY=true
#export CLOUDRUN_SERVICE_URL=https://heidless-pfolio-deploy-7@appspot.gserviceaccount.com

```

### enable cloud proxy
```
#./cloud-sql-proxy --credentials-file ./heidless-ror-0-658f2b5978e6.json \
#--port 1234 heidless-ror-0:europe-west2:fin-tracker-0-instance-0 

# kill & restart - IF address already in use
#sudo lsof -i -P -n | grep LISTEN
#kill -9 <PID>




```
rails s     # fails with webpack issues

bundle exec rails webpacker:install     # then retry

npm install --save-dev @babel/plugin-transform-private-methods
npm install --save-dev @babel/core@^7.0.0-0
npm install --save-dev @babel/plugin-proposal-private-methods

npm i fsevents@2.2.1


    create_table :articles do |t|
      t.text :title
      t.text :description
      t.timestamps

rails generate scaffold Article title:text description:text user:references
rails g bootstrap:themed Articles
article = Article.new(title: "third article", description: "description of third article", user_id: 1)

<%= link_to t('.back', :default => t("helpers.links.back")),
              articles_path, :class => 'btn btn-default'  %>
<%= link_to t('.edit', :default => t("helpers.links.edit")),
              edit_article_path(@article), :class => 'btn btn-default' %>
<%= link_to t('.destroy', :default => t("helpers.links.destroy")),
              article_path(@article),
              :method => 'delete',
              :data => { :confirm => t('.confirm', :default => t("helpers.links.confirm", :default => 'Are you sure?')) },
              :class => 'btn btn-danger' %>


rails generate scaffold Image name:string picture:string user:references


rails generate scaffold Pdf name:string description:string pdfdoc:string user:references

rails db:migrate

rails g bootstrap:themed Pdfs

user.rb
--
has_many :pdfs

--

rails generate uploader Pdfdoc




