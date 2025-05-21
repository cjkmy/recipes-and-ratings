# Recipes and Rating 🍽️

## Investigation Question: What types of recipes tend to have the most calories?

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
<br>
2. `interactions.csv`: a DataFrame that consists of information regarding people's reviews of certain recipes with 4 columns, indexed by user_id:

   - `recipe_id`: a series of numbers serving as identification that differentiates each recipe
   - `date`: the data of the review being sent formatted as MM/DD/YYYY
   - `rating`: a rating out of 5 for the recipe
   - `review`: comments made by the reviewer about the recipe
