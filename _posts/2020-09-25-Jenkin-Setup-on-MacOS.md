---
layout:     post
title:      Jenkin Setup on MacOS and Workflow
date:       2020-09-25
summary:    Record steps to setup Jenkin with JUnit, Gradle, Github and Jacoco 
categories: Java Jenkin JUnit Gradle Github
---

# Agile Tools Setup

## Initial Jenkins Configuration

1.  Go to `Jenkins > Manage Jenkins > Manage Plugins > Download`, and ensure the following plugins have been installed. *Notes: Jenkin requires to restart after adding new plugins.*

   - JUnit

      <img src='https://i.loli.net/2020/09/30/vhFxM9EKfe8auZH.png' alt='vhFxM9EKfe8auZH' style="width:50%"/>

   - Gradle

      <img src='https://i.loli.net/2020/09/30/kCf7blwAtRSTFgd.png' alt='kCf7blwAtRSTFgd' style="width:50%"/>

   - Github

      <img src='https://i.loli.net/2020/09/30/VGCaMH8NEe52oUz.png' alt='VGCaMH8NEe52oUz' style="width:50%"/>

   - Jacoco

      <img src='https://i.loli.net/2020/09/30/VGCaMH8NEe52oUz.png' alt='VGCaMH8NEe52oUz' style="width:50%"/>

2. Create a new project for `Currency Converter`. First go to `Jenkins > New Item`, write the project name at `Enter an iterm name` and select `Freestyle project`.

   <img src='https://i.loli.net/2020/09/30/RSOD8a9lkXyoiI1.png' alt='RSOD8a9lkXyoiI1' style="width:50%"/>

## Setup GitHub in Jenkins

1. Go to `Jenkins > Manage Jenkins > Configure System > GitHub Enterprise Servers`, write `https://github.sydney.edu.au/api/v3` at API Endpoint and set name to be `Github Sydney`.

   <img src='https://i.loli.net/2020/09/25/kxcrwBy1qiSaXtH.png' alt='kxcrwBy1qiSaXtH'/>

2. Go to `Currency Converter > Configure > Source Code Management` and select `Git`. Then add repository URL to `Repository URL` and set Credentials to one of group members.

   <img src='https://i.loli.net/2020/09/25/HXEIaKs1btfF3kQ.png' alt='HXEIaKs1btfF3kQ'/>

3. Go to `Currency Converter > Configure > Build Triggers` and select `Github hook trigger for GITScm polling.

   <img src='https://i.loli.net/2020/09/30/DWOIpLk1M57ZTzr.png' alt='DWOIpLk1M57ZTzr' style="width:50%"/>

## Setup Gradle in Jenkins

1.  Go to `Jenkins > Manage Jenkins > Global Tool Configuration > Gradle > Gradle Installation`. Then set gradle name with `gradle_build` and select `Gradle 6.7-rc-1` as Gradle.org Version.

   <img src='https://i.loli.net/2020/09/25/nhRTYzqfLpA1urW.png' alt='nhRTYzqfLpA1urW'/>

2. Go to `Currency Converter > Configure > Build > Add build step`, select `Invoke Gradle script`.

   <img src='https://i.loli.net/2020/09/30/R8A4StWlFxQfcaG.png' alt='R8A4StWlFxQfcaG' style="width:50%"/>

3. Then select `Invoke Gradle` with Gradle Version to be `gradle_build` and set `Tasks` to be `clean build test`.

   <img src='https://i.loli.net/2020/09/30/k3vAD6g9h1URcBH.png' alt='k3vAD6g9h1URcBH' style="width:50%"/>

## Setup JUnit in Jenkins

1. Go to `Currency Converter > Configure > Post-build Actions` and select `Publish JUnit test result report`.

   <img src='https://i.loli.net/2020/09/25/qEydhIY8gr6JHUS.png' alt='qEydhIY8gr6JHUS' style="width:50%"/>

2. Then set `**/test-results/**/*.xml` at `Test report XMLs`.

   <img src='https://i.loli.net/2020/09/30/1ELOifHtyD4plr8.png' alt='1ELOifHtyD4plr8'/>

## Setup Jacoco in Jenkins

1. Go to `Currency Converter > Configure > Post-build Actions` and select `Record JaCoCo coverage report`.

   <img src='https://i.loli.net/2020/09/25/grLqx4UbiAZsJly.png' alt='grLqx4UbiAZsJly' style="width:50%"/>


## Connect Webhook between Jenkins and Githubs

TODO: Add step to set up google webhook

1.

2.

1. Install ngrok using `brew cask install ngrok`. 

   <img src='https://i.loli.net/2020/09/30/R8A4StWlFxQfcaG.png' alt='R8A4StWlFxQfcaG' style="width:50%"/>
   
2. Login to your Ngrok account at [link](https://dashboard.ngrok.com/get-started/setup). Then type `ngrok authtoken ...` in terminal. 

3. Then type `ngrok http 8080` to get http

   <img src='https://i.loli.net/2020/09/25/IbBmqA2y9RYKcDr.png' alt='IbBmqA2y9RYKcDr'/>
   
4. Go to `Github > Settings > Hooks > Add webhook` and add this link at `Payload URL`, e.g. `https://<hostname>/github-webhook/`. Then select `application/json` as `Content Type`.

   <img src='https://i.loli.net/2020/09/25/5MbAuKTPgv4p2GV.png' alt='5MbAuKTPgv4p2GV'/>

# Workflow

1. After clone/pull the latest version of application, create a new a **branch** other than local **master** branch to make changes for new features or bug fixes.

   - Name convention
      - `feat-xxx` for new features
      - `fix-xxx` for bug fixes

   - Using `git checkout -b feat-testing` to create a `feat-testing` branch and checkout to this branch at the same time. `git switch master` could also be used to switch to other branches. 

      ![4gJKLn5UqFGdpBO](https://i.loli.net/2020/09/30/4gJKLn5UqFGdpBO.png)

2. Write your code in `feat-xxx` or `fix-xxx` branch **only** and test it **on local** if you completed a single feature. **DO NOT PUSH NOT WORKING APPLICATION**. If fails to build or test, fix it and test again.

3. If it passes local build or test and ready to push to remote repository, using `git pull origin master` to **get the latest version of project before pushing your own code** (your teammates may change it before you).

   - At first, git will try to merge for you, if might appears the following image. If it happens, first type `i` and write your comment below, then click `esc` and type `:wq`. 
     
      <img src='https://i.loli.net/2020/10/03/PbS1L8ImVE7ioJp.png' alt='PbS1L8ImVE7ioJp'/>
      
   - If git cannot automatically merge for you, it will list all the conflict file. 

      - The conflict files could be `(content)`, so that to resolve this conflict, the conflict content should be chosen between two version. 

         <img src='https://i.loli.net/2020/10/03/RAJyf82iEpF1Tlt.png' alt='RAJyf82iEpF1Tlt' style='width:70%'/>

         The content in conflict files: 

         <img src='https://i.loli.net/2020/10/03/BEPnde37zjMH2Ow.png' alt='BEPnde37zjMH2Ow' style="width:80%"/>
      
      - The conflict files could be `(modifiy/delete)`, this means you have add more files in local repository, so you need to nothing. 

         <img src='https://i.loli.net/2020/10/03/xgDs9Yz1Mo7jlA6.png' alt='xgDs9Yz1Mo7jlA6' style='width:70%'/>

4. Push the `feat-xxx` or `fix-xxx` branch to rempte repository with appropriate comments.
   ```
   git add xxx
   git commit -m "consice message"
   git push origin feat-xxx
   ```

   ![bzhJfO4wuvoYAr5](https://i.loli.net/2020/09/30/bzhJfO4wuvoYAr5.png)

5. Open a new pull request by clicking on `Compare & pull request` on Github's repository page on the top right corner. Write more details about what you have changed.

   ![zJikeRHTANL2OYf](https://i.loli.net/2020/09/30/zJikeRHTANL2OYf.png)
   ![QmTd5S3bRzHMsnJ](https://i.loli.net/2020/09/30/QmTd5S3bRzHMsnJ.png)

6. Then the code reviewer (your teammates) will review your code and determine whether merge into the master branch or not. If cannot merge into master, please write down some reasons about why cannot merge into the master branch.

   <img src='https://i.loli.net/2020/09/30/ps3QRDhNfJOKXTa.png' alt='' style="width:60%;"/>

7. After merging `feat-xxx` or `fix-xxx` branch to `master`branch, delete `feat-xxx` or `fix-xxx` branch on GitHub repository.

   <img src='https://i.loli.net/2020/09/30/ehUi5Rtgcs9dm64.png' alt='' style="width:60%;"/>

8. Meanwhile, Jenkin will automatically build and run unit test and coverage test for you.

   - A new commit is building in `build history`

      <img src='https://i.loli.net/2020/09/30/sD79dcwSPvLT4Ar.png' alt='' style="width:60%;"/>

   - Click on the that build, you will see commit message, commit id, JUnit test and Jacoco coverage test

      ![EXGvkQheW2PuBlj](https://i.loli.net/2020/09/30/EXGvkQheW2PuBlj.png)

9. At last, using `git pull  orign master` again and delete the `feat-xxx` or `fix-xxx` branch locally using `git branch -d feat-xxx`. 

   <img src='https://i.loli.net/2020/10/03/aoipLxsVlRQ5CtT.png' alt='aoipLxsVlRQ5CtT' style="width:80%"/>

   - Otherwise, you may encounter the following issue

      <img src='https://i.loli.net/2020/10/03/fGRNOkm7de6pjaI.png' alt='fGRNOkm7de6pjaI'/>

