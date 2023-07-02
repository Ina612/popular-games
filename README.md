<h1> :frog: Analyzing Popular Games </h1>
<h2> :cherry_blossom: Data source: </h2>

The [dataset](https://www.kaggle.com/datasets/arnabchaki/popular-video-games-1980-2023) is taken from Kaggle

**Description of the dataset:**

A list of video games from 1980 to 2023. Provides data on release dates, user review rating, and critic review rating. 
- Title: the title of the game
- Release Date: date of release of the game's first version
- Team: game developer team
- Rating: average rating of the title
- Times listed: number of users who listed this game
- Number of reviews: number of reviews received from the users
- Geres: the list of genres of a specified game
- Summary: summary provided by the team
- Reviews: user reviews
- Plays: number of users that have played the game before
- Playing: number of current users who are playing the game
- Backlogs: number of users who have access but haven't started with the game yet
- Wishlist: number of users who wish to play the game

<h2> :cherry_blossom: Data pre-processing </h2>

For pre-processing, we
1. Checked for the data types of the column and corrected them;
2. Looked through nulls and removed them, as there were few of them;
3. Dropped the columns that we didn't need: Unnamed, Times Listed, Summary, Reviews, Team;
4. Made the column names lowercase and replaced spaces with _;
5. Converted the columns no_of_plays, active_players, wishlist, number_of_reviews, backlogs to numeric types.

<h3> ✏️ Correlation matrix of the pre-processed data </h3>

There is correlation b/w backlogs and wishlist, number of reviews and wishlist, number of reviews and backlogs.
 <p> </p>
 
![Correlation matrix](https://github.com/Ina612/imgs/blob/main/Correlation%20matrix%20of%20the%20pre-processed%20data.png)

<h2> :cherry_blossom: ML </h2>

The target variable we want to predict here is Rating of the game. 
The models we decided to take are Random Forest regressor and XGBoost. 

First, we decided to take all the features we have and see how the models perform.

```
features = ['number_of_reviews', 'no_of_plays', 'active_players', 'backlogs', 'wishlist', 'popularity']
x = df_pop.loc[:, features]
y = df_pop.loc[:, ['rating']]
```			     
The results with random search were: 
    - Random Forest: MSE = 0.1899, R2 Score = 0.3205
    - XGBoost: MAE = 0.3207, RMSE = 0.4438, R2 Score = 0.2949

As we see, the performance is quite low. Therefore, we decided to alter the model.

Meaningful features for this task number_of_reviews, backlogs, and wishlist as meaningful features.

<h3> ✏️ Scatter plot for number of reviews, wishlist, and backlogs </h3>

 <p> </p>
 
![Scatter plot](https://github.com/Ina612/imgs/blob/main/Scatter%20plot%20for%20games.png)

<h2> :mushroom: Logarithmic transformation </h2>
As our features of the same scale but of different with the target variable, we took a log of them.

```
# take the logarithm of the selected features
x['number_of_reviews'] = np.log(x['number_of_reviews'])
x['backlogs'] = np.log(x['backlogs'])
x['wishlist'] = np.log(x['wishlist'])
```

The results for **XGBoost** regressor: 

- R2 Score:  0.8297
- Mean Absolute Error:  0.1673
- Root Mean Squared Error:  0.2091
 
<h1> :blossom: Power BI visualization dashboard </h1>

As the goal was not only ML but also EDA, we opted for Power BI and created a [dashboard](https://github.com/Ina612/popular-games/blob/main/Popular_games_dataset.pbix).

<p> </p>

![Dataset Power BI](https://github.com/Ina612/imgs/blob/main/Popular_games_dataset.png)
