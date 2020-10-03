---
layout:     post
title:      Jenkin Setup on MacOS
date:       2020-09-25
summary:    Record steps to setup Jenkin with JUnit, Gradle, Github and Jacoco 
categories: Java Jenkin JUnit Gradle
---

# Initial Jenkins Configuration 

## Install plugins

Jenkins > Manage Jenkins > Manage Plugins > Download 

-   JUnit
-   Gradle
-   Github
-   Jacoco

Might need to restart Jenkin after adding new plugins

## Add Gradle to global tool 

Jenkins > Manage Jenkins > Global Tool Configuration > Gradle > Gradle Installation > Add Gradle x.x. e.g

<img src='https://i.loli.net/2020/09/25/nhRTYzqfLpA1urW.png' alt='nhRTYzqfLpA1urW'/>

## Connect Github with Jenkins 

Jenkins > Manage Jenkins > Configure System > GitHub Enterprise Servers > API Endpoint > Set to https://github.sydney.edu.au/api/v3

<img src='https://i.loli.net/2020/09/25/kxcrwBy1qiSaXtH.png' alt='kxcrwBy1qiSaXtH'/>

# Create a New Project 

Jenkins > New Item > Enter an iterm name > Freestyle project > Configue > Source Code Management > Git

<img src='https://i.loli.net/2020/09/25/HXEIaKs1btfF3kQ.png' alt='HXEIaKs1btfF3kQ' style="width:20%;"/>

<img src='https://i.loli.net/2020/09/25/hYfEMoxzSRNOjc7.png' alt='hYfEMoxzSRNOjc7'/>

<img src='https://i.loli.net/2020/09/25/I9RaKSNgkYD6bAx.png' alt='I9RaKSNgkYD6bAx'/>

<img src='https://i.loli.net/2020/09/25/AlhWZnxISd826jL.png' alt='AlhWZnxISd826jL'/>

<img src='https://i.loli.net/2020/09/25/cB8XbtyoLwTepY9.png' alt='cB8XbtyoLwTepY9'/>

<img src='https://i.loli.net/2020/09/25/qEydhIY8gr6JHUS.png' alt='qEydhIY8gr6JHUS'/>

<img src='https://i.loli.net/2020/09/25/grLqx4UbiAZsJly.png' alt='grLqx4UbiAZsJly'/>

**Note: **add `**/test-results/**/*.xml` to JUnit settings

<img src='https://i.loli.net/2020/09/25/lS85Bwra4xvQngU.png' alt='lS85Bwra4xvQngU'/>

# Connect Ngrok with Jenkins

Install ngrok using `brew cask install ngrok`. 

Login to your Ngrok account at [link](https://dashboard.ngrok.com/get-started/setup). Then type `ngrok authtoken ...` in terminal. 

<img src='https://i.loli.net/2020/09/25/n3erGE548DLzU7w.png' alt='n3erGE548DLzU7w'/>

Then type `ngrok http 8080` to get http

<img src='https://i.loli.net/2020/09/25/IbBmqA2y9RYKcDr.png' alt='IbBmqA2y9RYKcDr'/>

Add this link to Github > Settings > Hooks > Add webhook e.g. `https://<hostname>/github-webhook/`

<img src='https://i.loli.net/2020/09/25/5MbAuKTPgv4p2GV.png' alt='5MbAuKTPgv4p2GV'/>



