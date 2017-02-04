# Slack-integrated Hubot


Setup hubot from https://slack.com/services/new/hubot and assign the API token to the following command:

```
docker pull saumilp/slackbot
docker run -e HUBOT_SLACK_TOKEN=xoxb-137727454998-ioDQwyOnuuD7ps2OU5Lb -d saumilp/slackbot
```
Alternatively:
```
git clone git@github.com:SaumilP/slackbot.git
sudo docker build -t --tag slackbot .
docker run -e HUBOT_SLACK_TOKEN=xoxb-137727454998-ioDQwyOnuuD7ps2OU5Lb slackbot
```

# Hubot Scripts
* hubot-diagnostics
* hubot-help
* hubot-heroku-keepalive
* hubot-google-images
* hubot-google-translate
* hubot-pugme
* hubot-maps
* hubot-redis-brain
* hubot-rules
* hubot-shipit
* hubot-moretext
* hubot-standup-alarm
* hubot-victory
* hubot-darksky
* hubot-auth
* hubot-pubsub

## Reference
* Bot Users | Slack https://api.slack.com/bot-users
