-  **OVERVIEW**

**Purpose**

Teams are formed to incorporate individuals with diverse ideas, skills,
and resources, which can spur creativity by introducing proven
innovations into new domains. However, research suggests that finding
the right balance of diversity on a team is challenging, as it may lead
to conflict and miscommunication, and may run counter to the security
individuals feel when working with past collaborators. Successful teams
find a size that enables specialization and effective division of labor
while avoiding overwhelming coordination costs.

The overall purpose of this model is to illustrate how the behavior of
individuals in assembling small teams for short-term projects can give
rise to a variety of large-scale network structures over time. It is
based on the team assembly model presented by Guimera, Uzzi, Spiro &
Amaral (2005) (Guimera et al., 2005), which draws upon observations of
collaboration networks ranging from Broadway musical industry
productions to scientific publications. The model explores how team
assembly mechanisms affect the structure of a creative field and the
success of certain teams in utilizing the resources and knowledge
available in that field, from a microscopic level to a macroscopic
level.

**Entities, state variables and scales**

In this simulation model, the agents are individuals who participate in
assembling small teams for short-term projects (For example, members of
music shows or scientific publications). They are categorized into two
types: inexperienced (newcomers) and experienced (incumbents) who have
previously participated on a team in the network structure of a specific
field. They are also part of a team that is being formed in that
structure, or they are not part of it. In addition, a specific time has
passed since the last collaboration of each of them in the form of a
team.

The environment in this model is a network of collaboration among
agents. There are links between agents that indicate members' experience
at their most recent time of collaboration, with different colors
corresponding to different types of collaboration ties , which includes
newcomer-newcomer, newcomer-incumbent, incumbent-incumbent (without
previous collaboration), and repeat collaborations).

The simulation model is displayed on a two-dimensional space where the
agents are represented as circles. The display depicts various emergent
topologies, where new collaborations and synergies among teams tend to
the center of the display, while teams or clusters with fewer
connections to new collaborations float to the edges of the world. The
figure below shows the general display of this model for the network
related to a number of agents after the passage of a number of time
ticks.

.. image:: /docs/Images/image1.png
   :width: 1.29996in
   :height: 1.31246in

State variables of this model describe important features of the
network, like the distribution of link types or the connectivity of the
network vary over time. These variables provide the number of links in
the collaboration network over time, the percentage of agents belonging
to the largest connected component network over time, and the average
size of isolated collaboration networks as a fraction of the total
number of agents.

The model will move forward in time tick by tick, not representing a
specific time unit. Agents that remain inactive for longer than τ time
steps are removed from the network. This rule is motivated by the
observation that agents do not remain in the network forever: agents age
and retire, change careers, and so on. The removal process enables the
network to reach a steady state after a transient time.

**Process overview and scheduling**

At each tick a new team is assembled with a number of agents (which is
set with "team size"). Time zero starts with an endless pool of
newcomers. After being selected for a team, newcomers become incumbents
the first time step. A new team is assembled and added to the network
every time step t. Different agents are sequentially selected to form a
team, which is added to the network. Each agent in a team has a
probability, p, of being drawn from the pool of incumbents and a
probability, 1 – p, of being drawn from the pool of newcomers. If an
agent is drawn from the incumbents' pool and there is already another
incumbent in the team, then (i) a new agent is randomly selected from
among the set of collaborators of a randomly selected incumbent already
in the team with probability q, or (ii) he or she is selected at random
among all incumbents in the network otherwise. When a team is created,
all members are linked to one another which indicate members' experience
at their most recent time of collaboration. Different colors
corresponding to different types of collaboration ties.

If an agent does not participate in a new team for a prolonged period of
time (which is set based on “max-downtime”), the agent and her links are
removed from the network. The state variables mentioned above are
updated.

-  **DESIGN PRINCIPLES**

**Basic principles**

This model investigates the mechanisms by which teams of creative agents
are assembled. Teams are formed with the purpose of integrating
individuals possessing diverse ideas, skills, and resources. The
introduction of proven innovations from one domain into a new domain
inspires fresh thinking and aids in solving old problems, thereby
encouraging creativity (Granovetter, 1973) (Reagans and Zuckerman, 2001)
(Burt, 2004). Despite the potential for diversity to stimulate
creativity, it can also lead to conflict and miscommunication (Larson et
al., 1996) (Edmondson, 1999) (Jehn et al., 1999).

**Emergence:** The system experiences a sharp transition from a
multitude of small clusters of agents to a situation in which one large
cluster of agents, comprising a substantial fraction of the individuals,
emerges: the so-called giant component.

**Adaptation:** Agents that remain inactive for longer than τ time steps
are removed from the network. In fact, agents do not remain in the
network forever: agents age and retire, change careers, and so on.

**Interaction:** Agents create links between themselves based on
members' experience at their most recent time of collaboration, and
these links are shown with four different colors.

**Stochasticity:** In each time tick when a team of agents is assembled,
team members are randomly selected from the pool of agent types based on
defined probabilities.

**Collectives:** A number of agents in each time tick form a team in the
large network of agents.

**Observation:** The variables which provide the number of links in the
collaboration network over time, the percentage of agents belonging to
the largest connected component network over time, and the average size
of isolated collaboration networks as a fraction of the total number of
agents are calculated. The color of the agents is updated. Also, the
color of the link between the agents is updated.

-  **DETAILS**

**Initialization**

The code initializes the simulation before the main schedule by creating
a team of agents (based on "team size") and linking them, and with an
endless pool of newcomers which are added to the network with a certain
probability during the run.

**Input data**

This model investigate empirically and theoretically the mechanisms by
which teams of creative agents are assembled. For investigation
theoretically, values like those in the table below can be used. For
investigation empirically, the model analyzes data from both artistic
and scientific fields to understand collaboration needs in the Broadway
musical industry (BMI) and scientific disciplines such as social
psychology, economics, ecology, and astronomy. It considers all
productions in Broadway from 1877 to 1990 and collaborations resulting
in publications in recognized journals within the fields studied.
Collaboration networks are built for each journal independently and for
the whole discipline by merging the data from the journals within a
discipline. The sources for the BMI are (Green and Ginell, 2019) and
(Simas, 1987). The data for scientific publications was obtained from
the Web of Science.

+--------------+--------------------------------------------+----------+
| Parameter    | description                                | value    |
+==============+============================================+==========+
|  team size   | the number of agents in a newly assembled  |    4     |
|              | team                                       |          |
+--------------+--------------------------------------------+----------+
| max-downtime | the number of steps an agent will remain   |    40    |
|              | in the world without collaborating before  |          |
|              | it retires                                 |          |
+--------------+--------------------------------------------+----------+
|       P      | the probability an incumbent is chosen to  |   0.4    |
|              | become a member of a new team              |          |
+--------------+--------------------------------------------+----------+
|       q      | the probability that the team being        |   0.65   |
|              | assembled will include a previous          |          |
|              | collaborator of an incumbent on the team,  |          |
|              | given that the team has at least one       |          |
|              | incumbent                                  |          |
+--------------+--------------------------------------------+----------+

**Submodels**

This section which is about each time step is presented in the form of a
flowchart and explanations about it are given below.

.. image:: /docs/Images/image2.png
   :width: 3.68518in
   :height: 6.22294in

Based on the experience of previous collaborations, at the beginning of
each time step, all existing agents are considered incumbents. Also, at
this stage, the color of all of them is set to gray and their size is
set to be slightly smaller than the size of participating agents in a
team.

Then a team with the number of members of "team size" is assembled based
on the defined rules and added to the network. Each agent in a team has
a probability, p, of being drawn from the pool of incumbents and a
probability, 1 – p, of being drawn from the pool of newcomers. If an
agent is drawn from the incumbents' pool and there is already another
incumbent in the team, then (i) a new agent is randomly selected from
among the set of collaborators of a randomly selected incumbent already
in the team with probability q, or (ii) he or she is selected at random
among all incumbents in the network otherwise.

At this stage, all members are linked to one another which indicate
members' experience at their most recent time of collaboration.
Different colors corresponding to different types of collaboration ties
(blue: newcomer-newcomer, green: newcomer-incumbent, yellow:
incumbent-incumbent (without previous collaboration), red: repeat
collaborations).

If an agent does not participate in a new team for a prolonged period of
time (which is set based on “max-downtime”), the agent and her links are
removed from the network.

To create an organized and aesthetically pleasing representation of the
network, which helps to improve the understanding of the structure and
relationships between nodes, a force-directed layout algorithm (spring
layout) is used to arrange the nodes and links, resulting in a visually
organized display that is easier to interpret.

At this stage, all the connected components in the network (i.e., groups
of connected agents) and their sizes are identified. It starts by
setting all agents as unexplored. It then randomly selects an unexplored
agent and explores all connected agents to it. The procedure continues
to randomly select unexplored agents and explores them until all agents
are explored. Finally, it outputs the sizes of all groups and the size
of the largest group.

**References**:

Burt, R.S., 2004. Structural holes and good ideas. Am. J. Sociol. 110,
349–399.

Edmondson, A., 1999. Psychological safety and learning behavior in work
teams. Adm. Sci. Q. 44, 350–383.

Granovetter, M.S., 1973. The strength of weak ties. Am. J. Sociol. 78,
1360–1380.

Green, S., Ginell, C., 2019. Broadway Musicals: Show by Show: Show by
Show. Rowman & Littlefield.

Guimera, R., Uzzi, B., Spiro, J., Amaral, L.A.N., 2005. Team assembly
mechanisms determine collaboration network structure and team
performance. Science (80-. ). 308, 697–702.

Jehn, K.A., Northcraft, G.B., Neale, M.A., 1999. Why differences make a
difference: A field study of diversity, conflict and performance in
workgroups. Adm. Sci. Q. 44, 741–763.

Larson, J.R., Christensen, C., Abbott, A.S., Franz, T.M., 1996.
Diagnosing groups: charting the flow of information in medical
decision-making teams. J. Pers. Soc. Psychol. 71, 315.

Reagans, R., Zuckerman, E.W., 2001. Networks, diversity, and
productivity: The social capital of corporate R&D teams. Organ. Sci. 12,
502–517.

Simas, R., 1987. The Musicals No One Came to See: A Guidebook to Four
Decades of Musical-comedy Casualties on Broadway, Off-Broadway, and in
Out-of-town Try-out, 1943-1983. New York: Garland Pub.
