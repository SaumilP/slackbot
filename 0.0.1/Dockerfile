FROM node:6
MAINTAINER Saumil Patel "https://saumilp.github.io"

# Software versions
ENV HUBOT_SLACK_VERSION=0.0.1
ENV HUBOT_VERSION=0.4.0
ENV YO_VERSION=1.8.5
ENV COFFEE_SCRIPT=1.10.0

# Usual update / upgrade
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update \
 && apt-get install -y jq

# Clean up APT when done
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install coffee-script, hubot
RUN npm install -g yo@${YO_VERSION} \
        coffee-script@${COFFEE_SCRIPT} \
        generator-hubot@${HUBOT_VERSION}

# Working enviroment
ENV BOTDIR /opt/bot
RUN install -o nobody -d ${BOTDIR}

WORKDIR ${BOTDIR}

# Install Hubot
USER nobody
ENV HOME ${BOTDIR}
RUN yo hubot --name="Hubot" --defaults

# Install slack adapter
RUN npm install hubot-slack@${HUBOT_SLACK_VERSION} --save

# Install moretext
RUN npm install moretext@1.0.0 --save
ADD scripts/moretext.coffee ${BOTDIR}/scripts/moretext.coffee

# Insall standup-alarm
RUN npm install hubot-standup-alarm@0.1.0 --save \
 && (cat external-scripts.json && echo '["hubot-standup-alarm"]') | jq -s add > external-scripts.json.new \
 && mv external-scripts.json.new external-scripts.json

# Install hubot-victory
RUN npm install hubot-victory@1.5.3 --save \
 && (cat external-scripts.json && echo '["hubot-victory"]') | jq -s add > external-scripts.json.new \
 && mv external-scripts.json.new external-scripts.json

# Install sentimental (required redis-server)
# RUN npm install hubot-sentimental@1.0.8 --save \
#  && (cat external-scripts.json && echo '["hubot-sentimental"]') | jq -s add > external-scripts.json.new \
# && mv external-scripts.json.new external-scripts.json

# Install hubot-google-translate
RUN npm install hubot-google-translate@0.2.0 --save \
 && (cat external-scripts.json && echo '["hubot-google-translate"]') | jq -s add > external-scripts.json.new \
 && mv external-scripts.json.new external-scripts.json

# Install hubot-auth
RUN npm install hubot-auth@2.1.0 --save \
 && (cat external-scripts.json && echo '["hubot-auth"]') | jq -s add > external-scripts.json.new \
 && mv external-scripts.json.new external-scripts.json

# Install hubot-darksky
RUN npm install hubot-darksky@1.1.0 --save \
 && (cat external-scripts.json && echo '["hubot-darksky"]') | jq -s add > external-scripts.json.new \
 && mv external-scripts.json.new external-scripts.json

# Install hubot-cron-events
RUN npm install hubot-cron-events@1.0.0 --save \
 && (cat external-scripts.json && echo '["hubot-cron-events"]') | jq -s add > external-scripts.json.new \
 && mv external-scripts.json.new external-scripts.json

 # Install hubot-team
 RUN npm install hubot-team@2.0.0 --save \
  && (cat external-scripts.json && echo '["hubot-team"]') | jq -s add > external-scripts.json.new \
  && mv external-scripts.json.new external-scripts.json

# Install hubot-google-images
RUN npm install hubot-google-images@0.2.6 --save \
 && (cat external-scripts.json && echo '["hubot-google-images"]') | jq -s add > external-scripts.json.new \
 && mv external-scripts.json.new external-scripts.json

# Entrypoint
CMD ["/bin/sh", "-c", "cd ${BOTDIR} && bin/hubot --adapter slack"]
