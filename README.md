# TravelTide Project: Segmenting Customer Behavior with Fuzzy Segmentation 
## Building up a data-driven loyalty program

❗ **Important Notice**
As the project used plotly library for final visualisation and dashboard design, the notebook needs to be run as a Google Colab or Jupyter file.  Download the repository for execution.


👀 Check my charming video presentation [Let'd dive into TravelTides reward program!](https://www.canva.com/design/DAGQLdvNT-g/AIceGYvIf4D6-Bqt3Ubxyw/view?utm_content=DAGQLdvNT-g&utm_campaign=designshare&utm_medium=link&utm_source=recording_view)

## Objective:
The objective of this project is to leverage customer data and advanced segmentation techniques to design and optimize a personalized loyalty perk system for TravelTide. By utilizing fuzzy segmentation, the project aims to better understand customer behaviors and preferences, driving app retention and brand loyalty. 

## Project Overview
This project focuses on segmenting TravelTide's customer base using data-driven insights to design relevant perks tailored to distinct traveler personas. The analysis explores customer spending patterns, trip length, and preferences to create a flexible perk distribution model. A comprehensive A/B testing strategy was proposed to validate the effectiveness of these perks, while also addressing key travel behavior metrics, including seasonality and booking gaps. 

## Data
The dataset was extracted from TravelTide's internal booking database and enriched through feature engineering. Key features include traveler demographics, trip details, or spending habits The final aggregated user table dataset (including feature engineering) is available for download as a CSV file to ensure project accessibility for future Data Analytics projects.

## Usage: Running the Notebook
To run the notebook, simply clone this repository, install the required dependencies, and execute the code cells in order. The notebook covers the entire analysis pipeline, from data extraction and feature engineering to visualization and model building.

Feel free to access the virtual notebook directly through the link: [ traveltide_notebook.ipynb](https://colab.research.google.com/drive/1GTus1srq_ToAVhMVkgbja-_LMUHAHOrQ?usp=sharing)


## Key Tasks of Analysis: Customer Segmentation (Technical Deep Dive)

In this project, customer segmentation was performed using a combination of SQL for building up relevant analysis metrics (feature engineering) and  Pandas for data manipulation, indexing techniques, correlation analysis, and later fuzzy segmentation to allocate customers into specific loyalty perk groups. 
Here's a breakdown of the approach:

**1. Data Preparation and Feature Engineering**: Using SQL and covering session-, booking- and travel-level metrics

**2. Scaled Features**: We scaled features such as `age`, `avg_trip_length`, and `avg_checked_bags` to ensure that each metric contributed equally when constructing indexes.

**3. Correlation Analysis**: To ensure that the right features were chosen for indexing, correlation analysis was conducted. By computing correlation matrices, we identified which features were most strongly linked to important metrics

**4. Indexing and Weighting**: 
A key component of the analysis was creating weighted indexes for each perk. The idea was to combine scaled features into a single index representing the likelihood of a customer valuing a particular perk. Each feature was assigned a weight based on its assumed relevance to that perk, and the final index was calculated using a weighted sum.
This approach provided flexibility to adjust the weightings based on further analysis, such as correlation coefficients between features and customer behavior metrics. For example, strong correlations between avg_trip_length and booking frequency suggested that trip length was a key factor for certain perks.

```
# Example: Free Hotel Meal index calculation with feature weighting

cohort_subset['free_meal_index'] = (
    0.2 * cohort_subset['scaled_has_children'] +
    0.3 * cohort_subset['scaled_avg_trip_length'] +
    0.4 * cohort_subset['scaled_avg_hotel_rooms'] +
    0.1 * cohort_subset['scaled_avg_distance_flown'])
```
**5. Fuzzy Segmentation Approach**: Traditional segmentation techniques assign each customer to a single segment. However, our project leveraged fuzzy segmentation using the calculated indexes. Fuzzy segmentation assigns probabilities to customers for belonging to multiple segments, reflecting the complex and overlapping nature of their preferences.

Instead of hard segment boundaries, customers were scored for each perk, and these scores were normalized to reflect the degree to which each customer might value different perks. This method allowed for greater flexibility and enabled personalized perk distribution, as a customer could qualify for more than one perk based on their fuzzy membership scores.

**6. A/B Testing**: Fuzzy Segmentation allows for flexible A/B Testing to validate perk effectiveness (most preferred perk vs. second most preferred perk), with KPIs centered around purchase frequency and user engagement. 

## Key Findings Summary
- Balanced Distribution Across Perks: The customer distribution across perks was well-balanced, ensuring that no single perk dominates user engagement. This diversification allows for targeted marketing strategies across segments
- Distinct Segment Appeal: Each perk resonated with specific user behaviors
     -   Free Hotel Meal attracted group travelers and families
     -   Free Checked Bag was popular among frequent long-distance travelers
     -   Travel Insurance catered to risk-averse, forward planners
     -   
- Behavior-Driven Segmentation: Weighted indices based on travel metrics (e.g., trip frequency, hotel bookings) effectively segmented customers, aligning perks with travel behaviors. Making use of the advantages of fuzzy segmentation.


## Deliverables Overview
- Code Repository: Contains all SQL queries and Python scripts used for data extraction, analysis, and visualization. The analysis pipeline is fully documented and easy to reproduce.

- Visualizations: A collection of sunburst charts, radar plots, and bar graphs that visually represent customer segmentation and perk effectiveness (suing also a small simplified DASH approach with plotly).

- Recommendations Report: A detailed report summarizing key insights, including actionable recommendations for improving customer engagement and conversion rates (within code repository).

- Presentation: A compelling, non-technical crafted presentation.

- CSV File: A final user table that includes all engineered features and customer segmentation data, making it easy to explore or use in other analyses

