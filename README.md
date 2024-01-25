#game_project
In this project, I take on the role of an analyst in a company developing mobile games.


#### **There are three issues to be resolved:**

1. Writing a function to count the Retention of players
**Available data:**
reg_data - df about registration time
auth_data - df about the time users entered the game
data - df in which reg_data and auth_data are merged by "uid"

2. There are two different sets of clauses (a_group and b_group).
- ARPU in the test group (b_group) is 5% higher than in the control group (a_group);
- In the control group (a_group) 1928 players out of 202103 are paying (~0.95%);
- In the test (b_group) group, 1805 out of 202667 are paying (~0.89%).

**Announcing hypotheses:**
- H0 – there is no difference between groups a & b
- H1 – groups a & b are significantly different

It is required to identify the best set of proposals.

3. It is necessary to determine a set of outcome evaluation metrics according to the following condition:
_In Plants & Gardens, there are time-limited themed events every month. In them, players can receive unique items for the garden and characters, additional coins or bonuses.
To receive a reward you need to complete a number of levels within a certain time. What metrics can be used to evaluate the results of the last past event?
Let's say that in another event we complicated the mechanics of events so that with each unsuccessful attempt to complete a level, the player will roll back several levels. Will the set of outcome assessment metrics change? If yes, how?_


#### **Stack used:**
*Python
- numpy
-pandas
- scipy.stats
- matplotlib.pyplot
- tqdm.auto
- seaborn
- datetime
* Tableau


### **Results:**
1. A function has been written for calculating Retention with the ability to specify individual selection parameters (indicating the time period for calculating Retention or selecting the entire period with the word “all”, selecting the required uids or selecting all, indicating the required range of retention days).
Also, for example, the period 2017-01-01 to 2017-01-10 was selected for which a visualization was prepared for greater convenience in Tableau - https://public.tableau.com/app/profile/maksim.kuzmin/viz/Final_project_v1_Retention/ Sheet2?publish=yes

2. Taking into account the bootstrap test, data cleaning (removing 'null values') and analysis of the graphs, I consider it absolutely reasonable to reject the H0 hypothesis and conclude that b_group (test group) is significantly different from a_group (control group)
and brings more profit to the company, which means the b_group promotional offer sets work correctly and it is worth distributing them (b_group promotional offer sets) to all users to increase the company’s profits.
P.S. Ideally, select new samples according to the methodology and conduct our analysis again:

- The sample must be representative (reflect the diversity of the GS)
- The sample size must be sufficient to detect differences
- The sample must be random
- Try to exclude outliers from the sample
- Take into account specific factors influencing samples.

3. Since thematic events are held for a limited amount of time per month, they should arouse increased interest among players, because this makes it possible to obtain additional and unique items/bonuses/coins for a character or garden, which in turn will improve their gaming performance,
will give an advantage over other players (at least moral pleasure) who do not participate in themed events and do not receive unique items/bonuses/coins, which means their garden and characters develop a little slower. A condition is also set for the time it takes to complete the levels,
which complicates the task for players, which means they need to take part in the thematic event as soon as possible after its start. Taking into account the above, I consider the following metrics to be a desirable set for evaluating results:

**REACH (total number of players)** - estimate before the start of the themed event
and during its holding, by counting the unique IDs of the players participating in the event, this will allow us to assess the interest and quality of the event itself;

**SESSION DURATION** - measure the duration of the players' gaming session at normal times (without events) and during them, you can also count the number of entries into the game.
If the events are exciting and interesting to the players, then the time spent in the game and the number of entries will be greater.

**RETENTION RATE** - measure the percentage of users who return to the game after their first login. If the retention rate drops,
then consider introducing additional rewards for players if they participate in each event or complete a minimum task.

**CHURN RATE (churn rate)** - track changes in the percentage of players who stopped using the game. It is unlikely that these events will negatively affect this metric,
but in the case of the same type of events or a decrease in player motivation, this metric will show an outflow, and in this case it is necessary to reconsider the format of the events.

**PASSAGE PROGRESS** - it is important to measure the average percentage of completion of each level
