
# Dissecting A Winning Team’s Passing Game: Inter Miami vs Toronto FC

 # Introduction

We’ve opted for Inter Miami due to their impressive performance, notably scoring four goals
even after Messi was substituted early. This prompts us to explore what Inter Miami did correctly and why other MLS teams should take note. Rather than focusing on Toronto FC’s
shortcomings, this report will delve into Inter Miami’s strengths, aiming to identify key factors
that could be replicated or countered.
In what contexts might such an analytical report prove advantageous? Let us consider a hypothetical scenario: Imagine I am employed as a data analyst for a professional sports club, and
we are preparing to confront Inter Miami in our forthcoming match, directly following their
commanding victory over Toronto FC. In this scenario, the recent match analysis could furnish
invaluable insights to the team’s manager upon request. It could illuminate key facets of Inter
Miami’s recent performance, enabling the formulation of informed strategies tailored to our
imminent encounter

 # Exploration and Overview of the Dataset

Navigating through the StatsBomb free dataset can pose challenges, but fortunately, we had
the StatsBomb documentation readily available to assist us. Following the documentation, we
searched the dataset for MLS competitions and found the available full match statistics. There
are five free match statistics available, and we decided to analyze the match between Toronto
FC and Inter Miami. Initially, the event columns didn’t offer specific information, so we delved
into the event types and selected the event key for passes. Thus, our analysis begins with
the passes dataframe, where all pass data and corresponding information are provided. (pass
provider, pass receiver, pass timestamp etc.)


 #  Preprocessing and Transformation


The dataset provides a wealth of information within the dataframe we’re using. To streamline
our analysis, we’ll concentrate on extracting pass recipient location coordinates and recipient
IDs from the ’pass’ column, which is formatted extensively in JSON for each row. Moreover,
we’ll refine the dataframe to encompass solely Inter Miami passing events. Additionally, we’ll
individually extract pass location coordinates from the ’location’ column for potential future
calculations. Furthermore, we’ll capture the shot assist key from the ’pass’ row, as it appears
to contain information about whether a pass led to a shot, which is pertinent to our analysis.



# Data Validation

The StatsBomb data doesn’t inherently indicate which side of the pitch is the attackers’ half and
which is the defensive half, nor does it automatically adjust for changes in location at halftime
when teams switch sides. To address this, I reviewed the actual match video and paused it
at specific timestamps. Using these timestamps, I plotted the locations of passing players to
ensure consistency with the data. After conducting this process multiple times to eliminate
any confusion from halftime switches, I was pleasantly surprised by how closely the StatsBomb
data aligned with the pitch and actual time. The plots consistently showed that the team was
attacking the right side regardless of the time on the clock, which proved incredibly helpful for
our analysis


# Drawing Insights

## Passing Dynamics Visualization:
In our exploratory data analysis (EDA), we begin by gradually visualizing the dataframe to
extract information. Initially, we tally the total number of passes before and after halftime.
Interestingly, post-halftime, the number of passes appears to double. To gain deeper insights,
we plot the passing initiation points on the pitch. Notably, most passes in the first half originate
from the left wing or the left side of the pitch. Conversely, during the second half, the bulk of
passes gravitate towards the left midfield. This indicates heavy involvement from the Left Mid,
CM, and Left Wing in the passing dynamics, albeit with more dispersion compared to the first
half.
![before_half](https://github.com/nayeem92/Dissecting-A-Winning-Team-s-Passing-Game-Inter-Miami-vs-Toronto-FC/assets/44882242/355ea38e-896a-43b3-85a5-075a0e84ee8d)
![after_halftime](https://github.com/nayeem92/Dissecting-A-Winning-Team-s-Passing-Game-Inter-Miami-vs-Toronto-FC/assets/44882242/d035dcde-3830-4bd4-b268-80f632fba5b8)

## Pass Flow Analysis
However, analyzing solely the starting coordinates of passes doesn’t offer a comprehensive view
of their progression or defensive nature. Therefore, we further analyze the passing data by
considering both the starting and ending coordinates of each pass. Even after segmenting
passes and their directions between the two halves, the pitch chart remains densely populated.
Consequently, we opt for a pass flow map to provide a general overview of pass flow directions
across different pitch areas. Notably, we observe a substantial number of progressive passes
from center midfield to the left wing.

![before_half_pass](https://github.com/nayeem92/Dissecting-A-Winning-Team-s-Passing-Game-Inter-Miami-vs-Toronto-FC/assets/44882242/6b21c4ce-3630-41cb-983f-ae23f3e19f28)
![after_half_pass](https://github.com/nayeem92/Dissecting-A-Winning-Team-s-Passing-Game-Inter-Miami-vs-Toronto-FC/assets/44882242/d11102c2-1660-40b5-99f6-18ef9d709a09)
![passflow](https://github.com/nayeem92/Dissecting-A-Winning-Team-s-Passing-Game-Inter-Miami-vs-Toronto-FC/assets/44882242/b51298de-3a20-4219-b9c6-71b27c0d46be)


## Passing Network Construction
Seeking more insights from the passing dataframe, we construct a pivot table using player IDs
and recipient IDs to ascertain the number of passes exchanged between each player pair. This
furnishes us with a breakdown of passes made from each player to every other player, offering
valuable insights. However, we further refine our analysis by aggregating passes both from
and to each player pair to discern the total number of passes between them. Utilizing this
information, we construct a pass network illustrating pass-heavy connections between player
pairs on the pitch
![passes_between](https://github.com/nayeem92/Dissecting-A-Winning-Team-s-Passing-Game-Inter-Miami-vs-Toronto-FC/assets/44882242/14cde40d-6d98-436e-9214-fb8e9ad0c89f)
![newplot (7)](https://github.com/nayeem92/Dissecting-A-Winning-Team-s-Passing-Game-Inter-Miami-vs-Toronto-FC/assets/44882242/67baf6c6-a5ab-4494-9aac-6783eb94d0c4)


## Key Player Pairs Passing
Focusing on the top 10 pairs, we visualize their passes to identify their most active zones on
the pitch, aiding in understanding their roles in both dangerous areas and potential weaknesses.
The passing network reveals intriguing findings, prompting us to delve deeper.
![top10pass](https://github.com/nayeem92/Dissecting-A-Winning-Team-s-Passing-Game-Inter-Miami-vs-Toronto-FC/assets/44882242/52b73741-50fb-4e85-8619-f1b35ba79e76)

## Significance of Degree Centrality
Graph node degree centrality is a fundamental concept in network analysis, particularly in the
study of social networks or communication networks within teams or organizations. It measures
the number of connections or interactions that a node (in this case, a player) has with other
nodes in the network. In the context of a passing network in sports, such as football (soccer),
a player’s degree centrality reflects their involvement in passing the ball to teammates.By analyzing the degree centrality of players in a passing network, we can identify those who are
most heavily involved in facilitating connections with their teammates. Players with higher degree centrality are typically more influential within the passing network, as they are frequently
involved in passing and receiving the ball from multiple teammates. Therefore, filtering out
the top players with the highest degree centrality allows us to pinpoint the key players who
orchestrate the passing network. These pivotal players play crucial roles in distributing the ball
and coordinating team movements, making them important targets for analysis and strategic
considerations in sports tactics.
![passgraph](https://github.com/nayeem92/Dissecting-A-Winning-Team-s-Passing-Game-Inter-Miami-vs-Toronto-FC/assets/44882242/aae01613-c564-471e-8c75-32659da861e2)


## Analysis of Passing Distance
In addition to evaluating degree centrality, we delve into the passing dynamics by analyzing the
highest average passing distance between player pairs. This analysis sheds light on instances
where players engage in long passes, which are crucial for stretching the opposition’s defense or
initiating quick counterattacks.
![avg_passing](https://github.com/nayeem92/Dissecting-A-Winning-Team-s-Passing-Game-Inter-Miami-vs-Toronto-FC/assets/44882242/5cbb26ff-e686-44f8-b2ee-19e70ce6968a)


## Preferred Receiving Areas Identification
Furthermore, we identify the preferred receiving areas for Inter Miami players on the pitch. By
examining patterns in passing distribution and reception locations, we uncover strategic zones
where players tend to position themselves to receive passes. This information is instrumental
for opponents as it enables them to anticipate and intercept passes, disrupting the flow of the
opposing team’s play and potentially gaining possession in advantageous positions.
![heatmap](https://github.com/nayeem92/Dissecting-A-Winning-Team-s-Passing-Game-Inter-Miami-vs-Toronto-FC/assets/44882242/3e94591a-121a-45d5-9bfd-da2c57872e35)


## Visualization of Passes Leading to Shots
Finally, we employ visualizations to highlight passes that lead to shots on goal. By tracking the
sequences of passes that culminate in goal-scoring opportunities, we identify players who are instrumental in creating goal-scoring chances through their precise passing and vision. Opponents
should pay close attention to these players, as they possess the ability to provide key assists and
significantly impact the outcome of the match. Understanding the passing patterns leading to
shots allows teams to devise defensive strategies to neutralize these threats and minimize the
opponent’s attacking prowess.
![shotassist](https://github.com/nayeem92/Dissecting-A-Winning-Team-s-Passing-Game-Inter-Miami-vs-Toronto-FC/assets/44882242/dd6bb421-d47b-40fa-9389-15a542fcda58)


# Findings
## Degree Centrality Analysis
In terms of degree centrality, which indicates the importance of a player within the passing
network, the following five players emerged as the key influencers:
- Sergio Busquets i Burgos: With a degree centrality of 1.93, Busquets holds a pivotal role
in the passing dynamics of the team.
- Facundo Far´ıas: Also boasting a degree centrality of 1.93, Far´ıas shares the top spot with
Busquets, emphasizing his significance in facilitating team connections.
- Serhiy Kryvtsov: Kryvtsov follows closely with a degree centrality of 1.73, indicating his
integral role in the team’s passing strategies.
- DeAndre Yedlin: Yedlin mirrors Kryvtsov’s degree centrality of 1.73, highlighting his
importance in maintaining passing links on the field.
- Kamal Miller: With a degree centrality of 1.67, Miller rounds up the top five players who
play crucial roles in the team’s passing network.
## Passing Combinations and Shot Creation
Several passing combinations stood out for their frequency and impact on creating opportunities:
- Serhiy Kryvtsov and Kamal Miller led with 33 passes between them, showcasing a strong
connection in the team’s passing dynamics.
- DeAndre Yedlin and Robert Taylor closely followed with 26 passes, suggesting a reliable
partnership in advancing the ball.
- Sergio Busquets i Burgos, David Ruiz, Jordi Alba Ramos, Facundo Far´ıas, and Robert
Taylor were identified as players whose passes frequently led to shots, underscoring their
role in offensive plays.
## Passing Distances
Analyzing the average passing distances revealed insights into the team’s passing strategy:
- Kamal Miller to Drake Callender had the longest average passing distance at 26.48 meters,
indicating a preference for longer passes between these players.
- Facundo Far´ıas to DeAndre Yedlin followed closely with an average passing distance of
25.52 meters, suggesting a strategic emphasis on stretching the play.
- Kamal Miller’s passes to Noah Allen and Jordi Alba Ramos, with average distances of
22.14 and 21.84 meters respectively, further demonstrated the team’s utilization of longer
passing ranges to advance the ball.
- Serhiy Kryvtsov’s passes to Kamal Miller, with an average distance of 21.82 meters, also
contributed significantly to the team’s strategic passing approach.
## Key Players to Neutralize
Considering the comprehensive analysis of passing dynamics, shot creation, and passing distances, the following players emerge as critical targets for the opposition to neutralize:
- Sergio Busquets i Burgos
- Facundo Far´ıas
- Serhiy Kryvtsov
- DeAndre Yedlin
- Kamal Miller
Neutralizing these key players could disrupt the team’s passing patterns and potentially
limit their effectiveness on the field.
# Conclusion
In conclusion, our analysis of Inter Miami’s performance against Toronto FC offers valuable
insights for strategic planning. By focusing on Inter Miami’s strengths, we’ve identified key
factors contributing to their success, providing actionable intelligence for future matches. Our
exploration of the dataset and validation efforts ensured the accuracy of our findings, aligning
closely with real match scenarios. Through insights into passing dynamics, player connections,
and strategic importance, we’ve highlighted critical targets for opposition teams to neutralize.
