# MICROSOFT MOVIE ANALYSIS

![alt text](../visual_data/microsoft_logo.png)

## Project overview
In this project, i aimed to provide actionable insights for Microsoft's new movie studio by analyzing trends in the film industry. By conducting exploratory data analysis (EDA) on box office data, i seek to understand which types of films are currently performing the best and translate those findings into recommendations for the types of films Microsoft should consider creating.

## Business understanding.
The primary objective is to explore the landscape of the movie industry and identify the types of films that are currently performing exceptionally well at the box office.

I formulated some questions to guide me inorder to identify the type of films doing well.

Here are the business questions:

Which movies are the most profitable?

Which movie genre are most commonly produced?

Which is the best time to release a movie?

## Data understanding and analysis

 I utilized publicly available data on movie box office performance, including information such as genre, budget, profit and release dates. The dataset was sourced from reputable sources such as IMDb, Box Office Mojo, or The Numbers.

1. https://www.boxofficemojo.com/

2. https://www.imdb.com/

3. https://www.rottentomatoes.com/

4. https://www.themoviedb.org/

5. https://www.the-numbers.com/


## Methodology
Data Collection: I gathered relevant datasets containing information on box office performance, movie genres, and other pertinent attributes.

Data Preprocessing: Cleaned the data by handling missing values, removing duplicates, and formatting data types appropriately.

Exploratory Data Analysis (EDA): Conducted thorough analysis to identify trends and patterns in the data.I did the summary statistics of the dataset. Explored relationships between variables such as genre, budget and profits.

Visualization: Created visualizations  to effectively communicate key findings and trends.

Here are the visualizations for  each question:

## Question 1. Which movies are most profitable?

To calculate the profit

df_movie_budget['profit'] = df_movie_budget['worldwide_gross'] - df_movie_budget['production_budget']

Calculate profit margin

df_movie_budget['profit_margin'] = (df_movie_budget['profit'] / df_movie_budget['worldwide_gross'])
df_movie_budget.head()

![budgetvsprofit](<../visual_data/budget vs profit.png>)

There is a positive correlation between budget and box office profits, indicating that investing in high-quality production and marketing is crucial for success.

### Part 2
Calculate adjustment factor

df_movie_budget['adjustment_factor'] = latest_year / df_movie_budget['Year']

Calculate adjusted budget

df_movie_budget['adjusted_budget'] = df_movie_budget['production_budget'] * df_movie_budget['adjustment_factor']

#calculating the adjusted profit

df_movie_budget['adjusted_profit'] = df_movie_budget['profit'] * df_movie_budget['adjustment_factor']

Drop the adjustment factor column if not needed

df_movie_budget.drop(columns=['adjustment_factor'], inplace=True)

The calculation above was to enable me to get the most profitable movie based on the adjusted calculated profit

![profitabel_movies](../visual_data/most_profitable_movies.png)

## Question 2. What is the most common movie genre?

Calculated the occurrence of each genre.

genre_counts = pd.Series(all_genres).value_counts()

![Genres](<../visual_data/histogram of genres.png>)

Analysis of box office data reveals that certain genres consistently perform better than others. Action, adventure, drama and comedy genres tend to attract larger audiences and generate higher revenue.

## Question 3. When is the best time to release a movie?

#### Got the number of movies released per month

month_total= df_movie_budget.groupby(['month'], as_index=False)['movie'].count().sort_values(by='movie', ascending=False)
month_total

![Movies released per month](<../visual_data/num of movies per month.png>)

Timing of movie releases also plays a significant role, with certain seasons or months showing higher box office returns.


## Recommendations
1. Focus on high performing genres- Action, adventure, drama, and comedy movies have been successful in the box office. Consider investing in these genres to attract a broad audience and maximize box office revenue.

2. Prioritize quality over quantity. Allocate resources to produce high-quality films with compelling narratives, talented casts, and cutting-edge visual effects. Increase in production budget will lead to higher profits.

3. Strategic release plan- Consider releasing movies around October and December when audience demand is high. Strategic release planning can optimize ticket sales and maximize exposure for Microsoft's movies.

