# Amazon Alexa and PubNub with the skill adapter code as a web service
This repository has the source code for my blog post about **Voice controlled home automation with Amazon Alexa and Pubnub**
This repository hosts the code for an alexa adapter running as a web service on cloud hosting platform such as heroku (as opposed to AWS Lambda function in the other repository https://github.com/gopal-amlekar/alexa-pubnub-aws).

Steps to follow:
* Create an account on Heroku (https://signup.heroku.com/dc).
* Download Heroku CLI and verify you have correct versions of node, npm and git installed on your host system. Follow the steps https://devcenter.heroku.com/articles/getting-started-with-nodejs#set-up
* Navigate to the folder where this git repository is checked out.
* Login to Heroku from command line:
```shell
  heroku login
	Enter your Heroku credentials:
	Email: test@xyz.com
	Password:
	Logged in as test@xyz.com
```
* Create a web app with following commands:
```shell
	heroku create
	Creating app... done, demo-app-96357 (Heroku will assign a random name to your app)
	https://demo-app-96357.herokuapp.com/ | https://git.heroku.com/demo-app-96357.git
```
* Add following details as environment variables on heroku. (Refer https://devcenter.heroku.com/articles/config-vars)
  * PUB_NUB_CHANNEL_KEY=alexa_world
  * PUB_NUB_PUBLISH_KEY=YOUR_PUBNUB_PUBLISH_KEY
  * PUB_NUB_SUBSCRIBE_KEY=YOUR_PUBNUB_SUBSCRIBE_KEY
  * AMAZON_APP_KEY=YOUR_AMAZON_SKILL_APP_KEY
  * WEB_APP_ROUTE=ANY_RANDOM_STRING
  This random string becomes part of the https endpoint. For e.g. if your app name is https://dreadful-bay-34521-herokuapp.com, and you chose "My-endpoint-6789" as your WEB_APP_ROUTE then the https endpoint becomes https://dreadful-bay-34521-herokuapp.com/My-endpoint-6789.

* Go back to https://developer.amazon.com and navigate to your alexa skill's configuration. Add this endpoint to the configuration section as an HTTPS endpoint (not AWS ARN). You can put this endpoint for North america and Europe both.

* Make sure to select the SSL certificate option there as "My development endpoint is a sub-domain of a domain that has a wildcard certificate from a certificate authority". 
  
* Save the configuration and go ahead to test your endpoint. You should get a valid response back. Also, you should get a message on the pubnub channel alexa_world as well.
  
* For more details read my blog post https://abszeroblog.wordpress.com/
