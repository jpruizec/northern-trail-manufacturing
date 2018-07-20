## Northern Trail Manufacturing

Read [this blog post]() for more information.

The Northern Trail Manufacturing App is written in Node.js and built to run on Heroku. It is a companion to the <a href="https://github.com/trailheadapps/northern-trail-outfitters">Northern Trail Outfitters</a> app, built on Salesforce. Using the two apps, you can explore how to integrate decoupled applications with Salesforce via Platform Events.

Follow the instructions below to deploy your own instance of the application:

## 1. Install and Configure the Salesforce App

1. Install the Northern Trail Outfitters Salesforce application first. See instructions here: <a href="https://github.com/trailheadapps/northern-trail-outfitters">https://github.com/trailheadapps/northern-trail-outfitters</a>

1. In **Setup > Users**, create an integration user that you will use to connect to Salesforce from the Node.js app. Select **Salesforce** as the license type and **System Administrator** as the profile. 

1. Log in (at least once) as that user via your browser. For scratch orgs, use <a href="https://test.salesforce.com">https://test.salesforce.com</a> as the login URL. For Develper Edition orgs, use <a href="https://login.salesforce.com">https://login.salesforce.com</a>. Choose to not register your phone number.

1. In **Setup > Users > Permission Sets**, assign your integration user to the **NTO** permission set.

1. Create a Connected App in your scratch org or your developer edition:
    - In **Setup > Apps > App Manager**, click **New Connected App**
    - Specify a Connected App Name. For example, **NTO Manufacturing**
    - Enter your email address for **Contact Email**
    - Enter **http://localhost:3000/oauth/_callback** as the Callback URL (This URL is not used in the application)
    - Check **Enable OAuth Settings**
    - Add **Full access (full)** to the **Selected OAuth Scopes**
    - Click **Save** and click **Continue**

## 2. Install the Manufacturing App

### Option 1: Install the Manufacturing App using the Heroku button

1. Make sure you are logged in to the Heroku Dashboard
1. Click the button below to deploy the manufacturing app on Heroku:

    [![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

1. Fill in the config variables as follows:
    - For **SF_CONSUMER_KEY**, enter the Consumer Key of your Salesforce Connected App
    - For **SF_CONSUMER_SECRET**, enter the Consumer Secret of your Salesforce Connected App
    - For **SF_USER_NAME**, enter the the username of your Salesforce user
    - For **SF_USER_PASSWORD**, enter the the password of your Salesforce user
    - For **SF_ENVIRONMENT**, enter the environment. Enter **sandbox** if using a scratch org, or **production** if using a regular Developer Edition.

### Option 2: Install the Manufacturing App manually

1. Clone this repository:
    ```
    git clone https://github.com/trailheadapps/northern-trail-manufacturing
    cd northern-trail-manufacturing
    ```

1. Create a Heroku app and give it a name:
    ```
    heroku create *your_app_name*
    ```

1. Set the Heroku config variables (replace with values from your connected app):
    
    ```bash
    heroku config:set SF_CONSUMER_KEY=*your_connected_consumer_key*
    heroku config:set SF_CONSUMER_SECRET=*your_connected_consumer_secret*
    heroku config:set SF_USER_NAME=*your_integration_user_name*
    heroku config:set SF_USER_PASSWORD=*your_integration_user_password*
    heroku config:set SF_ENVIRONMENT=*your_env_type*
    ```

    Set **SF_ENVIRONMENT** to **sandbox** if using a scratch org, or **production** if using a Developer Edition.

1. Push the code to your Heroku app: 
    ```
    git push heroku master
    ```

    or run the application locally:
    ```
    heroku run:local npm start
    ```

**Note:** If you're using a scratch org for this integration, keep in mind that you'll need to repeat the above steps and re-set your Heroku app's config variables when your scratch org expires.

## Troubleshooting

- Make sure you can successfully login with your integration user in a browser window (using https://test.salesforce.com for scratch orgs or https://login.salesforce.com for regular developer editions)
- Make sure the System Administrator profile has an IP Range set from 0.0.0.0 to 255.255.255.255.
- Make sure you assigned your integration user to the NTO permission set
- Check the Heroku logs
- Check the browser console log