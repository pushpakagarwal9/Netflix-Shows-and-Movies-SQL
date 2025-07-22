# Netflix-Shows-and-Movies-SQL
# <p align="center">Netflix Shows and Movies Project</p>
# <p align="center">![Pic](https://i.ibb.co/Q81WwRN/92399716.jpg)</p>
**Tools Used:** MySQL

[Datasets Used](https://www.kaggle.com/datasets/victorsoeiro/netflix-tv-shows-and-movies?select=titles.csv)
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
USE shows_movies;
SELECT age_certification,
round(avg(imdb_score),2) as avg_imbdscore
FROM titles
group by age_certification
order by avg_imbdscore desc;
```
```mysql
USE shows_movies;
SELECT age_certification,count(*) as count
FROM titles
where age_certification != ''
group by age_certification
order by count(*) desc;
```
The first query focused on the average IMDb scores associated with each age certification, revealing nuanced trends in audience ratings. According to the data, TV-PG stands out with the highest average IMDb score of 7.25, suggesting that content suitable for a broad audience garners the most favorable ratings. Close behind are TV-MA (7.13) and TV-14 (7.12), indicating that mature and teen-oriented content also resonates well with viewers. TV-Y7 (6.86), TV-Y (6.74), and PG-13 (6.71) further reflect strong audience appreciation across younger demographics. In contrast, certifications like NC-17 (5.96), R (6.38), and G (6.11) receive relatively lower average scores, suggesting a more mixed reception. Meanwhile, TV-G earns a modest 6.07, showing steady appreciation for content meant for general audiences. This range of ratings highlights how audience preferences vary across content maturity levels.

When examining the distribution of movies and shows across age certifications, the second query highlights the varying prevalence of content categories within Netflix's dataset. PG-13 emerges as the most common age certification, with 172 titles, indicating a strong focus on content tailored for teens and older audiences. This is followed by R-rated content, comprising 151 titles, which further reflects Netflix’s substantial offering for mature viewers. Certifications such as TV-14 (96 titles) and PG (87 titles) also represent a significant portion, indicating balanced content availability for both older teens and general audiences.
On the other hand, more family-friendly or children's certifications like G (38 titles), TV-PG (35), TV-G (32), TV-Y7 (25), and TV-Y (24) appear less frequently, though they still reflect Netflix's effort to maintain a varied content library. The least represented certification is NC-17, with only 5 titles, underscoring its niche nature in mainstream streaming platforms.
These findings not only reveal the diverse range of age certifications present in the dataset but also provide insights into content strategy and audience targeting. Combined with the earlier analysis of average IMDb scores, the higher ratings associated with TV-PG, TV-14, and TV-MA suggest that content within these age categories tends to be both widely available and well-received by viewers.
## 4. Which genres are the most common? 
- Top 10 most common genres for MOVIES
```mysql
USE shows_movies;
SELECT genres,count(*) as movie_count
FROM titles
where type = 'MOVIE'
group by genres
order by movie_count desc
limit 10;
```
- Top 10 most common genres for SHOWS
```mysql
SELECT genres,count(*) as movie_count
FROM titles
where type = 'SHOW'
group by genres
order by movie_count desc
limit 10;
```
- Top 3 most common genres OVERALL
```mysql
USE shows_movies;
SELECT genres,count(*) as movie_count
FROM titles
where type = 'SHOW' OR Type = 'MOVIES'
group by genres
order by movie_count desc
limit 3;
```
## Conclusion 
By exploring various aspects of the dataset, a comprehensive understanding of Netflix's content landscape was gained. The analysis of IMDb scores identified the top 10 and bottom 10 movies based on viewer ratings, offering insights into the titles that received widespread acclaim and those that were less well-received. This information helps viewers make informed decisions and indicates areas where content quality could be enhanced.

The examination of content distribution across decades revealed notable trends. A significant increase in titles from the 2000s onward underscores Netflix’s focus on modern, trend-aligned content that caters to evolving audience preferences.

Age certifications played a key role in shaping both content availability and viewer reception. The analysis showed that TV-PG had the highest average IMDb score (7.25), closely followed by TV-MA (7.13) and TV-14 (7.12), indicating that content aimed at general and mature audiences tends to be highly appreciated. In terms of content volume, PG-13 and R emerged as the most prevalent certifications, with 172 and 151 titles respectively. Meanwhile, certifications like NC-17 appeared very rarely, with only 5 titles, reflecting their niche appeal.

The genre analysis further revealed that Comedy was the most dominant genre across both movies and shows, followed by Documentary and Drama. Frequent combinations of multiple genres also highlighted audience interest in more complex and diverse storytelling formats.

Together, these insights provide a clearer picture of Netflix’s content strategy, viewer preferences, and areas of strength and improvement within its vast media library.



