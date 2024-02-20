# Are pitchers on teams with older managers more likely to intentionally hit batters?
## Hypothesis

Until the early 2000s, violating baseball’s so called unwritten rules (i.e staring too long at a home run, trying too hard to score when up big) often resulted in MLB pitchers intentionally throwing baseballs at hitters. Now, however, most look down on this practice -- it's far too extreme to hurt and potentially injure an opponent's batter just for a minor (and often unintended) slight. In spite of this, however, intetional hit by pitches still exist. Here, we analyze whether older managers, who grew up and had their norms influenced by the unwritten rules era, are more likely to have their pitchers intentionally hit batters.

## Description

In order to perform a hypothesis test, We need a few pieces of data.

1. A list of all times a pitcher intentionally hit a batter (done in hbp-ejections-by-year.ipynb)

This posed the initial problem: whether a pitcher intentionally hit a batter is highly subjective. Even if a pitcher looks to have intentionally hit a batter, they may argue that they just threw the pitch haywire on accident. Luckily, if an umpire believes that a hit-by-pitch was intentional, then they must either eject or warn the pitcher. Retrosheet has data of all the [ejections](https://www.retrosheet.org/eject.htm) (unfortunately, no warnings), their date, and importantly, a reason for them. We then develop a function to consider the keywords of the reason given by Retrosheet to get a list of only intentional hbps was for an intentional hit-by-pitch.

2. The age of the manager of the pitchers' team when an intentional hit-by-pitch ejection happened (done in managers-by-team.ipynb)

In order to get this information, we need a few things. First of all, we need the manager information for all teams. We can do this by taking manager information for each team individually via Wikipedia, and combining them into List_of_all_managers.csv. Then, some data cleanup is required to make columns like Name more consistent.

We also need to get the birth year of the managers, which were not in the tables. Here, we can use a web lookup via wptools, which extracts Wikidata from Wikipedia. Luckily, the manager names table is also from Wikipedia, so nicknames or other small differences are consistent, and thus do not cause hassle. Unfortunately, my script was unable to resolve the birth year of about 10% of managers, since they linked to a Wikipedia disambiguation page, instead of an ordinary page. We get a list of all these issues by printing out the names that cause an excpetion, and manually inputting the managers' correct year of birth information to resolve the issues.

3. A combined data table including necessary information from both (done in combined-project.ipynb)

Here, we need to resolve a few differences within the data tables -- such as the team names being stored differently and needing to extract all the years coached from a range (ex:2016-present, 2018- ), which took some cleanup. Now, we have a year and a team of an ejection in one table, and a list of all managers by team in another table. We can find the manager name who coached when the year and the team corresponded. After that, we need to fix one final annoying issue: multiple managers for the same team over the same year. This would make our script fail, since it would find multiple managers for one ejection -- which is impossible. To resolve this, we get a list of all the potential problems -- when multiple managers coach for the same year -- and then manually look up the manager coaching at the selected date. With this being performed, we can get an accurate average manager age for occasions when his pitcher intentionally hit a batter, of 54.30. 

4. The average age of **all** managers (in combined-project.ipynb)

We can take the weighted average of the manager age to do this, so that managers who coached more games get weighted higher. Thus, in effect, we measure the average age of taking a manager of a random game -- which is a reasonable comparison. Unfortunately, although our data consists only of managers who have had a coaching stretches from 2008-2023, managers who started coaching before 2008 and ended on 2008 or later have their games coached inflated. We only want the games that a manager coached within the time interval, so we have to get a list of managers who started coaching before, and manually decrease their games counts again. After doing this, we finally have all the information we need, and find that the weighted average age of all managers in this interval is 54.13. Using the Central Limit Theorem at a 90% level, we find no significant correlation.


## Conclusion and Further Analysis

Found no significant correlation of higher manager ages to higher likelihood of intentional hit-by-pitch ejections. In the future, a larger sample size than 122 would be beneficial, perhaps by extending the number of years considered or by manually adding ejections not in Retrosheet's database.


## Data Sources
- Wikipedia pages like [this](https://en.wikipedia.org/wiki/List_of_San_Francisco_Giants_managers), but for all teams
- [Retrosheet](https://www.retrosheet.org/eject.htm)
- Wikidata