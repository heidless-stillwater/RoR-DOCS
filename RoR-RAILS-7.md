# scrachpad
```
gem install rails --version=7.1.3.4
rails _7.1.3.4_ new rails-7-trial-0 --force -d=postgresql

############### Rails 6 ####################
#gem install rails --version=6.1.7.7
#rails _6.1.7.7_ new rails-7-test-3 --force -d=postgresql

/bin/zsh --login
export PATH="/home/heidless/.rvm/gems/ruby-3.3.4/bin:$PATH"
rvm use --default 3.3.4

/bin/zsh --login
export PATH="/home/heidless/.rvm/gems/ruby-3.2.2/bin:$PATH"
rvm use --default 3.2.2

# Dockerfile  
--
FROM ruby:3.3.4-bookworm

RUN (curl -sS https://deb.nodesource.com/gpgkey/nodesource.gpg.key | gpg --dearmor | apt-key add -) && \
    echo "deb https://deb.nodesource.com/node_20.x buster main"      > /etc/apt/sources.list.d/nodesource.list && \
    apt-get update && apt-get install -y nodejs lsb-release
--

############################################


rails db:create
rails db:migrate

rails generate scaffold Posts name:string title:string content:text
rails db:migrate

echo GCP_DB_NAME: ${GCP_DB_NAME}
echo GCP_DB_USER: ${GCP_DB_USER}
echo GCP_PROJECT: ${GCP_PROJECT}
gcloud sql instances list --project=${GCP_PROJECT}

gcloud sql connect ${GCP_INSTANCE} --database=${GCP_DB_NAME} --user=${GCP_DB_USER} --project=${GCP_PROJECT}
uAEEewUNkOojDVRHYVFWbEVPFJfecnhiciBgaHOKZvRTiqEiGK

EDITOR='subl --wait' ./bin/rails credentials:edit
bin/rails credentials:show
```
#####################################################################################
#####################################################################################
#####################################################################################

# [Running Rails on the Cloud Run environment](https://cloud.google.com/ruby/rails/run)
```
gcloud config set project heidless-rails-7-v0

git clone https://github.com/GoogleCloudPlatform/ruby-docs-samples.git

gcloud init

cd ruby-docs-samples/run/rails
bundle install

source config/.env-vars

cat /dev/urandom | LC_ALL=C tr -dc '[:alpha:]'| fold -w 50 | head -n1 > dbpassword
--
fNnRYhqvGjHbsUWeeWOZfvuaAXeUVtnAOxTudqmCCqlvaGgZeK

--

ls ../../RoR-DOCS/Env/Utils
zsh ../../RoR-DOCS/Env/Utils/RoR-CREATE-INSTANCE


gcloud sql instances create ${GCP_INSTANCE} \
    --database-version POSTGRES_15 \
    --tier db-f1-micro \
    --region ${GCP_REGION}

gcloud sql databases create ${GCP_DB_NAME} \
    --instance ${GCP_INSTANCE}

cat /dev/urandom | LC_ALL=C tr -dc '[:alpha:]'| fold -w 50 | head -n1 > dbpassword
--
upYvxGPxZXTumKVcMDgsCZQpjceOhjuTrjCPiABnKTjIpGZRKu

--

gcloud sql users create ${GCP_DB_USER} \
   --instance=${GCP_INSTANCE} --password=$(cat dbpassword)


## Set up a Cloud Storage bucket

```
echo BUCKET: ${GCP_BUCKET}
export bucket_path='gs://'${GCP_BUCKET}
echo $bucket_path

gcloud storage buckets create ${bucket_path} \
    --location=${GCP_REGION}

### [bucket permissions]()
gcloud storage buckets add-iam-policy-binding ${bucket_path} \
    --member=allUsers --role=roles/storage.objectViewer

```

# setup gcp:credentials

```
## make sure to delete previous config/credentials.yml.enc
rm config/credentials.yml.enc config/master.key

---
## password value in file config/credentials.yml.enc
EDITOR='subl --wait' ./bin/rails credentials:edit

gcp:
  db_password: ApmFtuPhBdLjzFlYTlwIUxNaPJWRiHQVjIRxWxVZsgVeRSZJvy

gcp:
  db_password: fNnRYhqvGjHbsUWeeWOZfvuaAXeUVtnAOxTudqmCCqlvaGgZeK
  db_instance_host: heidless-ror-6:europe-west1:rails-7-test-0-instance-0
  db_instance_url: heidless-ror-6:europe-west1:rails-7-test-0-instance-0
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

# Rails.application.credentials.gcp[:db_passsword]

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

## get project number
```
<!-- gcloud projects describe ${GCP_PROJECT_NAME} --format='value(projectNumber)' -->

echo ${GCP_PROJECT_ID}

--

## create Cloud Run service account
#CloudRun->Create Test Service
#Will generate ${GCP_PROJECT_ID}-compute@developer.gserviceaccount.com user account


# CLOUD COMPUTE access to secrets
echo SECRET: $GCP_SECRET_NAME
echo PROJECT_ID: $GCP_PROJECT_ID
echo ' '

# grant access to Cloud Run
gcloud secrets add-iam-policy-binding ${GCP_SECRET_NAME} \
    --member serviceAccount:${GCP_PROJECT_ID}-compute@developer.gserviceaccount.com \
    --role roles/secretmanager.secretAccessor


# grant access to Cloud Build
gcloud secrets add-iam-policy-binding ${GCP_SECRET_NAME} \
    --member serviceAccount:${GCP_PROJECT_ID}@cloudbuild.gserviceaccount.com \
    --role roles/secretmanager.secretAccessor

```

# enable Cloud Build API & Service Account
CloudBuild->Enable Cloud Build API

## [Cloud Build out with sample code](https://cloud.google.com/build/docs/build-push-docker-image?_gl=1*1g2k1sx*_ga*MjAxOTA0OTI2NS4xNzIxNzM5NjMy*_ga_WH2QY8WWF5*MTcyMjMzNTExNS4yNi4xLjE3MjIzMzU2MjUuMzMuMC4w)
```
mkdir quickstart-docker
cd quickstart-docker

echo "Hello, world! The time is $(date)." > quickstart.sh

subl Dockerfile
--
FROM alpine
COPY quickstart.sh /
CMD ["/quickstart.sh"]

--

chmod +x quickstart.sh

## Create a Docker repository in Artifact Registry
gcloud artifacts repositories create quickstart-docker-repo --repository-format=docker \
    --location=us-west2 --description="Docker repository"

## verify repository created
gcloud artifacts repositories list

# build image
gcloud config get-value project
--
heidless-rails-7-v0

heidless-rails-7-v1
--

gcloud builds submit --region=us-west2 --tag us-west2-docker.pkg.dev/heidless-rails-7-v0/quickstart-docker-repo/quickstart-image:tag1

# Build an image using a build config file
subl cloudbuild.yaml
--
steps:
- name: 'gcr.io/cloud-builders/docker'
  script: |
    docker build -t us-west2-docker.pkg.dev/heidless-rails-7-v0/quickstart-docker-repo/quickstart-image:tag1 .
  automapSubstitutions: true
images:
- 'us-west2-docker.pkg.dev/heidless-rails-7-v0/quickstart-docker-repo/quickstart-image:tag1'

--

# start build
gcloud builds submit --region=us-west2 --config cloudbuild.yaml


```

--

# view build details
Choose Region->us-west2
CloudBuild->History

# Connect Rails app to production database and storage
subl .env
--
echo PRODUCTION_DB_NAME: ${GCP_DB_NAME} > .env
echo PRODUCTION_DB_USERNAME: ${GCP_DB_USER} >> .env
echo CLOUD_SQL_CONNECTION_NAME: ${GCP_PROJECT}:${GCP_REGION}:${GCP_INSTANCE} >> .env
echo GOOGLE_PROJECT_ID: ${GCP_PROJECT} >> .env
echo STORAGE_BUCKET_NAME: ${GCP_BUCKET} >> .env
cat .env

--

# Grant Cloud Build access to Cloud SQL
```
gcloud projects add-iam-policy-binding ${GCP_PROJECT} \
    --member serviceAccount:${GCP_PROJECT_ID}@cloudbuild.gserviceaccount.com \
    --role roles/cloudsql.client

```

# Deploying the app to Cloud Run
```
echo ${GCP_PROJECT}
echo ${GCP_SERVICE_NAME}
echo ${GCP_INSTANCE}
echo ${GCP_REGION}
echo ${GCP_SECRET_NAME}
echo ' '

gcloud builds submit --config cloudbuild.yaml \
    --substitutions _SERVICE_NAME=${GCP_SERVICE_NAME},_INSTANCE_NAME=${GCP_INSTANCE},_REGION=${GCP_REGION},_SECRET_NAME=${GCP_SECRET_NAME}

gcloud run deploy ${GCP_SERVICE_NAME} \
     --platform managed \
     --region ${GCP_REGION} \
     --image gcr.io/${GCP_PROJECT}/${GCP_SERVICE_NAME} \
     --add-cloudsql-instances ${GCP_PROJECT}:${GCP_REGION}:${GCP_INSTANCE} \
     --allow-unauthenticated

```
