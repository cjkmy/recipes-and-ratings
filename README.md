# Recipes and Rating 🍽️

## Investigation Question: What types of recipes tend to have the most calories?

### INTRODUCTION
### This study is helpful for people who may be trying to watch their calorie intakes while still being able to enjoy various types of delicious recipes. There are two initial datasets that this study will be using one containing information about the recipes, and the other containing reviews of recipes in the first dataset - it will be combined to form one big dataset keeping all the recipes with reviews.


### Dataset
The two following datasets are available for this investigation: 

1. `RAW_recipes.csv` a DataFrame that consists of information regarding food recipes with 11 columns, indexed by recipe names:

   - `id`: a series of numbers serving as identification that differentiates each recipe
   - `minutes`: the number of minutes the recipe takes to finish 
   - `contributor_id`: a unique combination of numbers that differentiates each contributor
   - `submitted`: the data of submission formatted as MM/DD/YYYY
   - `tags`: a list of tags that can be used to categorize each recipe
   - `nutrition`: a list of floats entrailing nutritional values
   - `n_steps`: the number of steps in the recipe
   - `steps`: a list of steps to follow for the recipe
   - `description`: describes what the recipe makes 
   - `ingredients`: a list of items used to create the final product
   - `n_ingredients`: the number of ingredients needed for the recipe

2. `interactions.csv`: a DataFrame that consists of information regarding people's reviews of certain recipes with 4 columns, indexed by user_id:

   - `recipe_id`: a series of numbers serving as identification that differentiates each recipe
   - `date`: the data of the review being sent formatted as MM/DD/YYYY
   - `rating`: a rating out of 5 for the recipe
   - `review`: comments made by the reviewer about the recipe

### DATA CLEANING AND EXPLORATORY ANALYSIS
### Steps Taken To Clean The Data 
There are four segments or rather four steps consisting of several lines of code for each step.
1. Merging and Using Data Frames 
   
   I've merged `RAW_recipes.csv` and `interaction.csv` using the recipe names and preserving all rows (recipes) from the first data frame. I then used the merged dataset to calculate for 'avg_rating_per_recipe', which serves as a new column for the recipe data frame for usage in the rest of the analysis.

2. Converting Strings

   The `RAW_recipes.csv` is needed for several columns to be converted from strings. The 'submitted' column was converted to date-times, and the columns' nutrition, tags, steps, and ingredients were all converted into functioning lists.

3. Minimizing the Data Frame

   To prevent any outlandish statistics, I've decided to filter the recipe data frame to only include recipes with less than or equal to 900 calories. Adhering to the recommended calorie intake per day of 2500 to 2700, which is about 900 max per meal (breakfast, lunch, and dinner). This helps to prevent any extreme statistics from heavily skewing the analysis results. I've also filtered any times that explicitly has an integer at the start, since I noticed that if there exist an integer at the start of the name it is likely the number of multiple servings.



This is how the resulting data frame that will be used for analysis will look like!

|    | name                                    |     id |   minutes |   contributor_id | submitted           | tags                                                                                                                                                                                                                                                                                                                                              |   calories |   n_steps | steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | ingredients                                                                                                                                |   n_ingredients |   avg_rating |
|---:|:----------------------------------------|-------:|----------:|-----------------:|:--------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------:|----------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------|----------------:|-------------:|
|  3 | millionaire pound cake                  | 286009 |       120 |           461724 | 2008-02-12 00:00:00 | ['time-to-make', 'course', 'cuisine', 'preparation', 'occasion', 'north-american', 'desserts', 'american', 'southern-united-states', 'dinner-party', 'holiday-event', 'cakes', 'dietary', 'christmas', 'thanksgiving', 'low-sodium', 'low-in-something', 'taste-mood', 'sweet', '4-hours-or-less']                                                |      878.3 |         7 | ['freheat the oven to 300 degrees', 'grease a 10-inch tube pan with butter , dust the bottom and sides with flour , and set aside', 'in a large mixing bowl , cream the butter and sugar with an electric mixer and add the eggs one at a time , beating after each addition', 'alternately add the flour and milk , stirring till the batter is smooth', 'add the two extracts and stir till well blended', 'scrape the batter into the prepared pan and bake till a cake tester or knife blade inserted in the center comes out clean , about 1 1 / 2 hours', 'cool the cake in the pan on a rack for 5 minutes , then turn it out on the rack to cool completely']                                                                                                                                                                                                        | why a millionaire pound cake?  because it's super rich!  this scrumptious cake is the pride of an elderly belle from jackson, mississippi.  the recipe comes from "the glory of southern cooking" by james villas.                                                                                                                                                                                                                                                                                                                                                                           | ['butter', 'sugar', 'eggs', 'all-purpose flour', 'whole milk', 'pure vanilla extract', 'almond extract']                                   |               7 |            5 |
|  7 | blepandekager   danish   apple pancakes | 503475 |        50 |           128473 | 2013-07-08 00:00:00 | ['danish', '60-minutes-or-less', 'time-to-make', 'course', 'cuisine', 'preparation', 'pancakes-and-waffles', 'breakfast', 'scandinavian', 'european']                                                                                                                                                                                             |      358.2 |        10 | ['beat the eggs lightly and add the milk', 'combine the flour , sugar and salt', 'stir the flour mixture into the egg mixture , stirring in the cup of cream as you mix', 'fry the apple slices in butter in a skillet', 'preheat oven to 500 degree', 'cover the bottom of an oven-proof baking dish , or heavy skillet , with apples', 'pour the batter over slices and bake in a preheated 500 oven', 'when nearly done , remove from oven and sprinkle here and there with a mixture of sugar and cinnamon to taste', 'place dabs of butter on the pancake and return to oven until browned', 'just before serving , sprinkle with lemon juice , and cut into triangles']                                                                                                                                                                                                | this recipe has been posted here for play in zwt9 - scandinavia.  this recipe was found at website: mindspring.com - christian's danish recipes.                                                                                                                                                                                                                                                                                                                                                                                                                                             | ['eggs', 'milk', 'flour', 'sugar', 'salt', 'cream', 'apples', 'butter', 'cinnamon', 'lemon, juice of']                                     |              10 |            5 |
|  9 | lplermagrone  herdsman s macaroni       | 457136 |        40 |            65502 | 2011-05-23 00:00:00 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'cuisine', 'preparation', 'main-dish', 'side-dishes', 'pasta', 'european', 'swiss', 'pasta-rice-and-grains', 'elbow-macaroni']                                                                                                                                                |      708.6 |        14 | ['heat the oven to 100 c', 'boil potatoes in a saucepan without lid for 5 minutes', 'add macaroni and cook them al dente', 'until the liquid is almost absorbed', 'strain and return to pot', 'pour cream and muscat over the potatoes and macaroni , season to taste', 'alternating with cheese , place the macaroni in layers into a 2 litre dish', 'top with cheese', 'bake for approximately 10 minutes in the center of the preheated oven until the cheese has melted', 'optional onion ring topping:', 'melt the butter', 'mix onions and flour , shake off extra flour', 'fry in the butter at medium heat for about 5 minutes until crisp', 'place onions on paper towels and keep warm']                                                                                                                                                                           | basic ingredients for swiss alpine macaroni include potatoes, macaroni, cheese and onions. of course, there are several variations of this popular recipe, but no matter how it is prepared, this rustic delight, you just love it. muscat is a sweet or fortified white wine made from a muscat grape. mountain cheese (allgäuer bergkäse) is sometimes called the baby brother to emmentaler as it is eaten younger. it is made in the mountains in alpine dairy huts. i did not include the time for the optional onion ring topping as you can do it while cooking the main dish. enjoy! | ['potato', 'salt water', 'macaroni', 'heavy cream', 'muscat wine', 'black pepper', 'cheese', 'unsalted butter', 'onions', 'fine semolina'] |              10 |            5 |
| 10 | lplermagronen                           | 455351 |        55 |          1308592 | 2011-05-07 00:00:00 | ['60-minutes-or-less', 'time-to-make', 'preparation']                                                                                                                                                                                                                                                                                             |      651.8 |        15 | ['heat oven to 375f set a large pot of salted water to boil', 'heat butter / oil over medium-low heat in a frying pan', 'add onions and fry them until golden brown', 'add penne and potatoes to the salted water', 'stir to make sure pasta doesnt stick together', 'cook until tender , about 15 minutes', 'drain penne and potatoes', 'combine milk / cream with salt and pepper', 'in an ovenproof casserole dish , place 1 / 3 of the penne-potatoes , sprinkle with 1 / 2 of the grated cheese', 'make another layer with 1 / 3 of the penne-potatoes , sprinkle with the other 1 / 2 of the grated cheese', 'top with the remaining 1 / 3 of the penne-potatoes', 'pour the seasoned milk / cream evenly over the top', 'spread the browned onions on top', 'bake covered for 10-15 minutes until steaming hot and cheese is melted', 'serve with warmed applesauce'] | known as swiss mac n cheese, älplermagronen was traditionally a dish of peasant farmers  served with apple sauce. taken from growchew.wordpress.com and posted for zwt7                                                                                                                                                                                                                                                                                                                                                                                                                      | ['potato', 'penne pasta', 'onions', 'butter', 'cheese', 'milk', 'salt and pepper', 'applesauce']                                           |               8 |          nan |
| 11 | rter med flsk   pea soup with pork      | 333797 |       195 |            64642 | 2008-10-29 00:00:00 | ['time-to-make', 'course', 'main-ingredient', 'cuisine', 'preparation', 'occasion', 'north-american', '5-ingredients-or-less', 'soups-stews', 'beans', 'american', 'easy', 'beginner-cook', 'dietary', 'comfort-food', 'midwestern', 'inexpensive', 'free-of-something', 'taste-mood', 'savory', 'presentation', 'served-hot', '4-hours-or-less'] |      160.4 |         5 | ['soak peas overnight , drain and add 3 quarts water', 'bring to a boil and cook rapidly', 'skim off any skins', 'after cooking for an hour , add pork and simmer and simmer for 2 hours or until pork is tender', 'add seasonings']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | a hearty and comforting soup from the minnesota scandinavian chapter of the united states regional cookbook, culinary arts institute of chicago, 1947.  overnight soaking not included in preparation time.                                                                                                                                                                                                                                                                                                                                                                                  | ['dried yellow peas', 'water', 'salt', 'pork', 'ginger']                                                                                   |               5 |            5 |

### Univariate Analysis

This histogram shows the column 'n_ingredients'. It illustrates the total number of recipes with n number of ingredients. It is to be highlighted that this histogram is slightly skewed right, conveying that the majority of the recipes have between 2-16 ingredients in total.  

<iframe
  src="assets/univariate_analysis.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


### Bivariate Analysis

This scatterplot shows the columns 'calories' and 'n_ingredients' and their possible relationship. The plot illustrates how there are more recipes with lower calories, but also shows that higher-calories recipes tend to have a higher minimum ingredients used. It could be argued that the two columns have a slightly positive relationship, but it's not prominent.  

<iframe
  src="assets/bivariate_analysis.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Aggregates

This grouped table shows the mean calories and average rating based on the number of ingredients in a recipe. This graph entails an important connection between the three columns, alluding to the possibility of the columns being dependent columns. 

|   n_ingredients |   avg_rating |   calories |
|----------------:|-------------:|-----------:|
|               1 |      4.825   |    205.455 |
|               2 |      4.69343 |    202.887 |
|               3 |      4.66431 |    210.471 |
|               4 |      4.63967 |    234.057 |
|               5 |      4.64983 |    252.183 |
|               6 |      4.63227 |    274.539 |
|               7 |      4.62791 |    295.752 |
|               8 |      4.60912 |    313.73  |
|               9 |      4.60691 |    326.507 |
|              10 |      4.61245 |    335.397 |
|              11 |      4.6277  |    350.952 |
|              12 |      4.61569 |    362.189 |
|              13 |      4.63138 |    378.544 |
|              14 |      4.61153 |    390.683 |
|              15 |      4.63019 |    405.036 |
|              16 |      4.62639 |    421.105 |
|              17 |      4.62141 |    438.144 |
|              18 |      4.70006 |    444.472 |
|              19 |      4.61383 |    455.096 |
|              20 |      4.59164 |    460.509 |
|              21 |      4.65413 |    463.862 |
|              22 |      4.73628 |    479.471 |
|              23 |      4.78228 |    497.952 |
|              24 |      4.61029 |    515.653 |
|              25 |      4.7197  |    467.777 |
|              26 |      4.78796 |    497.104 |
|              27 |      4.89456 |    530.121 |
|              28 |      4.82692 |    478.164 |
|              29 |      4.96667 |    529.25  |
|              30 |      4.83889 |    554.09  |
|              31 |      5       |    402.94  |
|              32 |      5       |    363.1   |
|              33 |      5       |    338.2   |

### ASSESSMENT OF MISSINGNESS
### Not Missing At Random (NMAR) Analysis

There are three columns in the `recipe` data frame, `'name'`, `'description'`, and `'avg_rating'`, which could all possibly be Not Missing At Random (NMAR), assuming the following conditions:
- `'name'`: Users may choose not to provide a name if the recipe is simple or something very common. In this case, the missingness depends on the type of name the recipe would have had. 
- `'description'`: Similarly to the recipe names, users may choose not to describe if the recipe doesn't need any description due to its simplicity or self-explanatory. This makes the missingness depend on what would submitted to describe the recipe.
- `'avg_rating'`: People may have not rated the recipes, possibly due to not having tried them or having a negative experience. This makes the missingness tied to the user's unobserved actions, resulting in NMAR.

All three conditions rely on the idea that unobserved values explain why the data is missing, which is characteristic of NMAR.

### Missingness Dependency

I used permutation testing to evaluate whether the two columns, 'avg rating' and 'calories', are dependent on each other. Through the permutation testing, a p-value of 0.005994005994005994 is evaluated concluding that under a significance level of 0.05 the missingness of 'avg rating' may be dependent on the 'calorie' column. This is further elaborated through the graph showing that as calories increase the existence of missing values in comparison to non-missing values is more prevalent. 

<iframe
  src="assets/missingness_dependency.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### HYPOTHESIS TESTING
### Hypotheses

**Null Hypothesis:** The mean calories for low-rated recipes is greater than or equal to the mean calories for high-rated recipes.

**Alternative Hypothesis:** The mean calories for low-rated recipes is less than that of high-rated recipes.

### Test Method
A permutation test was conducted with the following steps:
- Recipes are split into 2 groups based on ratings: low-rated: < 3, high-rated: => 3
- Test Statistic: mean of low-rated - mean of high-rated
- Shuffling 1000 times
- Significance Level: 0.05

### Test Result
**Observed Mean Difference:** 0.7628970266521833

**p_value:** 0.036

**Reject or Fail to Reject:** Reject the null hypothesis

**Test Statistic:** Mean Difference 

**Significance Level:** 0.05

Since the p-value < significance level (0.05), we **reject the null hypothesis**. This provides evidence that low-rated recipes tend to have fewer calories than high-rated recipes. The observed difference is statistically significant and unlikely to be due to random chance. 

This test is appropriate because it allows me to compare the mean calories of two different groups without assuming any specific distribution of the data. It addresses whether the observed difference is statistically unusual, helping with my investigation about which types of recipes tend to have more calories. This shows the relationship between the two groups and possibly providing a partial solution to my investigative question!

### BASELINE MODEL

**Regression Type:** Linear Regression

**Features (BOTH QUANTITATIVE):** n_steps and n_ingredients

**Prediction:** Calories in a recipe

**Metric Used:** R²

**Metric Value:** 0.08897605083991178

This model is very simple and non-complicated, it allows for a very easy way to understand the relationship between the calories and the number of ingredients, and the number of steps taken. Although, this simplicity of the model fails to consider the possibility of having skewed data for the features - lacking of transformed and normalized data. It also strictly only includes linear features that are not scaled. The final model assumed to addresses these limitations and allow for a more robust model, but as a baseline model this model is suitable.

The baseline model has evaluated an R² value of 0.08897605083991178, which means that using the features in the model there about 8% of the data is being captured effectively to be useful on predicting values!

### FINAL MODEL

**Regression Type:** Lasso

**Features (2 QUANTITATIVE, 2 CATEGORICAL):** logn_steps, logn_ingredients, long_minutes, has_dairy

**Prediction:** Calories in a recipe

**Metric Used:** R²

**Metric Value:** 0.10916271694283142

I've started improving my model with engineering new features, I applied log n calculation for the columns n_steps and n_ingredients to normalize the data and counter any possible skewed data. Additionally, I've decided to binarize 2 categorical feature, has_dairy and long_minutes, it will be 1 if a recipe includes the following key words: milk, cheese, cream, and butter, and if a recipe takes more than 60 minutes to follow through, else it'll be 0. Engineering my final features took some time, as I created some features that didn't have much effect into the metric value and in some cases making it worse. These modifications attempts to tackle the issues I've discussed for my baseline model. 

Additionally, I followed the same process for the regression type trying several regressions, such as RandomForestClassifier and DecisionTreeRegression. However, these regressions did not calculate a metric value that was better than using Lasso. For this regression model, I decided to tune alpha and tol to regulize the data to prevent overfitting, and to ensure covergence occurs properly without any problems that can influence the result. The final model has evaluate an R² value of 0.10916271694283142, which is a 22.7% improvement compared to the baseline model. This does mean that this model captures about 11% of the data that is used to make predictions, which is still pretty small but shows an improvement from the baseline model through the modifications. 

### Fairness Analysis

**Group X:** Recipes with dairy products 

**Group Y:** Recipes without dairy products

**Null Hypothesis:** There is not difference between the R² of group x and group y

**Alternative Hypothesis:** There is a difference between the R² of group x and group y

**Metric:** R²

**Significance Level:** 0.01

The permutation test has gotten a p-value of 0.0775, which means the under the given conditions we fail to reject the null hypothesis. There is not enough evidence to conclude that it is wrong. Thus, my works similarly for both defined groups and that it will produce similar evaluatations for similar dataframes. 

