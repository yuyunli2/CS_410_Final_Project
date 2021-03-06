# CS_410_Final_Project

The documentation should consist of the following elements: 
1) An overview of the function of the code (i.e., what it does and what it can be used for). 
2) Documentation of how the software is implemented with sufficient detail so that others can have a basic understanding of your code for future extension or any further improvement. 
3) Documentation of the usage of the software including either documentation of usages of APIs or detailed instructions on how to install and run a software, whichever is applicable.  
4) Brief description of contribution of each team member in case of a multi-person team.  


## Purpose/ Function
This program is intended to help usese make better decisions about making recipes. It essentially provides two main uses.
  1) Evaluating a given recipe accorind the to uer's tastes
  2) Recommending a new recipe for the user based on user's preferences

This program will evaluate a recipe for a user based on the specific user's preferences. According to these proferences, this program can evaluate if a user will the the recipe is "good" or "bad" before even making the recipe. The intention of this functionality is to evaluate a specific recipes in which the user is interested. For example, the user may find a recipe online, but they aren't sure if they will like it. The use could simply enter the url into the program, and the program will be able to tell if the recipe is "good" or "bad" for that given user.

The recommendation functionality is slightly different. This functionality looks at the database or recipes within the program and finds the recipe that the user will most likely enjoy. For example, if a user can't decide what to make for dinner, the user can simply ask this program for a recommendation. The program will then output a title and associated url of the recipe that the use will enjoy.

Additionally, this program provides the ability for a user to udate preferences for different recipes within the database. Updating these preferences helps make the recipe evaluation and recommenation more accurate.


## Implementation

### Updating Preferences
Updating preferences is a relatively simple process. The user simply enters a url of the associated recipe and a rating (good or bad) for the recipe. The program then updates the pandas dataframe containing the prefences data. Addtionally the code overwrites the preferences.txt file, so the preferences can be saved for the next time the program runs.

### Evaluating a Recipe
Evaluating a recipe relies heavily on the functionality provides by scikitlearn text analysis features. The code essentially creates a classifier and trains the classifier according to the user's preferences. This classifier is then used to predict whether a recipe with no known preference will be good or bad. 

There are two primary components to creating the classifier - 1) the tfidf matrix and 2) the classifer itself. All data was transformed to a tfidf matrix based on unigrams and with english stopwords removed. This data was then used to train the multinomial Naive Bays classifier. These two components were then merged together utilizing a pipeline for ease of use. 

### Providing Recipe Reccomendation
Providing a recipe recommendation primarily utilizes a simmilarity function. All recipes were conveted to a tfidf matrix representation (unigram model with english stopwords removed). All recipes evalued a "good" by the user were compared to all recipes with no known preference. A consie similarity function was used to find which recipe without a preference was most similar recipes evalued as "good". The recipes with the highest avearege similarity to all "good" recipes is chosen as the recommendation.


## Software Documentation/ Overview of Functions:
Below is specific detail about how the program is implemented broken down by each funcition.

### def main_loop():
This function controls the flow of the program. It serves as the "main function". Initially it calls the "read_data()" function to read the raw recipe data scraped from the web. Then "main_loop()" calls "get_preferences()" to extracts the users preferences about the recipes in the database. Then "merge_data_pref()" is called to merge the raw recipe data scraped from the web with the user preferences into on pandas dataframe.

The "main_loop()" then enters into a loop to display the menu choices from the "menu_choise()" function. According the to the user input, the "main_loop()" will then enter to the appropriate function associated with the user's input. The user can choose to do any of the following:
  1) Update user's preferences about recipes in the database as either a "good" or "bad" recipe
  2) Evaluet a recipe for which the user has no known preference and classify it as being a "good" or "bad" recipe
  3) Get a recipe recomendation of a recipe for which the user has no known preference



### def menu_choice():
This function dispalys the main menu and takes the user's input.

### def recipe_rec(df):
This function provides a recipe recomendation for the users. The recommendation will be a recipe for which the users has not entred a preference. The recommended recipe title and url will be printed. This function takes the merged data and preferences pandas dataframe and returns None.

### def get_classifier(df):
The function is used by the "evaluate_recipe()" function to return a pipeline object. The merged pandas datafram is passes as an input to the fuction. This fuction then creates a pipeline to transform data into a tfidf matrix then classify it according the a multinomial Naive Bayes classifier. This function primarily relies on functionality from the scikitlearn python library.

### def evaluate_recipe(df):
This function evaluates a recipe by predicted that it will be either "good" or "bad" according the the user's preferences. This function takes asks the user to input a url of a recipe (url's must be already scraped and loaded into the database). This function then calls the "get_classifier()" function to get a multinomial Naive Bayes classifier trained on the tfidf transformed preferenes the user had previous defined. Using this classifier, this function will predicted whether the input url would be a good of bad recipe.

### def update_preferences(df):
This function allows the user to update prefrenes about recipes in the database. The user will entere a url and a rating (good or bad). This function then updates the preference values in the database and writes all new preferences to the preferences.txt file.

### def merge_data_and_pref(df, pref):
The function merged the pandas dataframes created in "get_preferences()" and in "read_data()" into one pandas dataframe.

### def get_preferences(df):
This function extracts the user preferences from the preferences.txt file. If this file does not exist, this function will create a new preferences.txt file initialized with "NULL" values for all preferences. Data extratacted from preferences.txt is then converted to a pandas dataframe and returnted by this function.

### def read_data():
This function reads the raw data .txt files containing the scraped recipe data. The .txt data files were created using a web crawler and scraper to extract recipe data. This data was then converted to .txt files. This function extracts all this data and converted it to a pandas dataframe, which this function returns.


## Usage/ Installation

Using this program is very simple. Simply download all files and store in the same directory. Please note the README.md and clearn_url_list.txt are not stictly needed to run the program. 

cleanr_url_list.txt provides a list of all url's included in the database. These are the only url's that the program can use for any functionality. YOu can use this file for testing and running the program when it is required for the user to input a url.

After downloading the program, this application should should be run as a command prompt interfact. Simply run this program from your command promt window using the following command:
  
   python final_project_main.py
   
The program should run and the user can simply follow the on-screen prompts. The user can navigate the program through the menu options displayed. Note that the user should enter "q" on the main menu to quite the program.

The main menu presents the user with the following opitons:

    1) Update preferences
    2) Evaluate a recipe
    3) Get a recipe reccomendation
    q) Quit
    
The user simply enters the correspoing menu choice (1, 2, 3, or q) to navigate to the proper functions in this application.

## Team contributions

John LaVanne dcontributions:
  - Invented project idea
  - Wrote project proposal
  - Scraped all web recipe data
  - Transformed data into .txt files
  - Write all program code
  - Wrote program documentation
