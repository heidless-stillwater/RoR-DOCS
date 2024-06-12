# New Domain
- ## new domain name
  ```
    westgreenconnection.co.uk

  ```
- ## verify with google
  - ### [verify domain](https://search.google.com/search-console/welcome?sjid=2772788460648112693-EU)

- ## verify with sendgrid
  - ### [Sendgrid: Domain Authentication](https://app.sendgrid.com/settings/sender_auth/domain/create)

# [verify domain ownership](https://support.google.com/webmasters/answer/9008080?hl=en&sjid=2772788460648112693-EU)
- ### [Add a website property to Search Console](https://support.google.com/webmasters/answer/34592?sjid=2772788460648112693-EU)
  - ### [verify domain](https://search.google.com/search-console/welcome?sjid=2772788460648112693-EU)
  ```
    verify the domain with google i.e. heidless.co.uk

  ```

# [sendgrid admin](https://app.sendgrid.com)
  - ## [Sendgrid: API Keys](https://app.sendgrid.com/settings/api_keys)
  - ## [Sendgrid: Sender Authentication](https://app.sendgrid.com/settings/sender_auth)
      - ## [Sendgrid: Domain Authentication](https://app.sendgrid.com/settings/sender_auth/domain/create)
      ```
        define:
          main_sender
          domain

      ```

# Configure Custom Domain
```
DOMAIN: heidless.com

```
- ## Activate Domain for GOOGLE
  - ### ensure svc created in REGION with Domain Mapping functionality i.e. europe-west1
  ```
  # set DEFAULT region/zone
  gcloud config set compute/zone europe-west1-a

  Deploy Svc

  # set domain mapping
  Cloud Run->Manage Custom Domains->Add Mapping->Add Custom Domain->photo-app-0-svc->Cloud Run Domain Mapping
  DNS:
  TXT google-site-verification 54UEwwMf2iW0_uO3kzX_cxTaNEeHdNrqZTOE5mur0gc

  ```

- ### [GUIDE: SENDGRID Domain Authentication](https://www.twilio.com/docs/sendgrid/ui/account-and-settings/how-to-set-up-domain-authentication)
  - ### [app.sendgrid.com](https://app.sendgrid.com/)
  ```
  lockhart.r@gmail.com

  Settings->Sender Authentication
    DNS Host: 123 Reg
    DOMAIN: heidless.com
    # Install DNS Records as specified
    
  ```

  - ### [Trace an email with its full headers and Email Log Search](https://knowledge.workspace.google.com/kb/trace-an-email-with-its-full-headers-and-email-log-search-000009352)
  

  - # STRIPE Login
  ```
  BACKUP Code: vbck-ruzr-ogah-yslv-skih

  Google Authenticator

  ```

  # STRIPE TEST Credentials
  ```
  PUBLISHABLER_KET:
  pk_test_51PLjRQGNOeNKBTc3wA60vBCW1bdhLVc4Y8wP4NX5E1cXiAh2TNYYgGThPvkcEYakAoOS6VNjFlKEBeweZsRnfQ1E009yKKEh2B

  SECRET_KEY:
  sk_test_51PLjRQGNOeNKBTc3eZKbQPlaUWyanXsmwNlHyHkiCUL0AmaG69zx6h2TOOxvXHm6XphlGbQTgr2ML9gzyEmj9mS600VMH0777F

  ```

# [stripe: docs](https://docs.stripe.com/)
  - ## [Stripe Checkout](https://docs.stripe.com/payments/checkout)

# [test card numbers](https://docs.stripe.com/testing)
```
# Testing interactively
# When testing interactively, use a card number, such as 4242 4242 4242 4242. Enter the card number in the Dashboard or in any payment form.

# Use a valid future date, such as 12/34.
# Use any three-digit CVC (four digits for American Express cards).
# Use any value you like for other form fields.

4242 4242 4242 4242
12/34
1234

```


###################
###################


- ### [configure SENDGRID](https://sendgrid.com/en-us)

- ### [SENDGRID for Google Cloud](https://sendgrid.com/en-us/partners/google)
  - ### [GUIDE:sendgrid authentication](https://www.twilio.com/docs/sendgrid/ui/account-and-settings/how-to-set-up-domain-authentication)
```
SIGN IN:
# switch lo google account 'lockhart.r@gmail.com'
# login
https://www.twilio.com/login
  - lockhart.r@gmail.com
  - choose account: lockhart.r@gmail.com

```

- ### configure stripe






```
```
LOGIN:
lockhart.r@gmail.com



```




# [stripe: guides](https://stripe.com/gb/guides)
  - ## 


