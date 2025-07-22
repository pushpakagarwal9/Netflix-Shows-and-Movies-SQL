# Netflix-Shows-and-Movies-SQL
- **Business Problem:** Netflix wants to gather useful insights on their shows and movies for their subscribers through their datasets. The issue is, they are working with too much data (approximately 82k rows of data combined) and are unsure how to effectively analyze and extract meaningful insights from it. They need a robust and scalable data analytics solution to handle the vast amount of data and uncover valuable patterns and trends.
- **How I Plan On Solving the Problem:** In helping Netflix gather valuable insights from their extensive movies and shows dataset, I will be utilizing SQL and a data visualization tool like Tableau to extract relevant information, and conduct insightful analyses. By leveraging SQL's functions, I can uncover key metrics such as viewer ratings, popularity trends, genre preferences, and viewership patterns. Once the data has been extracted and prepared, I will leverage Tableau to present the findings. This will allow for interactive exploration of the data, enabling stakeholders at Netflix to gain actionable insights through visually appealing charts, graphs, and interactive visualizations. I plan on creating a dynamic dashboard in Tableau that enables users to delve into specific movie genres, viewer demographics, or geographical regions.
## Questions I Wanted To Answer From the Dataset:

## 1. Which movies and shows on Netflix ranked in the top 10 and bottom 10 based on their IMDB scores?
- Top 10 Movies
```mysql
SELECT title, 
type, 
imdb_score
FROM shows_movies.titles
WHERE imdb_score >= 8.0
AND type = 'MOVIE'
ORDER BY imdb_score DESC
LIMIT 10
```
- Top 10 Shows
```mysql
SELECT title, 
type, 
imdb_score
FROM shows_movies.titles
WHERE imdb_score >= 8.0
AND type = 'SHOW'
ORDER BY imdb_score DESC
LIMIT 10
```
- Bottom 10 Movies
```mysql
SELECT title, 
type, 
imdb_score
FROM shows_movies.titles
WHERE type = 'MOVIE'
ORDER BY imdb_score ASC
LIMIT 10
```
- Bottom 10 Shows
```mysql
SELECT title, 
type, 
imdb_score
FROM shows_movies.titles
WHERE type = 'SHOW'
ORDER BY imdb_score ASC
LIMIT 10
```
## 2. How many movies and shows fall in each decade in Netflix's library?
```mysql
SELECT CONCAT(FLOOR(release_year/10)*10,'s') AS decade,
	COUNT(*) AS movies_shows_count
FROM shows_movies.titles
GROUP BY decade
ORDER BY decade;
```
The results of the SQL query provide a fascinating insight into the distribution of movies and shows across different decades in Netflix's library. The data reveals a significant shift in content availability over time, with a notable increase in the number of titles from the 2000s onwards. Starting from the earlier decades, the 1940s-1980s showcase a small fraction of the total entries, suggesting that Netflix's collection from these decades is relatively limited. The 1990s demonstrate a large surge in offerings, with 121 titles. However, the true turning point in Netflix's library occurs in the 2010s with a remarkable 3,304 movies and shows from this decade. This abundance highlights Netflix's dedication to featuring contemporary content that aligns with current trends and audience preferences.

Even though the 2020s are still in progress, the dataset reveals an impressive count of 1,972 movies and shows, indicating a strong focus on acquiring and producing content from recent years. Overall, these findings shed light on Netflix's strategy of curating library that covers a wide range of decades. The significant increase in content availability from the 2000s onwards suggests a concerted effort to offer a diverse selection of titles. This collection spanning multiple decades allows Netflix's audience to explore a variety of movies and shows that reflect different eras. 
## 3. How did age-certifications impact the dataset?
```mysql
