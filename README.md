# Hello from the Zendomo Team

### Here is a set of instructions to make this work locally for you.

#### Pre-reqs:
- Docker > v17.03
- Docker-compose > v1.8
- npm v5.x (nothing else)
- git
- Python > v2.7

To do this:

- brew install docker
- brew install docker-compose
- npm is probably fine but check the version...
- if you dont have git I dont know how you are reading this
- you should have python, but check python --version, and get it if you dont

then download docker from their website, run it until you see the green light...

#### Instructions:
- npm i -g composer-cli
- npm i -g generator-hyperledger-composer
- npm i -g composer-rest-server
- npm i -g yo

This installs Hyperledger composer, generator, server, && yeoman (it runs stuff automagically for you).

All of these are mandatory.

#### Starting up Zendomo:
- First we gotta make sure docker isnt going to hamstring our butts:
run:
-  docker kill $(docker ps -q)         //kills all open docker processes
-  docker rm $(docker ps -aq)          //cleaning up...
-  docker rmi $(docker images dev-* -q)  //cleaning up docker images...

- OPTIONAL: THIS REPO CONTAINS THESE THINGS, BUT FOR CLARITYS SAKE IL INCLUDE THE WHOLE PROCESS

- mkdir ~/fabric-tools && cd ~/fabric-tools

- curl -O https://raw.githubusercontent.com/hyperledger/composer-tools/master/packages/fabric-dev-servers/fabric-dev-servers.zip

- unzip fabric-dev-servers.zip

What this does is installs fabric tools, but as I said, its here already...


NON-OPTIONAL: To start the developer environment (not the actually ledger):

- cd ~/place_w_below_stuff
- ./downloadFabric.sh
- ./startFabric.sh
- ./createPeerAdminCard.sh

To end developer session (!important):

- cd ~/place_w_below_stuff
- ./stopFabric.sh
- ./teardownFabric.sh

#### Firing up the blockchain

Assuming there isnt something odd going on with GOPATH variables in ROOT (actually there is a lot that could go wrong) we should be able to start the blockchain now...

- composer runtime install --card PeerAdmin@hlfv1 --businessNetworkName zendomo

- composer network start --card PeerAdmin@hlfv1 --networkAdmin admin --networkAdminEnrollSecret adminpw --archiveFile zendomo@0.0.1.bna --file networkadmin.card

- composer card import --file networkadmin.card

- composer-rest-server
then: admin@zendomo, 
      never use namespaces, 
      No, 
      Yes, 
      No, 
 
Should be good to go now.

To restart zendomo:

- composer-rest-server -c admin@zendomo -n never -w true


# DISCLAIMER: THIS IS A COMPLEX PROCEDURE, CONTACT CBOYCE183 @ GITHUB WITH ANY QUESTIONS/ISSUES

### CONFIRM: Not deprecated as of 1/12/17.