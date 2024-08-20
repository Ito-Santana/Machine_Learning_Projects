# Kobe Bryant Shot Prediction

## Overview

This project aims to predict the success of Kobe Bryant's basketball shots based on historical data. Using machine learning techniques, we analyze various features to determine whether a shot will be made or missed. This repository contains code, data, and documentation related to the project.

## Project Structure

- `data.csv`: Contains datasets used in the project.
- `Kobe_Bryant_Shot_Selection.ipynb`: Jupyter notebook for exploratory data analysis and model training.
- `README.md`: This file.

## Data

The dataset used in this project includes information on Kobe Bryant's shots, such as location, distance, time remaining, and whether the shot was successful or not. The data can be found in the `data.csv` directory.

## Exploratory Data Analysis (EDA)

Exploratory Data Analysis (EDA) is a crucial step in understanding the dataset and uncovering patterns or insights that can inform model development. In this project, the EDA includes:

- **Shots per Year & Accuracy per Year**: 
  - Analyzed the number of shots and shooting accuracy by year. 
  - Noticed that Kobe Bryant's accuracy in championship years (2000, 2001, 2002, 2009, and 2010) was equal to or higher than his average accuracy.
  - Observed high accuracy in years when Kobe was the runner-up (2008 and 2006), indicating his crucial role in title contention during those seasons.

- **Relationship between Successful Shots and Court Position**:
  - Examined how the location on the court affects the success rate of shots.

- **Shots per Opponent**:
  - Analyzed the number of shots attempted against different opponents.

- **Shots to Time Remaining Ratio**:
  - Focused on shots taken with 6 seconds or less remaining on the clock, a critical moment for decision-making.
  - Found a correlation between shooting accuracy and the time remaining: Kobe Bryant's accuracy decreases as the time remaining gets shorter.

