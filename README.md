# Amazon Alexa and Pubnub with the skill adapter code as a web service
This repository has the source code for my blog post about **Voice controlled home automation with Amazon Alexa and Pubnub**
This repository hosts the code for an alexa adapter running as a web service on cloud hosting platform such as heroku (as opposed to AWS Lambda function in the other repository https://github.com/gopal-amlekar/alexa-pubnub-aws).

Steps to follow:
* Login to heroku and follow the steps on this webpage - https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction
* Once you have the basic heroku app up and running, replace the content of your app folder with the contents of this repository. 
* You can even delete the folder node_modules in your directory. 
* Follow the steps to deploy the heroku app:
  ``` shell 
  git add .
  git commit -m "Skill adapter code"
  git push heroku master
  ``` 
* Add following details as environment variables on heroku. (Refer https://devcenter.heroku.com/articles/config-vars)
  * PUB_NUB_CHANNEL_KEY=alexa_world
  * PUB_NUB_PUBLISH_KEY=YOUR_PUBNUB_PUBLISH_KEY
  * PUB_NUB_SUBSCRIBE_KEY=YOUR_PUBNUB_SUBSCRIBE_KEY
  * AMAZON_APP_KEY=YOUR_AMAZON_SKILL_APP_KEY
  * WEB_APP_ROUTE=ANY_RANDOM_STRING
  This string becomes part of the https endpoint. For e.g. if your app name (assigned by heroku) is https://dreadful-bay-34521-herokuapp.com, and you chose "My-endpoint-6789" as your WEB_APP_ROUTE then the https endpoint becomes https://dreadful-bay-34521-herokuapp.com/My-endpoint-6789.

Go back to developer.amazon.com and navigate to your alexa skill's configuration. Add this endpoint to the configuration section as an HTTPS endpoint (not AWS ARN). You can put this endpoint for North america and Europe both.

Make sure to select the SSL certificate option there as "My development endpoint is a sub-domain of a domain that has a wildcard certificate from a certificate authority". 
  
Save the configuration and go ahead to test your endpoint. You should get a valid response back. Also, you should get a message on the pubnub channel alexa_world as well.
  
For more details read my blog post https://abszeroblog.wordpress.com/
