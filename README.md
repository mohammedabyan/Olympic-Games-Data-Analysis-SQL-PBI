<div id="top"></div>
<!--
*** Thanks for checking out the Best-README-Template. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Don't forget to give the project a star!
*** Thanks again! Now go create something AMAZING! :D
-->



<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
[![LinkedIn](https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/mohammed-abyannash-400073194/)

<!-- PROJECT LOGO -->
<br />
<div align="center">

  <h2 align="center">Olympic Games Data Analysis using SQL PBI</h3>

  <p align="center">
    Front-to-end process starting from data cleansing to creating a dashboard for Olympics Database
    <br /><br />
    <a href = https://www.dropbox.com/s/3sxwx52o3x8ozj7/olympic_games.bak?dl=0>Dataset</a>
  </p>
</div>

![image](https://user-images.githubusercontent.com/29911769/165155396-68f0e4c1-6ff2-4941-a5e0-c6caf352dced.png)
![image](https://user-images.githubusercontent.com/29911769/165206267-82d08cee-447b-4f2c-bc60-54648ad92789.png)


<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#business-problem">Business Problem</a></li>
    <li><a href="#data-collection-and-table-structures">Data Collection and Table Structures</a></li>
    <li><a href="#olympic-games-analysis">Olympic Games Analysis</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>
<p align="right">(<a href="#top">back to top</a>)</p>

## Business Problem

The challenge for this data analyst project is outlined below. This has been used continuously to ensure that the right data has been selected, transformed and used in the data visualization which is meant to be passed on to the business users.

**"As a data analyst working at a news company you are asked to visualize data that will help readers understand how countries have performed historically in the summer Olympic Games.**

**You also know that there is an interest in details about the competitors, find anything interesting then don't hesitate to bring that in so if you also. The main task is still to show historical performance for different countries, with the possibility to select your own country."**

<p align="right">(<a href="#top">back to top</a>)</p>


## Data Collection and Table Structures

The necessary data is first put into and SQL database and afterwards and transformed using the transformations showed below.

```
SELECT
	[ID]
	,[Name] AS 'Competitor Name' --Rename Column
	,CASE WHEN SEX = 'M' Then 'Male' ELSE 'Female' END AS Sex
	,[Age]
	,CASE	WHEN [Age] < 18 THEN 'Under 18'
			WHEN [Age] BETWEEN 18 AND 25 THEN '18-25'
			WHEN [Age] BETWEEN 25 AND 30 THEN '25-30'
			WHEN [Age] > 30 THEN 'Over 30'
	END AS [Age Grouping]
	,[Height]
	,[Weight]
	,[NOC] AS 'Nation Code'
	,LEFT(Games, CHARINDEX(' ', Games)-1) AS 'Year'
	,RIGHT(Games, CHARINDEX(' ', REVERSE(Games))-1) AS 'Season'
	,[Games]
	,[Sport]
	,[Event]
	,CASE WHEN Medal = 'NA' THEN 'Not Registered' ELSE Medal END as Medal
FROM [olympic_games].[dbo].[athletes_event_results]
WHERE RIGHT(Games, CHARINDEX(' ', REVERSE(Games))-1) = 'Summer'
```

## Calculations

The following calculations were created in the Power BI reports using DAX (Data Analysis Expression). To lessen the extent of coding, the re-use of measures (measure branching) was emphasized:

Number of Competitors:
```
# of Competitors = DISTINCOUNT('Olympic Data'[ID])
```

Number of Medals:
```
# of Medals =
CALCULATE (
    [# of Medals],
    FILTER (
        'Olympic Games Data',
        'Olympic Games Data'[Medal] = "Bronze"
            || 'Olympic Games Data'[Medal] = "Gold"
            || 'Olympic Games Data'[Medal] = "Silver"
    )
)
```
<p align="right">(<a href="#top">back to top</a>)</p>

## Olympic Games Analysis

The finished dashboard consist of visualizations and filters that give an easy option for the end users to navigate the summer games through history. Some possibilities are to filter by period using year, nation code to focus on one country or look into either a competitor or specific sports over time. View the dashboard [here](https://github.com/mohammedabyan/Olympic-Games-Data-Analysis-SQL-PBI/raw/main/Olympic%20Games%20Dashboard.pbix).

![image](https://user-images.githubusercontent.com/29911769/165158656-16c2f292-aa4f-484f-9c62-dd6c64259f5e.png)

<p align="right">(<a href="#top">back to top</a>)</p>


## Contact

Mohammed Abyannash - mohammedabyan22@gmail.com

<p align="right">(<a href="#top">back to top</a>)</p>


