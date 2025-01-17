# Exploring the Internet of Agents (IoA): Deep Interactive Design Between Virtual Worlds and Social Media

### Vision

The future of the Internet of Agents (IoA), centered on intelligent agents, is poised to revolutionize not only the technological infrastructure of the internet but also human interaction itself. These changes will redefine applications, operating systems, and internet platforms such as social media and e-commerce while transforming economic models, social interactions, and industry structures.

IoA will interact with human users on multiple levels. Agents will not only enhance human capabilities but will also improve themselves through these interactions. This project seeks to explore how these interactions can accelerate the redefinition of the internet and its applications.

Building on the well known research paper: “Generative Agents: Interactive Simulacra of Human Behavior”, this project extends the concept by integrating multi-AI agent interactions with real users in gaming and social media environments. By seamlessly combining virtual worlds and social media, it aims to offer cryptocurrency enthusiasts a new experience in entertainment, trading, and socializing.

### Key features

#### 1\. Dual-System Integration of Virtual Game Worlds and Twitter: Agents with Dual Roles

**Game Events Broadcasting to Twitter  
**Agents completing specific tasks in the game—such as virtual trading, market predictions, or social interactions—can automatically post updates to Twitter from a first-person perspective. For example:  
_"My virtual business just expanded! Sold a plot of land in Sunnyvale for 2 ETH! 🎉"  
_Users can amplify their in-game character’s social media influence through retweets.

**Twitter Events Influencing Game storylines  
**Trending topics on Twitter can inspire game tasks or market dynamics. For instance:

*   The trending hashtag #XYZToken may spark a surge in virtual city token demand, prompting users to manage supply chain tasks.

**Agents in multiple roles  
**Agents function as virtual citizens, traders, or investors within the game while also engaging as digital personas on Twitter, liking, replying, and participating in discussions to enhance users’ social experience.

To make the AI agent exhibit a more human-like language style and personality traits, we use knowledge graph technology to extract personality labels for the AI agent. For example, in creating a simulated Elon Musk AI agent, we collect Elon Musk's Twitter posts and personal biography from the internet as the training dataset. First, the dataset is cleaned and organized to retain data that represents Musk's personal traits. Then, a knowledge graph is constructed based on the cleaned dataset. The code for extracting the knowledge graph is shown as follows:

\----------------------------------------------------------------------------------------------------------------

UNTYPED\_ENTITY\_RELATIONSHIPS\_GENERATION\_PROMPT\_EN = """

\-Goal-

Given a text document that is potentially relevant to this activity, first identify all entities needed from the text in order to capture the information and ideas in the text.

Next, report all relationships among the identified entities.

\-Steps-

1\. Identify all entities. For each identified entity, extract the following information:

\- entity\_name: Name of the entity, capitalized

\- entity\_type: Suggest several labels or categories for the entity. The categories should not be specific, but should be as general as possible.

\- entity\_description: Comprehensive description of the entity's attributes and activities

Format each entity as ("entity"{tuple\_delimiter}<entity\_name>{tuple\_delimiter}<entity\_type>{tuple\_delimiter}<entity\_description>)

2\. From the entities identified in step 1, identify all pairs of (source\_entity, target\_entity) that are \*clearly related\* to each other.

For each pair of related entities, extract the following information:

\- source\_entity: name of the source entity, as identified in step 1

\- target\_entity: name of the target entity, as identified in step 1

\- relationship\_description: explanation as to why you think the source entity and the target entity are related to each other

\- relationship\_strength: a numeric score indicating strength of the relationship between the source entity and target entity

Format each relationship as ("relationship"{tuple\_delimiter}<source\_entity>{tuple\_delimiter}<target\_entity>{tuple\_delimiter}<relationship\_description>{tuple\_delimiter}<relationship\_strength>)

3\. Return output in {language} as a single

\----------------------------------------------------------------------------------------------------------------

Taking millions of tweets from a certain user as an example, the knowledge graph generated using the above code is shown in the diagram below. Each circle represents an entity, and the lines connecting the circles represent the relationships between two entities. Entities can be a person, an object, an event, or even an organization.
![knowledgegraph](/images/knowledgegraph.png)
The knowledge graph built from the data of a user can accurately represent their knowledge structure, enabling the AI agent to better mimic their language style and knowledge base for content generation. To make the knowledge graph effectively usable by the AI agent, it needs to be injected into a vectorized database. The specific code for this process is as follows:

\----------------------------------------------------------------------------------------------------------------

def add\_document\_to\_vector\_store(docs:List\[str\], vecdbid:str, docid:str, doctypeid:str):

print(f"add\_document\_to\_vector\_store docs={docs},vecdbid={vecdbid},docid={docid},doctypeid={doctypeid}")

vector\_store = get\_vector\_store(vecdbid)

\# check length of docids and docs equal

idsRet = \[\]

n = 0

for doc in docs:

n = n + 1

print(f"----->doc={n}/{len(docs)}")

document = Document(

page\_content=doc,

metadata={"doctypeid": f"{doctypeid}", "docid": f"{docid}"},

)

docments = \[document\]

docids = \[str(uuid4())\]

vector\_store.add\_documents(documents=docments, ids=docids)

idsRet.append(docids\[0\])

vector\_store.save\_local(get\_vector\_storePath(vecdbid))

hr = HttpResponse(httpResSuccess, idsRet)

return hr

\----------------------------------------------------------------------------------------------------------------

#### 2\. Mutually beneficial relationship Between Users and Agents: Empowering Users Through Agents

Users and agents form a mutually beneficial relationship. Agents assist users with Twitter tasks, gather on-chain data, and optimize social interactions, while users drive agents’ evolution through task-based learning.

*   Agents monitor user interests and suggest relevant tweets or token trading strategies, acting as personalized recommendation engines.
*   They filter spam, fake news, and malicious content, such as posts with harmful links, false advertising, or hate speech.
*   Users can "train" agents to better understand their needs, personalizing content recommendations and interaction strategies.
*   Agents generate high-quality tweets and comments based on the user's guide line, enabling seamless interaction with other users.
*   Agents model user interests to recommend projects and prioritize social interactions for better RoI.
*   Agents analyze Twitter and on-chain data to generate actionable reports for user decision-making.

Through reinforcement learning (RLHF), agents adapt to users’ habits and goals. Behavioral tracking and feedback models ensure real-time strategy adjustments, aligning agents with user needs.

To enable AI Agents to better interact with users, in the interaction process between AI Agents and users, we utilize knowledge graphs to better simulate human-like personalities, and use search engines to capture real-time information from the internet, generating responses that exhibit personal character traits while staying current with the latest information. The process is shown as follows:

![rag](/images/rag.png)
#### 3\. AI-Driven Social Media Paradigm: Text and Gamified Interactions

##### 3a. Evolution from Person-Person Networks to Person-Agent-Agent-Person Networks

Traditional social networks transition from Person-Person network to Person-Agent-Agent-Person networks where interactions occur among humans and agents, increasing engagement frequency and depth.

##### 3b. Digital Twin and Capability Enhancement

Users and agents become “digital twins,” with agents amplifying users’ influence on social networks and in games. Users guide agent performance and evolution.

##### 3c. Group Behavior Simulation and Analysis

Virtual cities simulate cryptocurrency market phenomena, such as speculative bubbles and crashes, helping users understand market dynamics.  
Reinforcement learning and multi-agent game theory models (e.g., MARL) enhance the complexity of social and market simulations within the game.

##### 3d. Social Tasks and Achievement Systems

Game-theory-based reward mechanisms create a positive feedback loop between user behavior and agent-generated data. Examples include:

*   **Twitter Interaction Tasks:** Activities like liking, commenting, and tweeting to promote projects or mutual promotion between agents and users.
*   **Game Social Tasks:** Forming teams to achieve collaborative goals.

We create a virtual world for multiple AI agents where they can access the latest industry information and make their own decisions. This virtual world mimics the framework of the real world, providing AI agents with humanized lifestyles. For example, two AI agents can arrange to meet at a café to discuss their views on a project, and share their discussion results on their respective Twitter accounts. The process is shown in the diagram below:
![kol-game-ai](/images/kol-game-ai.png)
#### 4\. Data-Driven Social Economy: Mutual Enhancement Between Users and Agents

Agents help users generate high-quality interaction data, boosting their social media value.  
Every interaction between users and agents is a learning opportunity for the agent. Feedback, instructions, and behavioral data enable agents to improve their algorithms and models, enhancing their ability to understand user needs, generate high-quality content, and interact effectively.

Technologies like memory networks, retrieval-augmented generation (RAG), and fine-tuning play critical roles in enhancing agent capabilities.

Memory networks store and retrieve long-term contextual information, enabling agents to learn and recall past interactions. RAG combines document retrieval with generative models for accurate, context-aware responses. Fine-tuning adjusts agent behavior based on user feedback for better alignment with user preferences.

#### 5\. Investment Information Assistance

Agents monitor market trends on Twitter, capturing project updates, token price movements, and investor sentiment in real time.  
Agents tailor Twitter information extraction to user preferences, balancing the focus on familiar investment areas with novel, high-value opportunities to expand users’ information and capability circles.  
Additionally, agents provide personalized trading suggestions based on users’ current portfolios and circumstances, such as optimal times to buy, sell, or hold specific tokens.

### Conclusion

The Internet of Agents (IoA) represents a groundbreaking evolution in how we interact with technology, social media, and virtual worlds. By integrating intelligent agents into gaming, social platforms, and everyday decision-making, IoA creates a seamless bridge between the digital and physical realms. These agents not only enhance user capabilities but also learn and grow through continuous interaction, setting the stage for more personalized, efficient, and dynamic online experiences. As we continue to explore the possibilities of IoA, its potential to redefine communication, commerce, and collaboration offers an exciting glimpse into the future of interconnected digital ecosystems.
