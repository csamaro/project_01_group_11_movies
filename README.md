# American Movie Trends Before and After COVID: Analysis Report

## `Description`
An analysis of American movie trends before and after the COVD-19 pandemic based on data from [IMDb](https://www.imdb.com/) (**I**nternet **M**ovie **D**atabase).

## `Team Info`

- Acknowledgements:
    * Program: [University of California Berkeley Data Analytics Bootcamp](https://bootcamp.berkeley.edu/) (February - August 2023 cohort)
    * Instructor: Ahmad Sweed
    * TA's: Venkata Kuppa, Karen Fisher, Brian Perry, Ryan Bernstein
    * Tutor: Bethany Lindberg
- Analysis by 
    * [Crimson Amaro](https://github.com/csamaro)
    * [Chanelle Gonzalez](https://github.com/chanellelgonzalez)
    * [Irfan Senyurt](https://github.com/sncrsenyurt)
    * [Jing Sy](https://github.com/jingsy119)
    * [Matthew Reyes](https://github.com/Mattbreyes)
    * [Jared Perez](https://github.com/jaredap1995)
    * [Vinayak Shankar](https://github.com/VinnyShankar)

- `REPO:` https://github.com/VinnyShankar/project_01_group_11_movies

## `Data Sources`
|Name|Type|Description|Website|
|---|---|---|---|
|Wikipedia|Table|List of titles|https://en.wikipedia.org/wiki/Lists_of_American_films|
|Wikipedia|Table|List of titles|https://en.wikipedia.org/wiki/Lists_of_Netflix_original_films|
|Wikipedia|Table|List of titles|https://en.wikipedia.org/wiki/List_of_Disney%2B_original_films|
|Wikipedia|Table|List of titles|https://en.wikipedia.org/wiki/List_of_Amazon_Prime_Video_original_films|
|Wikipedia|Table|List of titles|https://en.wikipedia.org/wiki/List_of_Hulu_original_films|
|OMDb|API|List of IMDb ID's|http://www.omdbapi.com/|
|IMDb|HTML|Movie data|https://www.imdb.com/|

## `Table of Contents`
- Introduction
- Hypothesis
- Data
- Analysis
- Conclusion

## `Introduction`

In this program, we learned how to use `Python`, `Pandas`, `Matplotplib`, and `APIs`. For this project, we use all these skills and also some skills obtained outside class including `HTML web scraping` and `Predictive Modeling`. In this project, we perform basic analysis on movie success factors before and after the COVID-19 pandemic.

### Why?
We chose this topic because we all love movies and have all noticed a change in our movie-watching habits before and after the COVID-19 pandemic. We wanted to know if our anecdotal observations extended to industry-wide trends.

### Definitions
- `Pre COVID`
    * January 1, 2018 - December 31, 2019
- `Post COVID`
    * January 1, 2020 - December 31, 2022
- `BoxOffice`
    * Any film where Gross (revenue) is `not null`
- `Netflix`
    * Any film with the string `netflix` for Platform

### Our questions:
* `Before` and `after` COVID-19 for `BoxOffice` and `Netflix`:
    - Did the number of movies released change?
    - Did user ratings change?
    - Did movie budgets change?
    - Did movie gross revenue change?
    - Did the relationship between budget and rating change?
    - Did the relationship between budget and gross change?
    - What were the deeper statistical observations?

## `Hypothesis`
**H<sub>o</sub>:** The COVID-19 pandemic had no impact on movie trends.

**H<sub>a</sub>:** The COVID-19 pandemic had a statistically significant impact on movie trends.

## `Data`
### Data Acquisition
- `Wikipedia`: lists of movie titles (CSVs)
- `OMDb API`: lists of IMDb IDs (API)
- `IMDb`: movie data for each IMDb ID (BeautifulSoup HTML Scrape)
    * Title
    * Type
    * Release date
    * Runtime (seconds)
    * Genre
    * Nominations (major awards)
    * Metascore
    * IMDb user rating
    * IMDb user vote count
    * Production Budget
    * Gross revenue
    * Production Budget Currency
    * Gross Revenue Currency
    * Primary Language
- `Web scraping tutorial 1`: [3i Data Scraping](https://www.3idatascraping.com/how-to-scrape-imdb-top-box-office-movies-data-using-python.php)
- `Web scraping tutorial 2`: [YouTube](https://www.youtube.com/watch?v=LCVSmkyB4v8)
- `Web scraping tutorial 3`: [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
- `Web scraping tutorial 4`: [DataCamp](https://www.datacamp.com/tutorial/importing-data-into-pandas)
- `Web scraping tutorial 5`: [ScrapeOps](https://scrapeops.io/web-scraping-playbook/403-forbidden-error-web-scraping/)
- `Web scraping tutorial 6`: [freeCodeCamp](https://www.freecodecamp.org/news/python-json-how-to-convert-a-string-to-json/)


### Data Cleaning
- Create Filtered DataFrame
    - Exclude dates containing string "None"
    - Format dates as type "datetime64"
    - Filter for dates >= "2018-01-01" and < "2023-01-01"
    - Filter for Type == "Movie"
    - Filter for Runtime >= 5400 seconds
- Add Platform column to Filtered DataFrame
    - Create sub-DataFrames for each streaming platform
    - Add "Platform" column with corresponding labels
    - Concatenate streaming platforms into single DataFrame
    - Merge streaming DataFrame onto Filtered DataFrame using Title column
    - Find duplicated Titles and drop all rows for those Titles
    - Fill null values in Platform column with "others"
- Export to CSV

## `Analysis`
### `Number of movies released`
- `Box Office`: We definitely noticed a decline for 2020, during the peak of the shut down, which was expected. It seems to have bounced back quickly in 2021, which didn't continue into 2022. Perhaps this is from movies that had been completed in 2020, but the release was held until 2021. However, to really understand any true long term impact, we would need more historical data to establish a pattern before COVID, as it looks like 2019 already saw a decrease.
- `Netflix`: It appears that Netflix was already on the rise in 2019, and actually seemed to peak in 2020 and plateau with a slight decline in the years after COVID.
![TETCB by State Rank](Images/TETCB_State_Rankings.png)

### `Genre Comparisons Pre & Post COVID`
- `Box Office`: For the box office results, pre and post COVID didn't pose many differences. We see the highest three genres for both were Action, Comedy, and Drama. However, post-COVID production of dramas was doubled, making it the highest ranking genre overall. Also, we see that more thrillers and fantasy movies were made post COVID. But the number of both genres were still under double digits.
- `Netflix`: For Netflix, the amount of movies produced post-COVID is significantly greater, so all of their genre counts have seen an increase. The top three genres (Action, Comedy, and Drama) have each had 4x more movies produced than they did pre-COVID. On the opposite scale, we see that thrillers and horror films are two of the three lowest produced genres post-COVID. This may be a result of the effects COVID had on people and the overall feel of the country after the pandemic.

### `Ratings`
- IMDB `ratings` for both Box Office and NetFlix show a marginal decline after COVID. This implies a marginal decline in the quality after COVID.
- `Metascore ratings` for Box Office actually showed that the decline in ratings started before the pandemic, and has actually been on the rise, since rebounding from COVID. However, Netflix was really rocked by COVID and these ratings continue to slide.
- Generally speaking, the data suggests that COVID did affect the `ratings`/ quality of the movies. Given the small sample size, to confirm the trend we would need a larger historical pattern to indicate if this is truly significant.

### `Budget vs. Genre`
- Additional data manipulation
    - Load the "movies.csv" file using the pandas read_csv() function.
    - Convert the "Release" column to datetime format using pd.to_datetime().
    - Replace NaN values with 0 in the "Gross" and "Budget" columns using loc[] function.
        * Create separate dataframes for each category:boxoffice_preCOVID: Movies released in 2018-2019 in theaters
        * boxoffice_postCOVID: Movies released in 2020 and later in theaters
        * netflix_preCOVID: Movies released in 2018-2019 on Netflix
        * netflix_postCOVID: Movies released in 2020 and later on Netflix
    - Compute the average budget per genre for each category using groupby() and mean() functions.
    - Get the top 5 genres and group the remaining genres as "Other" using slicing and sum() functions.
- This data provides an insight into how the movie industry has been affected by the COVID-19 pandemic, specifically in terms of budget allocation for different genres. The data analysis shows that there has been a shift in budget allocation for different genres, with some genres seeing a significant decrease in budget allocation while others have seen an increase.

### `Gross for Box Office Movies`
- Pandemic significantly (p<<0.05) and negatively impacted box office movie gross
- Movie budget remained relatively constant throughout 2018-2022
- As per movie genre, animation gained the highest gross pre-COVID (~30%) in comparison to others
- Post-COVID, adventure type of movies had the highest gross amongst all genres in 2020 and 2022 (~40%), while action movies had the largest gross proportion in 2021 (36%). Animation movies, however, showed a reduction in gross proportion post-COVID (<30%)

### `Budget vs. Rating`
- `Overall` budget has increased from Pre-COVID to Post-COVID eras, leading to higher ratings and viewership across the spectrum.
- `Box Office` movie budgets stayed relatively similar, but produced less movies in addition to receiving lower ratings and lower viewership.
- `Netflix` movie budgets increased along with more movies being produced, followed by an increase in both ratings and viewership.
- `Metascore ratings` had similar effects on both Netflix and box office productions, with overall metascore ratings decreasing from one era to the next.

### `Budget vs. Gross`
- Additional definitions
    * `ROI`: Return on Investment (Gross / Budget)
    * `Profit`: Gross profit (Gross - Budget)
- The histograms of `Budget`, `Gross`, `ROI`, and `Profit` show that none of these metrics are normally distributed.
- The box plots of `Budget` show a moderate decrease when the pandemic begins, and a rapid recovery to above pre-pandemic levels.
- The box plots of `Gross` distribution by year show a significant decrease when the pandemic begins, and a slow recovery that has not reached pre-pandemic levels.
- The box plots of `ROI` distribution by year show a significant decrease when the pandemic begins, and a slow recovery that has not reached pre-pandemic levels.
### `Residuals and Predictive Modeling`

### Total Energy Consumption 2000's Bar Chart
#### CA vs US
![TETCB 2000s CA vs US](Images/TETCB_CA_vs_US_Bar_2000.png)

### Total CO2 Emission 2000's Bar Chart
#### CA vs US
![CO2 2000s CA vs US](Images/CO2_CA_vs_US_Bar_2000.png)

#### US vs North America
![CO2 2000s US vs NA](Images/CO2_US_vs_NA_Bar_2000.png)

#### US vs World
![CO2 2000s US vs World](Images/CO2_US_vs_World_Bar_2000.png)

## Conclusion

**H<sub>o</sub>:** The COVID-19 pandemic had no impact on movie trends.

**H<sub>a</sub>:** The COVID-19 pandemic had a statistically significant impact on movie trends.

Based on our analysis, we can reject the null hypothesis. We reject the statement  `The COVID-19 pandemic had no impact on movie trends`.

![TETCB vs. CO2 Correlation](Images/TETCBvsCO2_State_Combined_Correlation.png)

With such a strong positive correlation seen above (correlation coefficient of 0.976, p-value of 0.0), we can conclude that there is a correlation between fossil fuel energy consumption and CO2 emissions. `As Total Fossil Fuel Energy Consumption increases, CO2 Emissions increases with it.`