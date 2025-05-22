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

   To prevent any outlandish statistics, I've decided to filter the recipe data frame to only include recipes with less than 3,000 calories to adhere to realistic 1-serving sizes. Since some of the recipes have calories to the hundreds of thousands, there could be user error when inputting values and/or too big of serving sizes. The primary goal is to prevent extreme data from heavily skewing the analysis results.

This is how the resulting data frame that will be used for analysis will look like!

| name                                 |     id |   minutes |   contributor_id | submitted           | tags                                                                                                                                                                                                                                                                                               |   calories |   n_steps | steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | description                                                                                                                                                                                                                                                                                                                                                                       | ingredients                                                                                                                                                                                                                             |   n_ingredients |   avg_rating |
|:-------------------------------------|-------:|----------:|-----------------:|:--------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------:|----------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|-------------:|
| 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27 00:00:00 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings']                                                                        |      138.4 |        10 | ['heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes', 'remove from the oven and cool completely before cutting']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                            | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour']                                                      | 9 | 4 |
| 1 in canada chocolate chip cookies | 453467 |45 |1848091 | 2011-04-11 00:00:00 | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']| 595.1 | 12 | ['pre-heat oven the 350 degrees f', 'in a mixing bowl , sift together the flours and baking powder', 'set aside', 'in another mixing bowl , blend together the sugars , margarine , and salt until light and fluffy', 'add the eggs , water , and vanilla to the margarine / sugar mixture and mix together until well combined', 'add in the flour mixture to the wet ingredients and blend until combined', 'scrape down the sides of the bowl and add the chocolate chips', 'mix until combined', 'scrape down the sides to the bowl again', 'using an ice cream scoop , scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking', 'bake for 10 - 15 minutes or until golden brown on the outside and soft & chewy in the center', 'serve hot and enjoy !']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                                                                             |              11 |            5 |
| 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30 00:00:00 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                                                                                               |      194.8 |         6 | ['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']                                                                   |               9 |            5 |
| millionaire pound cake               | 286009 |       120 |           461724 | 2008-02-12 00:00:00 | ['time-to-make', 'course', 'cuisine', 'preparation', 'occasion', 'north-american', 'desserts', 'american', 'southern-united-states', 'dinner-party', 'holiday-event', 'cakes', 'dietary', 'christmas', 'thanksgiving', 'low-sodium', 'low-in-something', 'taste-mood', 'sweet', '4-hours-or-less'] |      878.3 |         7 | ['freheat the oven to 300 degrees', 'grease a 10-inch tube pan with butter , dust the bottom and sides with flour , and set aside', 'in a large mixing bowl , cream the butter and sugar with an electric mixer and add the eggs one at a time , beating after each addition', 'alternately add the flour and milk , stirring till the batter is smooth', 'add the two extracts and stir till well blended', 'scrape the batter into the prepared pan and bake till a cake tester or knife blade inserted in the center comes out clean , about 1 1 / 2 hours', 'cool the cake in the pan on a rack for 5 minutes , then turn it out on the rack to cool completely']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | why a millionaire pound cake?  because it's super rich!  this scrumptious cake is the pride of an elderly belle from jackson, mississippi.  the recipe comes from "the glory of southern cooking" by james villas.                                                                                                                                                                | ['butter', 'sugar', 'eggs', 'all-purpose flour', 'whole milk', 'pure vanilla extract', 'almond extract']                                                                                                                                |               7 |            5 |
| 2000 meatloaf                        | 475785 |        90 |          2202916 | 2012-03-06 00:00:00 | ['time-to-make', 'course', 'main-ingredient', 'preparation', 'main-dish', 'potatoes', 'vegetables', '4-hours-or-less', 'meatloaf', 'simply-potatoes2']                                                                                                                                             |      267   |        17 | ['pan fry bacon , and set aside on a paper towel to absorb excess grease', 'mince yellow onion , red bell pepper , and add to your mixing bowl', 'chop garlic and set aside', 'put 1tbsp olive oil into a saut pan , along with chopped garlic , teaspoons white pepper and a pinch of kosher salt', 'bring to a medium heat to sweat your garlic', 'preheat oven to 350f', 'coarsely chop your baby spinach add to your heated pan , stir frequently for approximately 5 min to wilt', 'add your spinach to the mixing bowl', 'chop your now cooled bacon , and add it to the mixing bowl', 'add your meatloaf mix to the bowl , with one egg and mix till thoroughly combined', 'add your goat cheese , one egg , 1 / 8 tsp white pepper and 1 / 8 tsp of kosher salt and mix till thoroughly combined', 'transfer to a 9x5 meatloaf pan , and cook for 60 min or until the internal temperature is at least 160f', 'let stand for 5min', 'melt 1tbsp unsalted butter into a frying pan , and cook up to three eggs at a time', 'crack each egg into a separate dish , in order to prevent egg shells from reaching the pan , then add salt and pepper to taste', 'wait until the egg whites are firm looking , but slightly runny on top before flipping your eggs', 'after flipping , wait 10~20 seconds before removing each egg and placing it over your slices of meatloaf'] | ready, set, cook! special edition contest entry: a mediterranean flavor inspired meatloaf dish. featuring: simply potatoes - shredded hash browns, egg, bacon, spinach, red bell pepper, and goat cheese.                                                                                                                                                                         | ['meatloaf mixture', 'unsmoked bacon', 'goat cheese', 'unsalted butter', 'eggs', 'baby spinach', 'yellow onion', 'red bell pepper', 'simply potatoes shredded hash browns', 'fresh garlic', 'kosher salt', 'white pepper', 'olive oil'] |              13 |            5 |

### Univariate Analysis

This histogram shows the column 'n_ingredients'. It illustrates the total number of recipes with n number of ingredients. It is to be highlighted that this histogram is slightly skewed right, conveying that the majority of the recipes have between 2-16 ingredients in total.  

<iframe
  src="assets/univariate_analysis.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


### Bivariate Analysis

This scatterplot shows the columns 'calories' and 'avg_rating' and their possible relationship. The plot illustrates how there are more recipes with lower calories, but also shows that lower-calorie recipes tend to have a higher average rating. 

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
    |               1 |      4.84091 |    274.892 |
    |               2 |      4.69218 |    293.149 |
    |               3 |      4.6617  |    269.191 |
    |               4 |      4.635   |    302.728 |
    |               5 |      4.64801 |    315.093 |
    |               6 |      4.63372 |    333.853 |
    |               7 |      4.6244  |    359.882 |
    |               8 |      4.61156 |    371.035 |
    |               9 |      4.60677 |    388.246 |
    |              10 |      4.60962 |    403.908 |
    |              11 |      4.62298 |    421.177 |
    |              12 |      4.61649 |    438.115 |
    |              13 |      4.6295  |    450.508 |
    |              14 |      4.61592 |    470.459 |
    |              15 |      4.62996 |    502.315 |
    |              16 |      4.6239  |    520.949 |
    |              17 |      4.63381 |    518.085 |
    |              18 |      4.69814 |    577.912 |
    |              19 |      4.61002 |    561.571 |
    |              20 |      4.61112 |    601.364 |
    |              21 |      4.67578 |    590.381 |
    |              22 |      4.69771 |    624.568 |
    |              23 |      4.77604 |    638.468 |
    |              24 |      4.5991  |    660.004 |
    |              25 |      4.70721 |    764.605 |
    |              26 |      4.7689  |    622.211 |
    |              27 |      4.59199 |    825.841 |
    |              28 |      4.85924 |    621.7   |
    |              29 |      4.9619  |    886.3   |
    |              30 |      4.86818 |    655.033 |
    |              31 |      5       |    760.688 |
    |              32 |      5       |    697.35  |
    |              33 |      5       |    338.2   |

### ASSESSMENT OF MISSINGNESS
### Not Missing At Random (NMAR) Analysis

There are three columns in the `recipe` data frame, `'name'`, `'description'`, and `'avg_rating'`, which could all possibly be Not Missing At Random (NMAR), assuming the following conditions:
- `'name'`: Users may choose not to provide a name if the recipe is simple or something very common. In this case, the missingness depends on the type of name the recipe would have had. 
- `'description'`: Similarly to the recipe names, users may choose not to describe if the recipe doesn't need any description due to its simplicity or self-explanatory. This makes the missingness depend on what would submitted to describe the recipe.
- `'avg_rating'`: People may have not rated the recipes, possibly due to not having tried them or having a negative experience. This makes the missingness tied to the user's unobserved actions, resulting in NMAR.

All three conditions rely on the idea that unobserved values explain why the data is missing, which is characteristic of NMAR.

### Missingness Dependency

I used permutation testing to evaluate whether the two columns, 'avg rating' and 'calories', are dependent on each other. Through the permutation testing, a p-value of 0.000999000999000999 was evaluated concluding that under a significance level of 0.05 the missingness of 'avg rating' is dependent on the 'calorie' column. This is further elaborated through the graph showing that as calories increase there are a lot more average rating values missing.

<iframe
  src="assets/missingness_dependency.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### HYPOTHESIS TESTING

### Hypotheses

Null Hypothesis: The mean calories for low-rated recipes is greater than or equal to the mean calories for high-rated recipes.

Alternative Hypothesis: The mean calories for low-rated recipes is less than that of high-rated recipes.

### Test Method
A permutation test was conducted with the following steps:
- Recipes are split into 2 groups based on ratings: low-rated: < 3, high-rated: => 3
- Test Statistic: mean of low-rated - mean of high-rated
- Shuffling 1000 times
- Significance Level: 0.05

### Test Result
Observed Mean Difference: 0.7628970266521833
p_value: 0.538
Reject or Fail to Reject: Fail to reject the null hypothesis

Since the p_value > significance level, there is no statistical significance to suggest that low-rated recipes have fewer calories than high-rated recipes. Any difference in calories happened by chance and is unlikely to reflect accurate real events. 

The test statistic for this test is the mean difference between the mean calories for low-rated recipes and the mean calories for high-rated recipes and a significance level of 0.05.

This test is appropriate because it allows me to compare the mean calories of two different groups without assuming any specific distribution of the data. It addresses whether the observed difference is statistically unusual, helping with my investigation about which types of recipes tend to have more calories. This shows the relationship between the two groups and possibly providing a partial solution to my investigative question!
