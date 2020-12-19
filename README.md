# Benefits of Cheating - a 2017 Baseball Study
## A look at the competitive advantage the 2017 Astros received by stealing signs
#### by Caleb Jones
[LinkedIn](https://www.linkedin.com/in/calebsjones/) | [GitHub](https://github.com/iamcalebjones) | [Presentation Slides](https://docs.google.com/presentation/d/1EHvNUX0hRqJepVOc2ngxzcHWRqIDS_4hiC8plM3Wd6Y/edit?usp=sharing)


<p align="center">
  <img src="https://github.com/iamcalebjones/Benefits-of-Cheating-a-2017-Baseball-Study/blob/main/plots_and_images/Screen%20Shot%202020-12-17%20at%209.48.13%20PM.png">
</p>


## Introduction

The 2017 baseball season was memorable for most everyone who pays attention to baseball. 
For fans of the Houston Astros, like myself, it was an incredible season, which ended with a World Series win. For fans of any other baseball team, the Houston Astros winning the 2017 World Series is almost fully discounted. And the reason for that is the subject of this project: the 2017 Houston Astros Sign Stealing Scandal.


## Background

In early November 2019, just days after the Astros lost the 2019 World Series to the Washington Nationals, Astros fans’ hearts were broken again with allegations that the Astros had cheated in 2017 by stealing pitch signs during games and feeding that information to their batters. The implications of this, if true, cast serious doubts about the legitimacy of their 2017 World Series win. 

What is sign stealing? It’s a long-standing baseball practice in which one team tries to decode the signs of its opponent. It’s not illegal, but the way the Astros went about it was.


## How It Was Done

As the news sank in, everyone wanted to know how they managed to do this. I mean, c’mon! In a stadium packed with fans game after game, how did they pull this off? Former players began to speak up about this and provided that information. 

But first, a little context. In baseball, every pitch consists of a pretty complicated sequence of events, the main part being the pitcher and catcher getting on the same page about what pitch to throw next. This is done with hand signs that the catcher gives to the pitcher, one finger for fastball, two fingers for curveball, etc., only the signs are much more complicated and the actual sign of the desired pitch is disguised in a sequence of signs designed to provide some security against anyone on the opposing team who might be watching. The pitcher can accept the catcher’s sign, or shake him off and ask for a different sign. Once they finally agree, the pitcher delivers the pitch.

<p align="center">
  <img src="https://github.com/iamcalebjones/Benefits-of-Cheating-a-2017-Baseball-Study/blob/main/plots_and_images/Screen%20Shot%202020-12-18%20at%202.08.53%20PM.png" width=1000>
  <pcaption>A runner on second base has a clear view of the catcher. If he has time to pick up the sign and communicate it to the batter before the pitch, this breaks no rules and is a legal way to steal signs.</pcaption>
</p>

Usually, the only time the signs are at risk of being picked up by the opponent is when the team who is batting has a runner on 2nd base (see image above), as this position on the field gives the base runner a clear view of the catcher’s signs. What the Astros did was have a camera installed in center field aimed at the catcher. The video was fed to the club house, where analysts were tasked with firstly deciphering the signs, then communicating the signs to a player in the dugout. This player then communicated the stolen sign to the batter via banging on a trash can. One bang for fastball, two bangs for curveball, etc. Yes, bangs on a trash can.

All this matters. Pitchers work hard at being able to deliver their pitches so that they appear the same to the batter when the ball leaves the hand, and only as the pitch makes its way towards the batter does the spin on the ball begin to influence how it flies. Batters work hard at being able to identify what the pitch is as early as possible so they know how to swing, when to swing, or if they should even swing at all. If the batter knows what the pitch will be before it is thrown, this gives him a serious advantage over the pitcher and could increase his ability to make contact and get on base.


## Focus of This Study

Wanting to preserve the legitimacy of the World Series title, I had one main question: **Did knowing the signs actually improve the Astros abilities at the plate?** Baseball is just as much about the game as it is about the stats, and every season massive amounts of data and stats on each player and team are generated. If knowing the signs actually did benefit the Astros, surely this would be evident somewhere in the data.


## The Data

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

Sometimes a player comes up to bat and may get hit by a pitch, for which he is awarded a free pass to first base. This appearance does not count as an at bat, so there is a distinction made to catch all outcomes of stepping into the batter’s box: a **plate appearance** is just that, stepping up to bat. An **at bat** is a plate appearance that ends in either a hit or a strikeout. There are some other minor special cases for at bat classifications, but this working definition catches the most important cases.

Initially I wanted to find batting average stats updated per at bat for each player, but I didn’t find this information out there. There is plenty of raw data available to calculate this on my own, but I was pretty sure this would have taken most of my available time so I kept looking for the next best thing, batting average updated per game. I did find this data, at the granddaddy of all baseball records, https://www.retrosheet.org/. 

<p align="center">
  <img src="https://github.com/iamcalebjones/Benefits-of-Cheating-a-2017-Baseball-Study/blob/main/plots_and_images/Screen%20Shot%202020-12-18%20at%204.12.13%20PM.png" width=1000>
  <caption>Example of a web page scraped for constructing career batting average tables for each player.</caption>
</p>

This is a historical collection of nearly every stat and every game for almost all of baseball history. I was able to scrape the batting average data from the website and construct career batting average tables for each player on the team, which I then plotted as a part of the data analysis. 

## Analysis and Results
Of the 20 batters represented in the bangs database, I chose to focus on batters who saw at least 300 pitches, 15% or more of which were bangs. This narrowed the list of batters to include down to 7 batters. 

The main parts of my analysis included developing a new baseball statistic, which I called Runs per 100 At Bats, or RABs for short. This stat is simply the number of runs batted in divided by the number of at bats, multiplied by 100 for the sake of being more logical. It makes much more sense to report that a batter generates 8.6 runs per 100 at bats than it does to say that a batter generates 0.086 runs per at bat. Those stats were calculated for each of the batters I focused on and are presented in the table below.

|                |Pitches with Bangs|Total Pitches|Bangs Percent|Bang AB Runs Generated|Bang Runs per 100 AB (RAB)|Clean AB Runs Generated|Clean Runs per 100 AB (RAB)|
| -------------- |:----------------:|:-----------:|:-----------:|:--------------------:|:------------------:|:---------------------:|:-------------------:|
|Alex Bregman    |133               |800          |16.62        |7                     |**_8.6_**           |13                     |6.3                  |
|Carlos Beltran  |138               |762          |18.11        |0                     |0                   |10                     |5.4                  |
|Carlos Correa   |97                |594          |16.33        |3                     |6.1                 |13                     |9.3                  |
|Evan Gattis     |71                |427          |16.63        |1                     |2.8                 |9                      |7.9                  |
|George Springer |139               |933          |14.90        |0                     |0                   |22                     |10.0                 |
|Jake Marisnick  |83                |364          |22.80        |4                     |**_10.0_**          |8                      |9.1                  |
|Jose Altuve     |24                |866          |2.77         |2                     |**_9.1_**           |19                     |8                    |
|Marwin Gonzalez |147               |776          |18.94        |2                     |2.9                 |18                     |10.1                 |
|Yuli Gurriel    |120               |670          |17.91        |5                     |7.4                 |16                     |8.4                  |

Looking at the two RAB data columns, most of the batters performed better on clean pitches than on pitches with bangs; however, a few players that have a higher RAB on bangs than on clean pitches. For Alex Bregman and Jake Marisnick, I believe the bangs actually helped them, which will become more evident in the upcoming plots. For Jose Altuve, the sample size is not enough to satisfactorily conclude that the bangs gave him a competitive advantage. It would be like flipping the first two coins heads up and then concluding that this is a 100% heads coin. There simply is not a large enough sample size for fair data to be represented. This is supported further by the fact that only 2.77% of the pitches he saw in the dataset were bangs. Bregman's 133 of 800 pitches being bangs lends more support to the bangs RAB being higher than the clean RAB being evidence of an actual advantage. 

The next step of the analysis was to plot the batting average of the players with indicators when games with bangs happened for a visual representation of the benefit received by knowing the pitches beforehand. Year after year, the baseball season runs from April through September, so it was easiest to display multiple years' data by overlaying the data by dates. In the plots below, the vertical lines are games that contained pitches with bangs for that batter. If the average increases on those games, this suggests the player gained a competitive advantage by knowing the signs. If the average remained unchanged or decreased, this suggests that either there was no effect in the batter's performance, or knowing actually hurt his chances of getting a hit.

<p align="center">
  <img src="https://github.com/iamcalebjones/Benefits-of-Cheating-a-2017-Baseball-Study/blob/main/plots_and_images/Alex%20Bregman_career_batting_averages_stolen_signs.png">
</p>

Alex Bregman was a rookie in 2016, so there is limited data to illustrate his career seasonal batting averages. However, for the 2017 season, the occurrences of bangs correlates with an increase in his batting average from about mid-July through September, supporting the idea that the bangs gave him a competitive advantage.

<p align="center">
  <img src="https://github.com/iamcalebjones/Benefits-of-Cheating-a-2017-Baseball-Study/blob/main/plots_and_images/Jake%20Marisnick_career_batting_averages_stolen_signs.png">
</p>

The results are mixed when looking at Jake Marisnick's career batting averages (but first, a note on his 2014 season: he was traded at the end of July and the datasets were constructed for each team a batter played on, so this is why he has two datasets for the one season and why the orange trendline for the first half of the season remains unchanged for the rest of the season after late July). Looking at his 2017 season however, there are instances of the bangs both benefitting and hurting his batting abilities based on the response of the batting average. So it is a little more difficult to say whether or not the bangs gave him a clear competitive advantage.

<p align="center">
  <img src="https://github.com/iamcalebjones/Benefits-of-Cheating-a-2017-Baseball-Study/blob/main/plots_and_images/Jose%20Altuve_career_batting_averages_stolen_signs.png">
</p>

I included this plot for Jose Altuve to illustrate the kind of trends that can be seen in baseball data. Altuve usually has a strong opening week, hitting .400 or .500 over the first half dozen games or so, followed by a few weeks of slumping down below .200. Then he digs himself out, finds his groove and usually puts up an impressive season batting well over .300. As mentioned earlier, Altuve only received stolen signs on 24 of 866 pitches in the dataset, which were spread out across 19 home games through the season.
