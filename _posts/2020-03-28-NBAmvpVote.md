---
title: NBA voting
date: {}
permalink: /2020/03/28/NBAmvpVote
tags:
  - NBA
  - R
  - MVP voting
published: true
---
# Why don't we have "Individual Game Voting" (IGV) for the NBA MVP?

Why do we do this to ourselves every year? The NBA plays for several months, 82 games for each team, and after All Star break comes and goes, everyone starts discussions about who will win the end of season awards. This inevitably leads to the *narrative* playing out. This year is no different. Giannis Antetokounmpo has been the best player for the whole year, everyone (humans and statistics) has agreed on this point up until a few weeks ago when, perhaps bored with same story for too many months, LeBron was touted as a competitor. Then on every talk show and podcast, media members start discussing the possibility. The league having to suspend/postpone due to the global pandemic put a dampener on these discussions to some degree, but if the season had continued momentum would have only grown.

## Does the media get caught up in their own narrative?
The MVP is voted on by 100 independent media members. Do they watch every game? Unlikely. Some may, but who could ever expect someone to properly absorb 1230 games a season, and remember in April who the best player was in early December? Normally the race comes down to one or two players in the upper tier, maybe three players in a competitive year. When the narrative comes along, these names circulate through the media, people argue on talk shows, and they poll each other to see who is voting for who. Suddenly everyone forgets what happened in November, December, and January, and it's 'what have you done for me lately?' Does a player take November off, but excel in April? Or blitz three months but miss the last 3 weeks of the season? Good chance the former isn't going to be penalised as much as the latter. Humans are prone to recency bias, it's a known fact, and yet we leave voting on the league's top individual award until the end of the year. It seems mad.

## Individual Game Voting (IGV) in the NBA
So it leads me to the obvious question, why doesn't a multibillion dollar sports league like the NBA vote on every game? I grew up following the Australian Football League (no...not rugby), and after every game the three umpires (equivalent to a referee) award 3-2-1 votes for the 'best and fairest' player of the game. These votes are secret, and the results are announced at an end of year event the week before the equivalent of the Championship game (called the 'Grand Final'). Now whether it is referees, or independent parties watching each game as it happens, surely this would provide a better proxy of who played the best in each game, across an entire season. Rather than who plays in a big market or is more frequently on National television?

## 2019 - 2020 season laid bare
Because I'm a nerd, I wanted to work out a way to simulate this process for the 2019-2020 season. I don't have the time to watch every game and vote, so the process will rely on data. There are obvious flaws in only using data, but the best I can do with the time that I have. I settled on applying a modified version of WinScore to every game, and allocating votes 5 - 1 to the top 5 players based on this metric. Just for comparison, the current end of year MVP vote is 10 for first, then 7, 5, 3, 1.

Standard Winscore uses this formula:
```
Win Score Formula = Points +
                    Rebounds +
                    Steals +
                    0.5 x Assists +
                    0.5 x Blocked Shots -
                    Field Goal Attempts -
                    Turnovers -
                    0.5 x Free Throw Attempts -
                    0.5 x Personal Fouls
```
Now, my changes were to halve the value of defensive rebounds, keep offensive rebounds at '1', increase the value of assists and blocked shots, and remove the penalty for free throws. Because I wanted to favour winning, and not stat padding, I added plus/minus to the result (therefore, subtracting score from a player with a negative plus/minus). This doesn't strictly favour winning, but does favour a players team being better when they're on the floor (yes, I'm aware +/- has it's own flaws).

My modified Winscore for IGV
```
Modified Win Score Formula =  Points +
                              Assists +
                              Steals +
                              Rebounds +
                              Blocked Shots +
                              Offensive Rebounds +
                              0.5 x Defensive Rebounds -
                              Field Goal Attempts -
                              Turnovers -
                              0.5 x Personal Fouls +
                              Plus/Minus
```

## Pros and Cons
Whilst IGV isn't a perfect system, it covers the basics. What it misses are those intangible things you can't measure with statistics. If ever implemented, an individual voting on a game would capture these things. In theory I could have worked out a few different metrics, for example one that values scoring more, and 'simulated' multiple voters, but that's more work than I'm cut out for. The big benefit of this simulation is that it captures all players, from all teams, regardless of marketsize or media attention. In a similar way it may be considered a drawback that someone scoring a 40 point triple double could get 5 votes, whilst in another game a player with 20 points and a good plus/minus could also get 5 votes. The aim is to award consistency of performance over the course of the year, so my theory would be that the player with highest cumulative Modified Win Score for the year will also take out the top prize.

## The Results
I must admit that I was somewhat surprised by the IGV results. LeBron was indeed on his way to catching Giannis looking at the game tracking (Figure below), particularly if injury meant Giannis would miss some of the upcoming games. Maybe the media narrative wasn't so bias afterall? Though I think the media was focussing on "have we been sleeping on LeBron", moreso than "if LeBron plays 10 more games than Giannis he should win". Really the latter is what is supported by the IGV projection, rather than votes per game played. On average LeBron was polling ~3.5 votes per game (v/gm), so he would have needed 5 games to catch up to Giannis (who was polling an exceptional ~3.9 v/gm!). A season long plot and final tally of the top 15 vote getters is below, with [Basketball Reference's MVP prediction model](https://www.basketball-reference.com/friv/mvp.html) and [Sekou Smith's NBA.com MVP ladder](https://www.nba.com/article/2020/03/06/kia-mvp-ladder-march-6-edition?collection=mvp-ladder) for comparison.

![Plot of NBA voting simulation 2020]({{site.baseurl}}/images/NBAvotes-plot.jpeg)
*__Figure 1.__ Cumulative totals of NBA votes per game throughout the 2019-2020 season. Lines are coloured based on end of season team using the R package "[teamcolors](https://github.com/beanumber/teamcolors)"*

*__Table 1.__ Top 15 players based on votes recieved per game, compared to rankings from Basketball Reference and NBA.com. Numbers in brackets are vote ranking for players outside top 15*

|Votes|Player|Cumulative Winscore|Basketball Ref|Change|NBA.com|Change|
|:-:|:---------------------|:---------:|---------------------:|:-:|---------------------:|:-:|
|   204|Giannis Antetokounmpo |     1722|Giannis Antetokounmpo | -       |Giannis Antetokounmpo | -       |
|   191|LeBron James          |     1527|LeBron James          | -       |LeBron James          | -       |
|   156|Rudy Gobert           |     1219|James Harden          | +2      |Luka Doncic           | +3      |
|   150|Nikola Jokic          |     1119|Anthony Davis         | +5      |Kawhi Leonard         | +3      |
|   147|James Harden          |     1350|Luka Doncic           | +1      |James Harden          | -      |
|   143|Luka Doncic           |     1200|Kawhi Leonard         | +1      |Anthony Davis         | +3      |
|   140|Kawhi Leonard         |     1133|Nikola Jokic          | -3      |Jayson Tatum          | +4      |
|   139|Bam Adebayo           |     1172|Khris Middleton       | +8 (16) |Nikola Jokic          | -4      |
|   138|Anthony Davis         |     1135|Kyle Lowry            | +17 (26)|Jimmy Butler          | +1      |
|   130|Jimmy Butler          |     1026|Jimmy Butler          | -       |Russell Westbrook     | +13 (23)|
|   125|Jayson Tatum          |      1000|                      |         |                      |         |
|   123|Chris Paul            |      937|                      |         |                      |         |
|   121|Domantas Sabonis      |     1010|                      |         |                      |         |
|   118|Damian Lillard        |     1001|                      |         |                      |         |
|   118|Trae Young            |      875|                      |         |                      |         |


Perhaps unsurprisingly, it wasn't close after The Greek Freak and the King. What was surprising was that third place was the Utah Jazz's Rudy Gobert, followed by Nikola Jokic and James Harden. I wondered if rebounds may have played a role in this; removing them as a valued statistic chucks most of the big men from the top 10 besides Giannis and Anthony Davis; halving the value of offensive rebounds doesn't do much more than move Harden up the rankings. So I guess whether you put stock in the metric used to simulate voting somewhat comes down to how much you care about rebounds. Even when they're only considered at half value they clearly play a role in this ranking system.

There are a lot of other takeaways you can get from both the IGV, and the comparison rankings. For example, Denver's Nikola Jokic was criticised early on in the season for his fitness and play, but he made a consistent enough contribution to Denver's winning season that the November slump didn't drop him out of the top 5. Similarly, both the model of human voting (Basketball Reference) and the human (NBA.com) valued players in big markets, recent successes (e.g. Westbrook), and players in top 3 teams (Lowry, Middleton, Davis) compared to the simulated IGV.

## 2020 IGV leaders by team
We can also look at the 'best' player per team. The IGV predominately favours winning teams, with Trae Young and Damian Lillard being the obvious standouts in regards to having over 100 IGV despite their teams having a losing record. The very worst 'best players' belonged to Minnesota (Karl-Anthony Towns, 54), Chicago (Zach LaVine, 55), and Golden State (Andrew Wiggins, 56). If we only look at players on Golden State who were their before and after the trade deadline, Eric Paschall and Draymond Green come out on top with 35 votes each (Alec Burkes, traded at the deadline, would have been the leader otherwise with 41 end of year IGVs).

*__Table 2.__ Top player per team for the 2019-2020 NBA season based on votes recieved per game*

|Team                   |Player                | Votes |
|:----------------------|:---------------------|:-----:|
|Atlanta Hawks          |Trae Young            |  118  |
|Boston Celtics         |Jayson Tatum          |  125  |
|Brooklyn Nets          |Jarrett Allen         |  98   |
|Charlotte Hornets      |Devonte' Graham       |  71   |
|Chicago Bulls          |Zach LaVine           |  55   |
|Cleveland Cavaliers    |Andre Drummond        |  75   |
|Dallas Mavericks       |Luka Doncic           |  143  |
|Denver Nuggets         |Nikola Jokic          |  150  |
|Detroit Pistons        |Andre Drummond        |  70   |
|Golden State Warriors  |Andrew Wiggins        |  56   |
|Houston Rockets        |James Harden          |  147  |
|Indiana Pacers         |Domantas Sabonis      |  121  |
|LA Clippers            |Kawhi Leonard         |  140  |
|Los Angeles Lakers     |LeBron James          |  191  |
|Memphis Grizzlies      |Jonas Valanciunas     |  88   |
|Miami Heat             |Bam Adebayo           |  139  |
|Milwaukee Bucks        |Giannis Antetokounmpo |  204  |
|Minnesota Timberwolves |Karl-Anthony Towns    |  54   |
|New Orleans Pelicans   |Brandon Ingram        |  82   |
|New York Knicks        |Julius Randle         |  70   |
|Oklahoma City Thunder  |Chris Paul            |  123  |
|Orlando Magic          |Nikola Vucevic        |  74   |
|Philadelphia 76ers     |Ben Simmons           |  106  |
|Phoenix Suns           |Devin Booker          |  95   |
|Portland Trail Blazers |Damian Lillard        |  118  |
|Sacramento Kings       |Buddy Hield           |  62   |
|San Antonio Spurs      |DeMar DeRozan         |  70   |
|Toronto Raptors        |Pascal Siakam         |  103  |
|Utah Jazz              |Rudy Gobert           |  156  |
|Washington Wizards     |Bradley Beal          |  82   |

## IGV and the NBA All Stars
If such a format was ever implemented, inital 'Votes' could be announced prior to the All-Star Break, contributing to the fan and player vote (also potentially a media vote), and would give us a hint at the  trajectory that we could discuss for the rest of the season.

Here's what the All Star teams could have looked like using just the voting simulation for the 2019-2020  season, using the cut off date of 11.59 pm January 20th. In a real world scenario you'd perhaps want to adjust values based on the total games played by the team to make up for any schedule related disparities.

*__Table 3.__ NBA All Stars for the 2019-2020 NBA season based on votes recieved per game up to January 20th 2020*

|East All Stars          | Pos |Votes | West All Stars         | Pos |Votes |
|:-----------------------|:---:|-----:|:-----------------------|:---:|-----:|
|**Starters**            |     |      |**Starters**            |     |      |
|Giannis Antetokounmpo   | F   |   150|LeBron James            | F   |   133|
|Jimmy Butler            | G   |   102|Rudy Gobert             | C   |   116|
|Bam Adebayo             | F   |   100|Luka Doncic             | G   |   111|
|Domantas Sabonis        | C   |    92|Nikola Jokic            | C   |   104|
|Ben Simmons             | G   |    90|James Harden            | G   |    98|
|**Reserves**            |     |      |**Reserves**            |     |      |
|Jayson Tatum            | F   |    78|Kawhi Leonard           | F   |    92|
|Khris Middleton         | F   |    73|Anthony Davis           | F   |    88|
|Trae Young              | G   |    73|Chris Paul              | G   |    83|
|Eric Bledsoe            | G   |    70|Damian Lillard          | G   |    78|
|Kemba Walker            | G   |    69|Hassan Whiteside        | C   |    70|
|Joel Embiid             | C   |    68|Devin Booker            | G   |    68|
|Andre Drummond          | C   |    64|Bojan Bogdanovic        | G   |    67|

Note how the Centres seem to be over represented compared to what we'd normally expect, I'm unsure whether this is a result of rebounds being overvalued again, or just that we don't appreciate the affect that centres have on winning NBA games (...probably the former!).

## Conclusions
If you've made it this far, well done. There was a lot more fun analysis I did, including tweaking the formula for Defensive Player of the Year, All NBA and All Defense teams. I also had a look at historical seasons and the outcome of using the same formula from my simulation to compare the results to actual media voting. The differences were quite interesting, and I think they fit pretty well against those seasons we look back at and think 'Player X deserved this but the media had voting fatigue'. All the formulas I used are on my [GitHub page](https://github.com/alegione) if you're wanting to play around with the data. Though I admittedly got a bit lazy part way though so it's not particularly well commented.

If you've got any thoughts, suggested changes, or analysis you're interested in, please feel free to get in touch via [Twitter](https://twitter.com/alegione) or Github

**- Dr Alistair Legione**

## References and tools
I did the data analysis with the help of the following R packages
+ nbastatR
+ tidyverse
+ teamcolors
+ directlabels

And of course, I utilised R and RStudio for the analysis.
