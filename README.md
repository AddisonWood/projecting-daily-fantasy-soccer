# projecting-daily-fantasy-soccer

### This repository contains a exploration and testing file, as well as a framework to create optimal lineups for soccer Showdown-style DraftKings contests.

### Lineup_Optimizer.ipynb
#### This is the main framework for generating an optimal lineup
#### It utilizes StatsBomb event data scraped from FBRef, as well as odds hand-compiled from OddsChecker, OddsShark, and FiveThirtyEight.

### XGBoost_Testing.ipynb
#### The model is dependent of projected goals, shots, and shots on target.
#### This notebook contains the testing to determine whether the simple linear regression or ensemble-based XGBoost performs better on the given dataset.
#### Future addition to this notebook will include a Poisson-based projection model to more accurately project goals scored.

### DK_Point_Shares.ipynb
#### This short notebook is a brief exploration into the share of fantasy points scored for each fantasty-point-scoring event in each of the top 5 European leagues, as well as MLS.

##
##


## UPDATE 11/8/21
### A lot of things have changed in the project recently.
#### &nbsp;&nbsp;&nbsp;&nbsp;- There are two lineup optimizers, one for Showdown contest, and one for Classic contests
#### &nbsp;&nbsp;&nbsp;&nbsp;- There is a file (`StatFilling.ipynb`) that scrapes FBRef, Odds Sites, and FiveThirtyEight to compile pre-game data automatically
#### &nbsp;&nbsp;&nbsp;&nbsp;- The stat predictions (Goals, shots, crosses, etc.) is done in an R markdown file (`R_StatPreds.Rmd`)
#### &nbsp;&nbsp;&nbsp;&nbsp;- There is a structured backtesting notebook too, to efficiently test new methods or contest structures
##
### Reccomended Workflow
#### 1. Compile data using the `StatFilling.ipynb` file
##### - Data comes from OddsChecker.com, FBRef.com, and the `spi-matches-latest.csv` file downloaded from https://data.fivethirtyeight.com/ (Club Soccer Predictions)
##### - Data also previously came from OddsShark.com, but their model seems to have been broken for a couple weeks now
#### 2. After a sufficient number of games have occured, use the R_StatPreds file to create stat predictions
##### - This markdown file cleans and prepares data for an ensemble regression, where the right combination of linear regression, decision trees, bagging, boosting, and random forest regression (found through K-fold cross validation) writes predictions (and RMSEs) to the `Regression_Matrices` directory.
#### 3. Download the salary data for the desired competition from DraftKings (save to the correct league subdirectory in the `DK_Salaries` directory)
##### - The filename convention is `{home_abbrev}_{away_abbrev}_{yyyymmdd}_Salaries.csv`. This convention is used for almost every single-game file
#### 4. Go to the correct Lineup Optimizer notebook, and enter fill it out down to where the matchup spreadsheet is output
#### 5. Open the matchup spreadsheet (found in the correct league subdirectory in the `Matchup_Spreadsheets` directory) and denote the starters with 'y' and the bench players with 'b'
##### - Make sure that if a starter has no start_mins, fill that cell with an educated guess
##### - If a bench player does not have sub_mins listed, do not put a 'b' for them
##### 6. Continue with the Lineup Optimizer, creating the regressions and reading the stat predictions, and then reading in the matchup spreadsheet to create a `...matchup_spreadsheet_finished.csv` file;
##### 7. Now that there are predicted points, run the optimizer to generate the best legal linups, and save the top selection of those out to the `Generated_Lineups` directory.
##### 8. After the contest is over, export the .csv of the results from DraftKings, and save to the correct league subdirectory in the `DK_standings` directory.
##### 9. After the xG data from the game is released on FBRef, fill out the PlayerPointsAnalysis2.csv file with the pre-game data and the FBRef matchreport url, which can then be scraped before later games to get the real fantasy points - used to create those player-level regressions.
##### 10. Once the data is in PlayerPointsAnalysis2.csv, and a few games have occurred, now you can enter and follow the `Backtesting_notebook.ipynb` file to start backtesting
