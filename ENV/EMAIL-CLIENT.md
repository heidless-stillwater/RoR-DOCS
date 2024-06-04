
# TRY AGAIN




########################################
########################################

```
TODO:
- try with SSL : 
  - test with 587
  - test with 465

```
 
# [Using SendGrid's Ruby Library](https://www.twilio.com/docs/sendgrid/for-developers/sending-email/v3-ruby-code-example)

# [sender authentication](https://app.sendgrid.com/settings/sender_auth/domain/configure?s=%7B%22makeLink%22%3Afalse%2C%22provider%22%3A%22Google%20Cloud%22%7D)
- ## [Add, modify, and delete records](https://cloud.google.com/dns/docs/records#console)



# [Action Mailer in Ruby on Rails (and how to deploy with Gmail)](https://dev.to/jhalfman/action-mailer-in-ruby-on-rails-and-how-to-deploy-1nlm)

```
TODO: configure to use gMail in production

```

# [Ruby On Rails - Send confirmation emails for users who sign up to your app](https://www.youtube.com/watch?v=sVJRkTxqlSQ)
```
Rails 5
```

# [udemy: RoR](https://www.udemy.com/course/the-complete-ruby-on-rails-developer-course/learn/lecture/3853538#overview)
```
config/environments/development.rb
--
Rails.application.routes.default_url_options[:host] = 'localhost:3000'

--

config/environments/development.rb
--
Rails.application.configure do
  # Settings specified here will take precedence over those in config/application.rb.
  config.action_mailer.delivery_method = :smtp
  config.action_mailer.default_url_options = { :host => "https://photo-app-0-svc-wei2spmagq-nw.a.run.app", :protocol => "https" }

--
```
# [Google Sendgrid API](https://console.cloud.google.com/marketplace/details/sendgrid-app/sendgrid-email?_ga=2.135787377.1330680949.1716827449-201215364.1713169786&project=heidless-ror-2)
  - ## [sendGrid account](https://app.sendgrid.com/account/details)

# SendGrid ActionMailer
- ## [Setup ActionMailer](https://www.twilio.com/docs/sendgrid/for-developers/sending-email/rubyonrails)
  - ## [sendgrid/twilio account](https://console.twilio.com/)

  - ## [How to Send Emails with Action Mailer and SendGrid in Rails 5](https://medium.com/le-wagon/how-to-send-email-with-action-mailer-and-sendgrid-in-rails-5-32ed0c9167fd)

  - ## [SendGrid:Authentication](https://www.twilio.com/docs/sendgrid/for-developers/sending-email/authentication)

  - ## [SendGrid With Ruby on Rails](https://www.oneworldcoders.com/apprentice-journals/sendgrid-with-ruby-on-rails)
    - ## [Sendgrid not accepting username/password](https://stackoverflow.com/questions/58848022/sendgrid-not-accepting-username-password)
    - ## [Email Activity Feed](https://www.twilio.com/docs/sendgrid/ui/analytics-and-reporting/email-activity-feed)
    - ## [Retrieve all recent access attempts](https://www.twilio.com/docs/sendgrid/api-reference/ip-access-management/retrieve-all-recent-access-attempts)


```
TODO:
- configure action mailer
- init credentials
- create secret
- service account permissons

---
rm config/credentials.yml.enc config/master.key

EDITOR='subl --wait' ./bin/rails credentials:edit

secret_key_base: GENERATED_VALUE
gcp:
  db_password: LtJfjdjUZMrKigjnasuSozQCEdSmxpIuTgtnusJFPbHXcqjcyY
sendgrid_mailer:
  user_name: apikey
  api_key_secret: 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
  domain: photo-app-0-svc-wei2spmagq-nw.a.run.app

  auth_token: f6817edca25a334e5e49bf7fb77d8451
  user_login: lockhart.r@gmail.com
  user_sid: USac89b5bfb4ac2f1c924169bae9cf7a22
  account_sid: AC333bf50a85d1069799c79865221e9406


# working!?
```
ActionMailer::Base.smtp_settings = {
  :user_name => Rails.application.credentials.sendgrid_mailer[:user_name],
  :password => Rails.application.credentials.sendgrid_mailer[:api_key_secret], # secret sendgrid API key
  :domain => Rails.application.credentials.sendgrid_mailer[:domain],
  :address => 'smtp.sendgrid.net',
  :port => 465,   # 465	(for SSL connections). 25, 587	(for unencrypted/TLS connections)
  :authentication => :plain,
  :enable_starttls_auto => true
}

```






TEST API KEY

curl -i --request POST \
--url https://api.sendgrid.com/v3/mail/send \
--header 'Authorization: Bearer SzZ5Wyt2l2Kp8PSdLisRzZTPCU1GXGSd' \
--header 'Content-Type: application/json' \
--data '{"personalizations": [{"to": [{"email": "lockhart.r@gmail.com"}]}],"from": {"email": "sendeexampexample@example.com"},"subject": "Hello, World!","content": [{"type": "text/plain", "value": "Howdy!"}]}'



```

```
# api key

sendgrid-ssl-api-key
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

sendgrid-api-key
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






photo-app-api-0
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




friendly-name: 
photo-app-api-key-0
SID:
SKef51cc1550651d52c159c4c67d8bb2ab
SECRET:
SzZ5Wyt2l2Kp8PSdLisRzZTPCU1GXGSd


FRIENDLY_NAME:
photo-app-api-key-1
SID:
SKc4673b763d26850662129e6fac9a184c
SECRET:
6P7IQLEGja3Rs0dTFiFwPagK45UXS49b


```



# utils - IF NEEDED
echo $GCP_SECRET_NAME
gcloud secrets delete $GCP_SECRET_NAME

## create 'secret'
```
echo $GCP_SECRET_NAME
echo ' '
gcloud secrets create $GCP_SECRET_NAME --data-file config/master.key

```

### describe Secret
```
echo $GCP_SECRET_NAME
gcloud secrets describe $GCP_SECRET_NAME

gcloud secrets versions access latest --secret $GCP_SECRET_NAME

---
0bcafedda94de32d70431034bf5008f0%

```

## setup gcp: secret access permissions

```
# CLOUD COMPUTE access to secrets
echo $GCP_SECRET_NAME
echo $GCP_PROJECT_ID
echo ' '

gcloud secrets add-iam-policy-binding $GCP_SECRET_NAME \
    --member serviceAccount:$GCP_PROJECT_ID-compute@developer.gserviceaccount.com \
    --role roles/secretmanager.secretAccessor

## CLOUD BUILD access to secrets
echo $GCP_SECRET_NAME
echo $GCP_PROJECT_ID
echo ' '

gcloud secrets add-iam-policy-binding $GCP_SECRET_NAME \
    --member serviceAccount:$GCP_PROJECT_ID@cloudbuild.gserviceaccount.com \
    --role roles/secretmanager.secretAccessor

```

### suggestion: [Sending system emails on GCP](https://www.googlecloudcommunity.com/gc/Google-Cloud-s-operations-suite/Sending-system-emails-on-GCP/m-p/630676)


# Secret Mgmt

- local credentials
  ```
  ENV['SENDGRID_USERNAME']
  ENV['SENDGRID_PASSWORD']

  .env
  --
  export SENDGRID_USERNAME='lockhart.r@gmail.com'
  export SENDGRID_PASSWORD='password'
  --  

  .credentials
  

  ```

ATTEMPT:

1:
  :user_name => Rails.application.credentials.sendgrid_mailer[:user_name], # the string literal 'apikey', NOT the ID of your API key
  :password => Rails.application.credentials.sendgrid_mailer[:auth_token], # the secret sendgrid API key
  :domain => Rails.application.credentials.sendgrid_mailer[:domain],

2:
  :user_name => Rails.application.credentials.sendgrid_mailer[:user_sid], # the string literal 'apikey', NOT the ID of your API key
  ...

