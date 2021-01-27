# Extracting-sequences-in-computer-games-logs
Project for Development Workshop classes - model based on computer games logs.

## The dataset
![BIRAFFE2](https://zenodo.org/record/3865860#.XvjpwecwhPY)

## Current state:
- Event searching - will be used for HMM
- Stage visualization with event logs, example:

Map of stage 1. with scattered data on each participant's death.
![Stage1](/stage_1_deaths.jpg?raw=true "Map and data on deaths from stage 1")

Map of stage 2. with scattered data on each participant's death.
![Stage2](/stage_2_deaths.jpg?raw=true "Map and data on deaths from stage 2")


## References:
1. Rama, A. M., Rodriguez-Fernandez, V., & Camacho, D. (2020, April). Finding Behavioural Patterns Among League of Legends Players Through Hidden Markov Models. In International Conference on the Applications of Evolutionary Computation (Part of EvoStar) (pp. 419-430). Springer, Cham.

## Code Description

### Winning conditions section
This section was made to check for the best way to approach the winning condition. For each stage, the condition was set differently:
1. How fast the game was finished
2. How far did the person get

get_deaths/time/distance methods are searching for those values in logs. The loop beneath uses those functions to fill each stage's list of winning condition.

Next cells include GausianHMM model with the usage of those conditions. Unfortunately, the results are not satisfying enough.

### Events section
Cell 8th includes another approach - filling the lists of events, which are declared in later cells.

filter_logs - a method used for verifying the change in logs - if the value was changed -> an event happened. The event is then saved in a returning list.
get_event_coordinates - returns the position of a character for a particular event
get_coordinates_by_event_type - searches the logs for certain events and returns the list of coordinates from get_event_coordinates
read_map/draw_map/draw_stage_event - methods used for drawing the map. The maps are read from files in read_map, then drew with draw_map (the walls/floor of each map) and draw_stage_event (each coordinate of an event as a dot).
StageData class - contains data about map (parameters of graph, colors, shift etc).

Later in code there are examples of those usage with Bokeh library - images as above.

### HMM fitting section
This section contains last approach to the usage of HMM with events gathered from 1. stage. The hidden stages from this method are shown in cell 57th, and remodeled samples in 62nd cell. Unfortunately, this approach was not enough for the model to show any tendencies.

### Statistic analysis
In order to show the differences in data, a proper set of statistical methods were used. The gamelogs themselves were not put into the statistical analysis (yet?) because of their variety. The results are as follows:

Basic statistical values for personality traits and Valence/Arousal answers.
![statistics](/statistics.jpg?raw=true "Table of statistical values")

ANOVA of Valence/Arousal answers with personality types for each subject.

|                          |  sum_sq  |    df   |     F    | PR(>F) |
|:------------------------:|:--------:|:-------:|:--------:|:------:|
| Personality Type/Valence | 66476.35 |   15.0  | 11584.55 |   0.0  |
| Residual                 | 4204.7   | 10991.0 | Nan      | Nan    |
| Personality Type/Arousal | 41598.33 |   15.0  |  6741.44 |   0.0  |
| Residual                 | 4521.36  | 10991.0 | Nan      | Nan    |
