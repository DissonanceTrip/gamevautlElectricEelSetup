# NOTE: This is a community guide made by someone that just really likes GameVault. THIS IS NOT OFFICIAL DOCUMENTATION. USE AT YOUR OWN RISK.

## INTRO
If you have absolutely no idea what you are doing with TrueNAS Scale, this is the guide for you.
This guide is a VERY detailed step-by-step guide to getting TrueNAS Scale set up and GameVault installed.

If you are familiar with storage/user management in TrueNAS Scale, use the other guide. If not, follow along!

## Prerequisits

- You need to know how to install an OS on a system. This guide will not cover how to do this.
- That is pretty much it...you just need to install TrueNAS Scale yourself then this guide will walk you through everything else!
- Stay cool - your games will be with you soon

## Step 1: Install TrueNAS Scale and get the initial setup complete
You gotta do this on your own. I believe in you <3

## Step 2: Setting up your storage
ZFS Pools
Datasets
Directories within datasets


## Step 3: Understanding ACLs and ensuring that your data is accessible

## Step 3.5: Making new users and ensuring they have access to stuff via groups or directly

## Step 4: Get your games on the server
SMB Share setup
setting user access and permissions
Accessing your share from another system

Discussion about game naming conventions and syntax per the main documentation goes here

Put your games into the server

## Step 5: Reading documentation and building your docker-compose file
ALL the docker-compose stuff goes here with more detailed explainations of everything.

## Step 6: How does this whole "Docker" thing work?
What is Docker?
How does it work?
Why is it being used?
AHHHHHHH

## Step 7: How to get GameVault running in Docker on TrueNAS Scale (v24.10 or newer)
Copy paste the main guide and add more detail here
admin user
user gamevault runs as
API key setup for whatnot and all that jazz

## Step 8: Testing access and functionality
Test web interface
Download client - walk through setup
check that games are found and info is grabbed as needed

## Step 9: Administration of GameVault
adjusting game metadata as needed
approving new users if that setting is set and whatnot
other settings and jazz

## Step 10: What about making everything publically accessible?
I do not accept ANY liability for you doing this. You do this at your own risk.

YOU DO THIS AT YOUR OWN RISK OKAY? Yes? Ok.

## Step 11: Understanding your local network
oof this part is gonna suck to write

## Step 12: Understanding how people on the Internet can talk to things on your local network
this part is gonna suck less to write but still a lot

## Step 13: Why you SHOULD NOT DO THIS
If you are reading this guide, you are not a systems/network admin and you also probably don't have a background in cybersecurity....probably.
So, while I can tell you how to do this, and explain the dangers, you may still not fully understand exactly HOW it all works.
This means that if you make a mistake, or something isn't configured right, it may all work but might not be properly secure.
Please, take the time to learn about the basics of network security, exposing things to the internet, DNS security, etc. 
There are plenty of excellent Youtube channels that talk about all of this stuff.
~~ LINKS TO GOOD CHANNELS HERE  ~~

## Setting up DNS/nginx proxy manager (link to youtube video for it cause I dont wanna write that much lol)

## Testing that jazz

## discussion about docker networking

## Local access vs internet access (give yourself the fastest path)

## More stuff goes here

# DONE!!!!
