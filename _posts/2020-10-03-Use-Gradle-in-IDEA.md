---
layout:     post
title:      Use Gradle in IDEA
date:       2020-10-03
summary:    Steps to configure gradle in IDEA 
categories: Java gradle IDEA
---

1.  Click on `Open or Import` on the starting page of IDEA. 

<img src='https://i.loli.net/2020/10/03/aiYEcqKIoNyl7VG.png' alt='aiYEcqKIoNyl7VG'/>

2.  Open select `build.gradle` file of specific project. 

    <img src='https://i.loli.net/2020/10/03/s28UwJFNOR5intV.png' alt='s28UwJFNOR5intV'/>

3.  Click on `OPEN AS PROJECT`

    <img src='https://i.loli.net/2020/10/03/np9GwLfclvWZCFR.png' alt='np9GwLfclvWZCFR'/>

4.  Wait for IDEA to load, then click on `Edit Congigurations` on top left. 

    <img src='https://i.loli.net/2020/10/03/SDvQChFqe9T35uM.png' alt='SDvQChFqe9T35uM'/>

5.  Add the following three configurations

    <img src='https://i.loli.net/2020/10/03/sYEdKybDR5nUtVh.png' alt='sYEdKybDR5nUtVh'/>

    <img src='https://i.loli.net/2020/10/03/BUrZypLc2938hOJ.png' alt='BUrZypLc2938hOJ'/>

    <img src='https://i.loli.net/2020/10/03/mGcZUq8AJChYa5f.png' alt='mGcZUq8AJChYa5f'/>

6.  Go to `File > Project Structure > Plateform Settings `, set `JDK home path` end with home.  

    <img src='https://i.loli.net/2020/10/03/g7IhyvfEji624x8.png' alt='g7IhyvfEji624x8'/>

    As shown in the diagram below, it could directly access the `bin` folder. 

    <img src='https://i.loli.net/2020/10/03/hK1lsyL4JIdojGc.png' alt='hK1lsyL4JIdojGc'/>

7.  Go to `IntelliJ IDEA > Preference > Build, Execution, Deployment > Build Tools > Gradle`

    -   select `'wrapper' task in Gradle build script` in  `Use Gradle from` 
    -   set `Gradle JVM` to the **SAME VERSION** with `JDK home path` in `Project Structure` (which is the previous step) 

    <img src='https://i.loli.net/2020/10/03/YmOXP6F7r3ikwbQ.png' alt='YmOXP6F7r3ikwbQ'/>

🎉🎉🎉 Finish Setup Gradle in IDEA

# Build in IDEA

1.  General build

    Select one of build configurations, and click on `play` buttom beside. 

    <img src='https://i.loli.net/2020/10/03/iChfo47mLHSw3As.png' alt='iChfo47mLHSw3As'/>

2.  Terminal build 

    IDEA inbuild terminal is located at bottom left, then type `gradle build`, then `gradle run` or `gradle test`. 

    <img src='https://i.loli.net/2020/10/03/UVpBlxd61DgQXcH.png' alt='UVpBlxd61DgQXcH'/>

3.  Force build 

    Click on `Gradle` on top right, then click on `reload` buttom. (Not recommand) 

    <img src='https://i.loli.net/2020/10/03/Eomzh3Zy1KOl2MU.png' alt='Eomzh3Zy1KOl2MU'/>

