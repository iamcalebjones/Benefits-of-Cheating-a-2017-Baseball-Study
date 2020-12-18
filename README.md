# Benefits of Cheating - a 2017 Baseball Study
### A look at how much, if at all, stealing pitch signs helped the 2017 Astros

<p align="center">
  <img src="https://github.com/iamcalebjones/Benefits-of-Cheating-a-2017-Baseball-Study/blob/main/plots_and_images/Screen%20Shot%202020-12-17%20at%209.48.13%20PM.png">
</p>


### Introduction

The 2017 baseball season was memorable for most everyone who pays attention to baseball. 
For fans of the Houston Astros, like myself, it was an incredible season, which ended with a World Series win. For fans of any other baseball team, the Houston Astros winning the 2017 World Series is almost fully discounted. And the reason for that is the subject of this project: the 2017 Houston Astros Sign Stealing Scandal.


### Background

In early November 2019, just days after the Astros lost the 2019 World Series to the Washington Nationals, Astros fans’ hearts were broken again with allegations that the Astros had cheated in 2017 by stealing pitch signs during games and feeding that information to their batters. The implications of this, if true, cast serious doubts about the legitimacy of their 2017 World Series win. 


### How It Was Done

As the news sank in, everyone wanted to know how they managed to do this. I mean, c’mon! In a stadium packed with fans game after game, how did they pull this off? Former players began to speak up about this and provided that information. 

But first, a little context. In baseball, every pitch consists of a pretty complicated sequence of events, the main part being the pitcher and catcher getting on the same page about what pitch to throw next. This is done with hand signals that the catcher gives to the pitcher, one finger for fastball, two fingers for curveball, etc., only the signs are much more complicated and the actual sign of the pitch is disguised in a sequence of signs designed to provide some security against anyone on the opposing team who might be watching. The pitcher can accept the catcher’s sign, or shake him off and ask for a different sign. Once they finally agree, the pitcher delivers the pitch.

<p align="center">
  <img src="https://github.com/iamcalebjones/Benefits-of-Cheating-a-2017-Baseball-Study/blob/main/plots_and_images/Screen%20Shot%202020-12-18%20at%202.09.43%20PM.png" width=1000>
  <pcaption>A runner on second base has a clear view of the catcher. If he has time to pick up the sign and communicate it to the batter before the pitch, this breaks no rules and is a legal way to steal signs.</pcaption>
</p>

Usually, the only time the signs are at risk of being picked up by the opponent is when the team who is batting has a runner on 2nd base (see image above), as this position on the field gives the base runner a clear view of the catcher’s signs. What the Astros did was have a camera installed in center field aimed at the catcher. The video was fed to the club house, where analysts were tasked with firstly deciphering the signs, then communicating the signs to a player in the dugout. This player then communicated the stolen sign to the batter via banging on a trash can. One bang for fastball, two bangs for curveball, etc. Yes, bangs on a trash can.

All this matters. Pitchers work hard at being able to deliver their pitches so that they appear the same to the batter when the ball leaves the hand, and only as the pitch makes its way towards the batter does the spin on the ball begin to influence how it flies. Batters work hard at being able to identify what the pitch is as early as possible so they know how to swing, when to swing, or if they should even swing at all. If the batter knows what the pitch will be before it is thrown, this gives him a serious advantage over the pitcher.


### Focus of This Study

Wanting to preserve the legitimacy of the World Series title, I had one main question: **Did knowing the signs actually improve the Astros abilities at the plate?** Baseball is just as much about the game as it is about the stats, and every season massive amounts of data and stats on each player and team are generated. If knowing the signs actually did benefit the Astros, surely this would be evident somewhere in the data.


### The Data

The fact that the signs were stolen via a camera installed in center field meant that only home games were involved in this scheme. Away games provided no ability to cheat in this manner, so right away only 81 of the 162 games in the 2017 season were candidates for the study. The main data source for the bangs came from http://signstealingscandal.com/. Tony Adams, a programmer and Astros fan, had rewatched all the home games for the season, generated a spectrogram for every pitch, which is a visual representation of an audio file, visually picked out the audio signature of the bangs in the spectrogram, and recorded the relevant info in a database. He did this for every pitch in 58 of the 81 home games, almost 8300 pitches, and the relevant information he collected for every one of these pitches included the following:

* Batter
* Opposing team
* Whether or not the pitch had bangs
* Inning, score at the time, and position of base runners if any
* Pitch type (fastball, curveball, etc.)
* The result of the plate appearance (hit, walk, strikeout, etc.)
* Did anyone score
* Some metadata about the audio adn video evidence used to generate the data

From here going forward, mentions of ‘bangs’ refers to a pitch that had the sign stolen and was communicated to the batter via the banging on the trash can, the bang. This is how the instance was referred to in the data compiled by Tony Adams above, and I carried the convention through my analysis as well. I did eventually start referring to pitches with no bangs as clean pitches, so that shows up in my analysis, bangs or clean pitches.

To support the bangs dataset, relevant batting statistics were needed. Nothing is more fundamental than batting average. The formula for batting average is the number of **hits** divided by the number of **at bats**. 

<p align="center">
  <img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/b1a9a962a9a544aa68480dfacb4a5d4f63ff92c0" alt="{\displaystyle AVG={\frac {H}{AB}}">
</p>

Sometimes a player comes up to bat and may get hit by a pitch, and be awarded a free pass to first base. This appearance does not count as an at bat, so there is a distinction made to catch all outcomes of stepping into the batter’s box: a **plate appearance** is just that, stepping up to bat. An **at bat** is a plate appearance that ends in either a hit or a strikeout. There are some other minor special cases for at bat classifications, but this working definition catches the most important cases.

