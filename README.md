# Formula 1 Result Predictor
**The goal of this project is to predict the top 10 points scorers in every race of the 2021 Formula 1 Season.**


## A quick introduction to Formula 1:
Formula 1 is one of the most popular and thrilling motorsport categories.  There are 20 drivers, 10 teams, so 2 drivers per team. There are 22 races in the 2021 Formula 1 Season. The race weekend starts on a Friday with Free Practice 1 & Free Practice 2, moves to Saturday with Free Practice 3 & Qualifying, and ends on Sunday, with the Grand Prix. For this project, I ignored all Free Practice results as they are not completely indicative of performance/pace. Qualifying is when drivers compete to set the fastest lap times, determining their starting positions on the grid for the race. Pole position means you start the race from 1st position. Each race is on a different circuit and the goal at the end of the season is to collect the most points and win the Championship. Only the drivers who are in the top 10 at the end of a Grand Prix will score points, with 1st place being awarded 25 points, 2nd place = 18 points, 3rd place = 15 points, down to 10th place = 1 point.

## Step 1: Data Collection/Preparation

The first step to this project is gathering historical Formula 1 data using [Ergast API](http://ergast.com/mrd/db/) CSV database tables. This provided me with the following features:

- Races 
- Results 
- Drivers
- Constructors
- Qualifying 
- Circuits
- Status

Through Wikipedia web scraping, I was able to gather weather information and merge it with the Races dataframe. Afterwards, I merged the other tables with the main dataframe, deleting columns that were not useful in our analysis and/or modeling. I also merged circuit type information (whether the circuit is a normal racing track or a street circuit) with the dataframe. 
## Step 2: Exploratory Data Analysis + some more processing

### Who has the most race wins?

The following chart compares the drivers and the number of race wins.

![Image](https://user-images.githubusercontent.com/100377723/256383117-d1f7f3bc-a8e3-4b36-9f1c-476638d14c3f.png)

### What is the pole-to-win ratio of the drivers?

The following chart compares the number of poles and the number of race wins.

![Image](https://user-images.githubusercontent.com/100377723/256383574-eedb9c8d-ceda-48a5-bf6a-fd88c90e09b5.png)

### What are the number of race wins of the drivers from outside of pole?

The following chart compares the race wins from outside of pole position.

![Image](https://user-images.githubusercontent.com/100377723/256383803-d261574d-da5d-48b8-b91c-66f50e1fc27d.png)

### What are the number of race wins on high altitude circuits?

The following chart compares the number of race wins on high altitude circuits.

![Image](https://user-images.githubusercontent.com/100377723/256383934-c1e604c6-5363-4395-91bf-68446f14b97d.png)

### Who is the "King of the Streets" in Formula 1?


The following charts compare the number of race wins on street circuits vs. normal racing tracks.

![Image](https://user-images.githubusercontent.com/100377723/256384511-a555afe6-4dd8-44a7-b2d9-899fdb75a8c9.png)



![Image](https://user-images.githubusercontent.com/100377723/256384526-4d5b3465-9301-471f-b333-2062d0854969.png)


Next, I decided to begin processing the columns in the dataframe, starting off with weather, then status, circuit, circuit info, race name, constructors, and lastly dealing with qualifying times. I deleted extra columns and cleaned some incorrect data.

## Step 3: Modeling

TRAIN - TEST SPLIT: the train set contains data from 2010 to 2020 inclusive. The test set consists of all data in the 2021 season.

I implemented a pipeline which scales the numeric features and applies various machine learning models. It then evaluates the models using metrics like accuracy, precision, and recall. The top 10 predictions for each round are displayed, along with their corresponding probabilities. I ran a bunch of models including, Logistic Regression, Support Vector Machines, Decision Tree Classifier, Random Forest Classifier, Neural Network Classifier, and XGB Classifier and saved the evaluations in a dataframe.

![Image](https://user-images.githubusercontent.com/100377723/256387678-3c4b2384-5712-40c3-805e-19088d4100f9.png)

The final model I chose was Random Forest Classifier. The final model function will display the top 10 predictions for each race in 2021, compared to the actual top 10 results. Additionally, the function calculates and displays the accuracy of the model based on correct predictions of top 10 finishers.  I also performed feature importance to detect which features contributed to a good result. 


![Image](https://user-images.githubusercontent.com/100377723/256389336-7e546b7c-869e-495c-a521-75425f11e6e0.png)

The predictions can be found in the file.

# Formula 1 Championship Dashboard
An interactive Tableau dashboard analyzing historical Formula 1 data.
This project joins multiple datasets to provide insights into driver and constructor performance, race locations, and trends over time.

## Dashboard Features

- **Wins by Driver:**  
  A bar chart showing the total number of race wins by each Formula 1 driver across the entire dataset.

- **Wins by Constructor:**  
  A bar chart summarizing the number of wins by each constructor (team), highlighting dominant teams in F1 history.

- **F1 Race Locations Map:**  
  A geographic map plotting all the circuits where Formula 1 races have taken place. Circle sizes indicate the number of races held at each circuit, and colors represent the country location.

- **Constructor Wins by Year:**  
  A multi-line chart showing how constructor dominance changed over time, illustrating trends and shifts in team performance season by season.

You can explore the interactive dashboard live on Tableau Public here:  
[View Dashboard on Tableau Public]([https://public.tableau.com/profile/your-profile#!/vizhome/your-dashboard](https://public.tableau.com/views/Book1_17535576644430/Dashboard1?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link))

## How to Use the Workbook

If you want to download and explore the Tableau workbook:

1. Download the `.twbx` file from this repository.  
2. Open it with [Tableau Desktop](https://www.tableau.com/products/desktop) or [Tableau Public](https://public.tableau.com/en-us/s/).


