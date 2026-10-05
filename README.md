# netflix-analysis

Netflix Data Analysis (SQL and Power BI)

An SQL analysis of Netflix's catalogue of 8,807 movies and TV shows. It answers 23 business questions about content mix, genres, ratings, countries and talent, and a Power BI dashboard covers the same dataset.

Overview

The project uses the public Netflix titles dataset from Kaggle to answer the questions a content strategy team would ask: what the catalogue is made of, where it comes from, who it is rated for, and where the gaps are. All answers come from SQL queries against a single table. The Power BI report presents the same data as an interactive dashboard.

Dataset
Source: Netflix Movies and TV Shows on Kaggle (user: shivamb)
Size: 8,807 records, 12 columns, release years 1925 to 2021
Columns: show_id, type, title, director, cast, country, date_added, release_year, rating, duration, listed_in, description
Missing values: director is empty for 2,634 titles, cast for 825, country for 831, date_added for 10, rating for 4 and duration for 3


Tools

SQL (PostgreSQL)

Power BI

Repository structure

Business questions

Queries	Theme	What they cover

1 to 5	Content type and distribution	Movies vs TV shows, underrepresented genres, titles per genre, TV shows with more than 5 seasons, average seasons per show

6 to 8	Ratings and categorisation	Most common ratings, family-friendly vs mature content, keyword flags ('kill', 'violence') in descriptions

9 to 11	Trends and additions	Titles released in 2020, titles released 2020 to 2024, day of the week titles were added

12 to 14	Regional focus	Top 5 countries, contribution by country, average release year by country

15 to 19	Talent and collaboration	Titles by Rajiv Chilaka, titles featuring Salman Khan, most active actors, most frequent directors, recurring actor pairs

20 to 21	Duration and performance	Longest movie and TV show, long-running TV shows by seasons

22 to 23	Missing metadata and documentaries	Titles without a director, documentary movies

SQL techniques used
CTEs and aggregates (GROUP BY, COUNT, AVG, ROUND)
Splitting comma-separated columns into rows with string_to_array and UNNEST
A self-join on title to find recurring actor pairs
CASE WHEN to bucket ratings and flag description keywords
String parsing with SPLIT_PART and SUBSTRING for the mixed minutes and seasons duration field
Date handling with TO_DATE and TO_CHAR
Key findings
Two movies for every TV show. Movies are 6,131 titles (69.6%) and TV shows are 2,676 (30.4%).
International films and drama lead the genres. International Movies (2,752), Dramas (2,427) and Comedies (1,674) are the largest of the 42 genre tags. Classic & Cult TV has only 28 titles.
The United States dominates. 3,689 titles involve the US, followed by India (1,046), the United Kingdom (804), Canada (445) and France (393). A co-production counts once for each country.
The catalogue skews mature. Using the rating groups defined in the queries, 6,659 titles are mature and 2,052 are family-friendly. TV-MA is the most common rating (3,207), then TV-14 (2,160).
Friday is the busiest day for new titles. 2,498 titles were added on a Friday, about 28% of all dated additions and 1.8 times the next busiest day, Thursday (1,396).
Most TV shows are short. The average is 1.76 seasons, only 99 shows run past 5 seasons, and the longest is Grey's Anatomy at 17.
Director data has gaps. 2,634 titles (about 30%) list no director.
Most frequent director: Rajiv Chilaka, credited on 22 titles when co-directing credits are split out.
How to run
Download netflix_titles.csv from Kaggle and save it as data/netflix_titles.csv.
Create a PostgreSQL database and run the CREATE TABLE statement at the top of sql/netflix_analysis.sql.
Load the CSV. The column order in the file matches the table, so this works in psql:
sql
   \copy netflix FROM 'data/netflix_titles.csv' WITH (FORMAT csv, HEADER true);

The table names the cast column casts, while the CSV header says cast. 4. Run the queries one at a time. Each is introduced by a numbered comment, so select a query and execute it in pgAdmin or psql.

Power BI dashboard

dashboard/Netflix_Power_BI_Dashboard.pdf is a two-page export of the report.

Page 1: KPI cards for titles, countries, ratings, genres, directors and average duration; year-released and year-added slicers; the movie and TV split, rating mix, popular actors and genres, content released over time, and a country map.
Page 2: a decomposition tree that drills from content type through genre, rating, release year and director down to a single title.
Report

docs/Netflix_Data_Analysis_Report.docx documents the problem statement, dataset, methodology and queries.

Author

Dharshika Sivasenthilkumar, Data Analyst. LinkedIn

Disclaimer

This is an independent analysis of a public dataset. Netflix is a trademark of Netflix, Inc., and this project is not affiliated with or endorsed by Netflix.
