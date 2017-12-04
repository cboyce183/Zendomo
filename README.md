# Hello

## If you found your way here, congratulations, and welcome to hell.

### Here is a set of instructions for attempting to make this work locally for you.

#### Pre-reqs:
- Docker < v17.03
- Docker-compose < v1.8
- npm v5.x (nothing else)
- git < v2.9
- Python < v2.7

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
  docker kill $(docker ps -q)         //kills all open docker processes
  docker rm $(docker ps -aq)          //cleaning up...
  docker rmi $(docker images dev-* -q)  //cleaning up docker images...

- OPTIONAL: THIS REPO CONTAINS THESE THINGS, BUT FOR CLARITYS SAKE IL INCLUDE THE WHOLE PROCESS

mkdir ~/fabric-tools && cd ~/fabric-tools

curl -O https://raw.githubusercontent.com/hyperledger/composer-tools/master/packages/fabric-dev-servers/fabric-dev-servers.zip

unzip fabric-dev-servers.zip

What this does is installs fabric tools, but as I said, its here already...

- To start the developer environment (not the actually ledger):

cd ~/fabric-tools
./downloadFabric.sh
./startFabric.sh
./createPeerAdminCard.sh

- To end developer session (!important):

cd ~/fabric-tools
./stopFabric.sh
./teardownFabric.sh



#### Omitting how to make the blockchain, because I only have 8gb of ram.
#### Firing up the blockchain

Assuming there isnt something odd going on with GOPATH variables in ROOT (actually there is a lot that could go wrong) we should be able to start the blockchain now...

composer runtime install --card PeerAdmin@hlfv1 --businessNetworkName zendomo

composer network start --card PeerAdmin@hlfv1 --networkAdmin admin --networkAdminEnrollSecret adminpw --archiveFile zendomo@0.0.1.bna --file networkadmin.card

composer card import --file networkadmin.card

composer-rest-server
then: admin@zendomo
      never use namespaces
      No
      Yes
      No

Should be good to go now.

To restart zendomo:

composer-rest-server -c admin@zendomo -n never -w true


# DISCLAIMER: THE LIKELYHOOD OF SOME INSTRUCTION BEING MISSING IS PRETTY MUCH 100%, COME GET THE ADMIN IF SOMETHING GOES WRONG