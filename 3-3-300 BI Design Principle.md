# [Introduction - The 3-30-300 Rule](https://www.sqlbi.com/articles/introducing-the-3-30-300-rule-for-better-reports/) 

## Literture Review

[Shneiderman(1996)](https://www.cs.umd.edu/~ben/papers/Shneiderman1996eyes.pdf) explains that for most task of displaying large volume of information, visual representations are superior to textual or spoken representations. As computing techonology advances, the role of visual representations are likely to expand beyond their initial purposes. 
Throughout Shneiderman's portfolio of projects, he iteratively found a constant condensation of visual design guidelines into a basic principle known as the 'Visual Information Seeking Mantra' - _Overview first, filter & zoom, then details on demand_.
It emphasizes the importance of providing users with an initial overview of the data, allowing them to zoom in on areas of interest, filter out irrelevant information, and then accessing detailed information where necessary.

Shneiderman proposes a Type by Task Taxonomy (TTT) of information visualistion. He assumes that user are interested in viewing the attributes of grouped items. One example is to list all department within the company with a budget greater than $500,000.
The left of the TTT represents the Data Type, it describes the task-domain information object and it is organised according to the user's problem. Task across the top of the TTT are task-domain information action performed by the user.

The following seven task are considered a high level of abstration and could be further expanded or refined.
<details>
  <summary> Seven Tasks </summary>

* Overview - Provides an overview of the entire collection
* Zoom - Zoom in on items of interest
* Filter - Filter out uninteresting items
* Details on Demand - Retrieve details of items when needed
* Relate - View relationship among items
* History - keep a history of action to support undo, replay, and progressive refinement 
* Extract - extracts sub-collections and query parameter

</details>

In the context of the '3-30-300' rule for Business Intelligence (BI), we are only interested in the first four task. 

## Findings

The Visual Information-Seeking Mantra identified by Shneiderman relates the to the well - established '3-30-300' rule. Through this mantra, we set out to achieve the following tasks.

* **3** seconds - for users to get an **overview** of the **most important questions and areas**.
* **30** seconds - for users to **filter & zoom** in order to **highlight important periods and catergories**.
* **300** seconds - for users to get **details on demand** to **make informed decisions**.

<details>
  <summary>Infographic</summary>
  
  ![image1-83](https://github.com/user-attachments/assets/f8e9a120-662c-4d70-a335-b9308dfba837)
  
</details>

## Guidelines

1. Focus on specific questions - Avoid creating an report that tries to show everything
2. Go from Top Left to Bottom Right - Place the most important information on the top left of the dashboard
3. Use color to steer direction - Make it quick and convenient for user to get what they need
4. Limit Ink and Information - Avoid overwhelming user with too information (information overload)
5. Keep it simple - 
6. Make it Convenient
