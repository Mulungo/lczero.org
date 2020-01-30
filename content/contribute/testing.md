---
title: "Testing"
weight: 300
draft: true
---

(Describe how to run tests in cutechess/arena/etc, how to report results, how to
run Ordo, maybe also how to stream the process)

**Using Cutechess**

Leela depends on its community to contribute towards game generation, and to test the networks it develops along its path. 
This guide is meant to help those new to Cutechess on how to test Leela on Windows. 
This guide assumes you have downloaded Leela and one or more networks to test, if you have not - https://newsite.lczero.org/play/quickstart/

1.	Downloading Cutechess
https://github.com/cutechess/cutechess/releases - Download and install Cutechess through its official releases page on Github. 
1.1.	Launch Cutechess, click on TOOLS and then SETTINGS.
1.2.	Change to the ENGINES Tab and click on the PLUS button on the bottom right.
1.3.	Click on the BROWSE button on the command and then browse to the location where you have the Leela chess Engine, or any other engine you wish to install. 
1.4.	Select lc0.exe and click OPEN. 
1.5.	Change the name from lc0 to your desired name. Usually, we name engines within certain directions to simplify when compiling the PGN’s and to make it easier to read and search. Therefore, Leela running with the network 42850 would be named “lc0.net.42850” and Leela running with the network 61500 would be named “lc0.net.61500”.
1.6.	Under command, after lc0.exe you should add your weights options. You do this by adding the command –weights=NETWORKNAME which if your network is 42850, it should be added as –weights=42850.
1.7.	Click on the ADVANCED tab and this is where you can change the engine parameters. If you have added the weights command successfully, you should see the weights file value as 42850 or whichever you chose. (Please note that it helps to name the network files according to their short names and to place them on the same folder as the engine).
1.8.	If you have an RTX or superior card, it is better to change the backend to cudnn-fp16. If you are using only one graphics card, it is recommended to use one thread.
1.9.	The rest of the options it is up to you, if you want LogitQ enabled, or to change the CPuct parameters, as well as adding tablebases for the engine to use. Remember that whatever change you make, if you are to post the results on our Discord channel, you have to document them. 
1.10.	Once you are done selecting the parameters, click on OK and you can restart the process for other engines or networks that you would like to test. 
1.11.	Once you have more than one engine/network added. It is time to start a tournament. 

**Starting a Tournament**

1.	Click on the Tournament Tab and select New.
2.	Fill in the tournament name and select a location to save the PGN output. 
3.	Select the tournament type – Round Robin if you want all vs all, or Gauntlet if you want all vs one. In Gauntlet, the first player added is the gauntlet player. 
4.	On the Rounds tab, it is recommended to select 2 games per encounter, so that each player plays two games vs the other on both sides (Black and White). 
5.	As for the number of rounds, the higher the better, whatever serves your purpose. Too low, means the sampling size is too small, therefore the results are not trustworthy, and too high, requires a long time for the tournament to complete. An average sample depends on time controls, try to see what other testers have done. 
6.	Tick Play each opening twice, so that the engines repeat the opening as black and white. 
7.	Opening Suite – It is recommended to have a strong opening suite with enough variety to avoid having repeated games. If you are to make a tournament of total 2000 games, an ideal opening book would have 1000 openings, that way each engine plays each opening on both sides. Chad has compiled some good opening suites of different sizes. Ask on Discord.
8.	Add the players and click OK to start the tournament. 

Tip: If you stop and start a new tournament with the same PGN, it is possible that the games will be added instead of replaced to the file. Therefore, it would add noise. So always remember to delete the old canceled PGN tournament file, or to create a new one. 

**Using ORDO**

Once the tournament is over it is time to run a high accuracy ORDO on the tournament PGN and then post the results. 
1.	Download and extract Ordo for Windows - https://github.com/michiguel/Ordo/releases/tag/v1.2.6
2.	Once it is extracted, click on SHIFT on your keyboard, and RIGHT Click on your mouse inside ORDO’s empty part of the window folder so you have access to PowerShell. Click on Open PowerShell window here. 
3.	Then, you can run Ordo using multiple commands, whichever you prefer, and be sure to read the manual on the project’s Github page to understand the options better.
3.1.	A high accuracy test would look like this:  .\ordo-win64.exe -a 0 -A "NAMEOFNETWORKANCHORINBRACKETS" -D -W -q -J -U "0,1,2,3,4,5,6,7,8,9,10" -s 500 -n 1 PGN_PATH.pgn
3.2.	 The network anchor depends on the test that you are running. For example, if you are testing42850 vs the latest two T60. The anchor network could be lc0.net.42850. 

How do I post the results?
In order to post the results, you need two things:
1.	A template.
2.	The games PGN.

Template:
**Match:** Match Name
**LC0-version:** Whichever version you are using
**LC0 options:** All the parameters changed
**Time control:** Time Control Used
**Hardware:** Graphics Card(s) and CPU
**Speed:** Benchmark of nets used. See - https://newsite.lczero.org/dev/wiki/running-a-benchmark/
**Book:** Opening Book
**Tablebases:** For which engines, only for adjudication, or not at all?
**Adjudication:** Options used.
**Software:** cutechess-gui
**Comments:** 
Tip: In order to use BOLD for a word, we use ** word(s) go(es) here with two stars on each side of the word(s) ** .

Please note the three backticks below in order to place the ORDO results inside a table. - You need three backticks before and after the table. (``` ```)
After filling the template with **all** the information. It is time to add the PGN to the results. You might have to upload a compressed file (7zip, Winrar, Winzip) as depending on the PGN size, Discord might not accept a big file. 

And there you go. You have helped the community by testing. It is helpful to check what other testers are doing and see if the developers have asked for any specific testing to be done in order to make the tests more relevant. 
Thank you for your interest in testing Leela, if you have any doubts not mentioned in this short guide, please contact our Discord #help channel or #test-discuss. 

Example table of an Ordo run posted to Discord together with the template above: 

```
   # PLAYER                    :  RATING  ERROR  POINTS  PLAYED   (%)  CFS(%)    W     D    L  D(%)
   1 lc0.net.58613-bonus       :     0.0   ----   850.5    1500    57      98  408   885  207    59
   2 lc0.net.58613-tuned.LQ    :   -16.8   15.8   816.0    1500    54     100  369   894  237    60
   3 stockfish.dev             :   -48.5   11.4  1333.5    3000    44     ---  444  1779  777    59

White advantage = 57.46 +/- 4.16
Draw rate (equal opponents) = 62.40 % +/- 0.92```

