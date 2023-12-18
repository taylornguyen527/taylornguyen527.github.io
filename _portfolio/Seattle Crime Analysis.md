## Author note:
In the context of my Master of Data Science program at Seattle University, this project represents a collaborative effort for my Data Visualization class. 
In the public-facing iteration of this report, my emphasis shifts towards seamless narratives and effective storytelling, deviating from the original focus on visualization components and design choices.

My specific contribution to this report lies in executing a multi-level geospatial analysis. The process commences with geoprocessing multiple geometry types, aiming to unveil crime patterns across multiple zoning areas. Additionally, it ensures the precise integration of demographic details, including population and land areas, thereby facilitating a more thorough and nuanced analysis.

The original collaborative submission that providing detailed insights into the design choices for each graph encodings could be found here [link].

# Goal:
The central aim of this analysis is to conduct an investigation into the transformation of crime in Seattle over time while discerning its geographical distribution across various levels of zoning. The study seeks to reveal patterns and trends that illustrate the dynamics of criminal activity within the city, extending its focus to smaller communities for a more detailed understanding.

# Data Introduction and Preparation:
The analysis relies on crime data acquired from the Seattle Police Department, covering the period from 2008 to 2022. Each crime report is uniquely identified by a Report Number, and are categorized by both specific Offense Types and broader Offense Parent Groups. Notably, due to the granularity of Offense Types, the report opts for Offense Parent Groups to streamline the crime classification.

Each incident is associated with start time, end time, and report time, with a preference for using the reported time for filtering as incidents are considered finalized at that point. Additionally, incidents are geographically tagged with coordinates and various location identifiers such as police precincts, beats, and sectors. To ensure public understanding, the analysis utilizes Community Reporting Areas (CRAs) in Seattle, which delineate neighborhoods and neighborhood districts,providing a more accessible language. These CRAs aggregate smaller zoning areas like Census tracts and blocks, ensuring precise reporting without overlaps. Data from the Census Bureau are pulled in for these smaller area characteristics and geometry.

The incident coordinates undergo transformation into Geometry point objects, facilitating a spatial join technique to determine the larger zoning areas to which each point belongs. Subsequently, a merger is conducted with the "Selected Demographic and Housing Estimates (DP05)" data for the year 2020, incorporating geo spatial population information. The combination of crime patterns with demographic factors provides valuable insights, enriching the understanding of the socio-economic landscape in Seattle.

# Insights:

## Seattle Crime Dynamics: Crime Trends Over the Period 2008-2022
Examining the data from 2009 to 2022 reveals a noteworthy upward trend in overall crime in Seattle. 
![Figure 1: Crime Trends In Seattle ](https://raw.githubusercontent.com/taylornguyen527/Seattle_Crime_Analysis/main/Figures/Crime_trend.png)
Although crime rates experienced a dip from 2008 to 2012, decreasing from 65,000 to just under 60,000, they consistently rose, peaking at around 76,000 in 2020 and maintaining levels above 70,000 through 2022.

![Figure 2: Top 3 crime in change percentage](https://raw.githubusercontent.com/taylornguyen527/Seattle_Crime_Analysis/main/Figures/top3_change_overtime.png)
During this period, the top three crimes with the most significant increases were extortion/blackmail, human trafficking, and kidnapping/abduction, exhibiting growth rates of 425%, 376%, and 1,500%, respectively. Despite these seemingly rapid changes, the absolute numbers of these crimes remain relatively insignificant compared to other crime categories. Extortion/blackmail increased from 27 to 115 cases over 13 years, while kidnapping/abduction grew from 55 to 207 cases. Human trafficking, first reported in Seattle in 2018, consistently reported cases below 15 annually.

![Figure 3: Most frequent crimes in Seattle](https://raw.githubusercontent.com/taylornguyen527/Seattle_Crime_Analysis/main/Figures/Top10_count.png)

Interestingly, these high-growth categories do not make the top 10 list of popular crimes in Seattle. The most frequently committed crime in 2022 is Larceny/Theft, accounting for 24,115 cases and contributing to more than a third of all crimes in Seattle. Following closely are Assault and Burglary, with 11,402 and 8,742 cases, respectively. Collectively, these top three crimes, constituting 10% of total crimes, contribute to 65% of all reported incidents.

![Figure 4: Crime Trends In Seattle ](https://raw.githubusercontent.com/taylornguyen527/Seattle_Crime_Analysis/main/Figures/Top3_count_overtime.png)
While these three major crimes collectively grew over 24% during the analyzed period, they followed distinct trajectories. Until 2018, they fluctuated with upward trends, after which Larceny/Theft returned to approximately the same level as in 2008 in 2020. Assault cases experienced a drop from a 25% increase to a 15% increase in the same period. Notably, Burglary surged significantly in 2020, increasing by 50% compared to 2008, and maintained a high count, cooling down to a 33% increase in 2022.

In summary, the overall crime rate in Seattle increased by approximately 15% over the 13-year period, averaging around 1.15% per year. The fastest-growing crime was human trafficking, reported since 2018, showing a remarkable 1,500% increase from one annual case to 15 annual cases. The most frequently committed crimes in Seattle—Theft, Assault, and Burglary—account for 65% of all incidents, with a collective increase of more than 25% over the specified time frame. Notably, during the year of the COVID-19 pandemic, Theft cases mirrored the initial period, while Burglary experienced a sudden 30% surge.

## Geographical Analysis of Crime
