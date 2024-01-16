# Are pitchers on teams with older managers more likely to intentionally hit batters since 2008?
## Hypothesis

Until the early 2000s, violating baseball’s unwritten rules (i.e staring too long at a home run, trying too hard to score when up big) often resulted in MLB pitchers intentionally throwing baseballs at hitters. Now, however, most look down on this practice -- it's far too extreme to hurt and potentially injure an opponent's batter just for a minor (and often unintended) slight. Still, however, this practice does occur. Many, including myself, suspect that older managers -- who coached in an era where this was acceptable -- would be more likely to intentionally hit an opponent's batter. 

## Description

In order to perform a hypothesis test, I needed two key pieces of data (or a good way to approximate them)
1. A list of all times a pitcher intentionally hit a batter

This poses a problem: whether a pitcher intentionally hit a batter is highly subjective. Even if a pitcher looks to have intentionally hit a batter, they may argue that they just threw the pitch haywire on accident. The best way I could think of to measure this is by using the umpires' opinion, since an umpire has adequate context. If an umpire believes that a hit-by-pitch was intentional, then they must either eject or warn the pitcher. Retrosheet has data of all the [ejections](https://www.retrosheet.org/eject.htm) (unfortunately, no warnings), their date, and importantly, a reason for them. I developed a function to consider the keywords of the reason and determine whether the ejection was for an intentional hit-by-pitch in hbp-ejections-by-year.ipynb.

2. The age of the manager of the pitchers' team when an intentional hit-by-pitch ejection happened

In order to get this information, I need a few things. First of all, I need the manager information for all teams. I did this by taking a manager information for each team individually via Wikipedia, and combining them into List_of_all_managers.csv. Then, after some cleanup, I got a list of all managers by team who managed since 2000. 

I also needed to get the birth year of the managers, which were not in the tables. In order to do this, I used web lookup via wptools, seen in managers-by-team.ipynb. Unfortunately, my script was unable to resolve the birth year of about 10% of managers, since they had a Wikipedia disambiguation page (containing multiple people with the first and last name). I had to manually detect and resolve these, inputting the managers' correct year of birth information.

