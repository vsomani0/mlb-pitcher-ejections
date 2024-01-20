# Are pitchers on teams with older managers more likely to intentionally hit batters since 2008?
## Hypothesis

Until the early 2000s, violating baseball’s unwritten rules (i.e staring too long at a home run, trying too hard to score when up big) often resulted in MLB pitchers intentionally throwing baseballs at hitters. Now, however, most look down on this practice -- it's far too extreme to hurt and potentially injure an opponent's batter just for a minor (and often unintended) slight. Still, however, this practice does occur. Many, including myself, suspect that older managers -- who coached in an era where this was acceptable -- would be more likely to intentionally hit an opponent's batter. 

## Description

In order to perform a hypothesis test, I needed a few pieces of data.

1. A list of all times a pitcher intentionally hit a batter (done in hbp-ejections-by-year.ipynb)

This posed the initial problem: whether a pitcher intentionally hit a batter, the thing I'm trying to measure, is highly subjective. Even if a pitcher looks to have intentionally hit a batter, they may argue that they just threw the pitch haywire on accident. The best way I could think of to measure this is by using the umpires' opinion, since an umpire has adequate context. If an umpire believes that a hit-by-pitch was intentional, then they must either eject or warn the pitcher. Retrosheet has data of all the [ejections](https://www.retrosheet.org/eject.htm) (unfortunately, no warnings), their date, and importantly, a reason for them. I developed a function to consider the keywords of the reason and determine whether the ejection was for an intentional hit-by-pitch in hbp-ejections-by-year.ipynb.

2. The age of the manager of the pitchers' team when an intentional hit-by-pitch ejection happened (done in managers-by-team.ipynb)

In order to get this information, I need a few things. First of all, I need the manager information for all teams. I got this by taking a manager information for each team individually via Wikipedia, and combining them into List_of_all_managers.csv. Then, I did some cleanup on Pandas to make it work properly.

I also needed to get the birth year of the managers, which were not in the tables. In order to do this, I used a web lookup via the wptools, which extracts Wikidata from Wikipedia. Here, having my other data table from Wikipedia made it so that I got a match for each name).Unfortunately, my script was unable to resolve the birth year of about 10% of managers, since they had a Wikipedia disambiguation page (containing multiple people with the first and last name). I got a list of all these issues, and manually resolve them, inputting the managers' correct year of birth information.

3. A combined data table including necessary information from both (done in combined-project.ipynb)

Here, I needed to resolve a few differences within the data tables -- such as the team names being stored differently and needing to extract all the years coached from a range (ex:2016-present, 2018- ), which took some cleanup. Now, I had a year and a team of an ejection in one table, and a list of all managers by team in another table. I would find the manager name who coached when the year and the team corresponded. After that, I needed to fix one final annoying issue: multiple managers for the same team over the same year. 

## Data Sources
- Wikipedia pages like [this](https://en.wikipedia.org/wiki/List_of_San_Francisco_Giants_managers), but for all teams
- [Retrosheet](https://www.retrosheet.org/eject.htm)
- Wikidata

## Conclusion

Found no significant correlation of lower manager ages to higher likelihood of intentional hit-by-pitch ejections.
