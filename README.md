# Naïve Bayes Classifier for NBA Players
# Table of contents

- [Background](#background)
- [The Statistics](#the-statistics)
- [Statistics Source](#statistics-source)
- [The methodology](#the-methodology)
- [Goal](#goal)
- [Usage](#usage)
- [Findings](#findings)
- [Predicting the 2020-21 NBA MVP](#predicting-the-2020-21-NBA-MVP)
- [Legality](#legality)
- [Source Files](#source-files)

## Background
As someone who has been playing basketball since the second grade and has been a Warriors fan since birth, the NBA and basketball in general has always held a special place in my heart. There are several questions in the world of basketball that will forever be debated such as: 
- Has basketball become a positionless sport, where you don't need to play the sport with the traditional point guard, shooting guard, small forward, power forward, and center?
- Who is the GOAT (greatest of all time)?
- Has the game really changed over the years?
- Do the numbers truly never lie? 

Using data and the Naïve Bayes approach to classification, I seek to find answers to these questions. Using a Naïve Bayes classifier, I will use statistics from nearly 19,000 players' seasons from 1980-2017. I will then test my classifier using statistics from the 2018-19 season (the most recent "normal" NBA season) and the current season's statistics to see if the numbers can answer any of the sport's burning questions.

[(Back to top)](#table-of-contents)

## The Statistics
The NBA tracks almost 50 different statistics for every player in the league. For the purposes of this project, I will only use statistics that must be greater than or equal to 0 since using Gaussian naïve Bayes only works for positive values. Additionally many of the statistics are dependent on each other, and for naïve Bayes to work, we must naïvely assume that the features (statistics) are independent. Furthermore, many statistics are often unknown to most basketball fans, so using only the common statistics will make the most sense for everyone. 
Here are some basic definitions of the statistics I will be using in my classifier:
- True shooting percentage (TS%): a metric that demonstrates how efficiently a player shoots the ball. Takes into consideration field goals, 3-pointers, and free throws (unlike other metrics like field goal percentage).
- Rebounds per game (RPG): a metric that shows how many total rebounds (both offensive and defensive) a player averages per game. 
- Assists per game (APG): a metric that shows how many total assists a player averages per game.
- Points per game (PPG): a metric that shows how many total points a player averages per game.
- Blocks per game (BPG): a metric that shows how many total blocks a player averages per game.
- Steals per game (SPG): a metric that shows how many total steals a player averages per game.

[(Back to top)](#table-of-contents)

## Statistics Source
The training data comes from [Kaggle](https://www.kaggle.com/drgilermo/nba-players-stats?select=Seasons_Stats.csv). The test data come from https://www.basketball-reference.com/.  

[(Back to top)](#table-of-contents)

## The Methodology:
This naïve Bayes classifier uses two different approaches. In one, I discretize the statistics, categorizing each statistic into their respective quartiles, and use the data with the traditional Bayes' Theorem:

P(class | features) = P(features | class) * P(class) / P(features)

In the other approach, I used the statistics as they are (continuous data) and used [Gaussian naïve Bayes](https://en.wikipedia.org/wiki/Naive_Bayes_classifier#Gaussian_na%C3%AFve_Bayes) which calculates a probability density for a parameter given a class.

In order to exercise what I have learned in my Data Science courses, I chose to implement these probability functions myself, but there are Python packages out there that do all the work for you!

Using the statistics above, I attempted to classify players': 
- All Star status: based on a player's season statistics, would we classify them as an All Star or not?
- Position: based on a player's season statistics, which position would we classify them as (guard, guard-forward, forward, forward-center, or center)?
- Decade: based on a player's season statistics, which decade would we classify them as (80s, 90s, 2000s, or 2010s)?
[(Back to top)](#table-of-contents)

## Goal
The goal of this project, along with my others, is to provide a fun and interesting way to practice my growing Data Science skills and to delve deeper into something I'm interested in. Additionally, I have sought out to answer some of the burning questions that are circulated amongst the basketball community!

[(Back to top)](#table-of-contents)

## Usage

Please refer to the [Jupyter Notebook viewer](https://nbviewer.jupyter.org/github/jacquelinekclee/naivebayes_nba_players/blob/main/naive_bayes_nba_players.ipynb) to view all the code used to make this project.

The [source files](#source-files) contain all the functions used to calculate the probabilities and clean/manipulate the data and DataFrames.

[(Back to top)](#table-of-contents)

## Findings
The classifier for All Star status had relatively high accuracy (determined by number of correct classifications / total number of classifications), but this is likely because only 20-30 players out of over 500 per season are all stars. Instead, I took the players who were most likely to be an All Star, which is defined by players whose probability of being an All Star were highest, and found how many I guessed correctly. For the 2018-19 season, I guessed 6/26 All Stars correctly, namely Kyrie Irving, Bradley Beal, DeMar DeRozan, Jimmy Butler, Klay Thompson, and Kemba Walker. For the 2020-21 season, I guessed 4/22 All Stars correctly, namely Jayson Tatum, Anthony Davis, Donovan Mitchell, and LeBron James.

The classifier for position only guessed correctly around 60-70% of the time. This could be some indication that position either doesn't matter all that much and is more trivial than some may think, or that a player's position goes beyond their statistic performance. I believe the latter is true, but also think that positionless basketball is definitely here to stay. 

The classifier for decade only guessed correctly around 30% of the time. This indicates that any sort of play style or typical stat line is characteristic of a certain decade. I think positions per game, other metrics that measure pace, the different types of shots attempted, points scored per game, and other statistics that measure how the game as a whole is played (not a player's performance) would be better statistics to try and classify gameplay by decade. 

[(Back to top)](#table-of-contents)
 
## Predicting the 2020-21 NBA MVP
The classifier predicts that the 5 players who are most likely to be the 2020-21 MVP are:
- LeBron James
- Kawhi Leonard
- Giannis Antetokounmpo
- Luka Dončic
- Jaylen Brown

## Source Files
* [probabilities.py](https://github.com/jacquelinekclee/naivebayes_nba_players/blob/main/probabilities.py)
  * Has all the functions used for calculate the naïve Bayes probabilities.
* [naivebayes_nba_players.py](https://github.com/jacquelinekclee/naivebayes_nba_players/blob/main/naivebayes_nba_players.py)
  * Has all the functions used to manipulate/clean the data/DataFrames so that they're ready for analysis.

## Legality
This personal project was made for the sole intent of applying my skills in Python thus far and as a way to learn new ones. It is intended for non-commercial uses only.

[(Back to top)](#table-of-contents)
