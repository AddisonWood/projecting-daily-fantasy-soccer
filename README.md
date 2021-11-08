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



## UPDATE 11/8/21
#### A lot of things have changed in the project recently.
#### &nbsp;&nbsp;&nbsp;&nbsp;- There are two lineup optimizers, one for Showdown contest, and one for Classic contests
#### &nbsp;&nbsp;&nbsp;&nbsp;- There is a file (`StatFilling.ipynb`) that scrapes FBRef, Odds Sites, and FiveThirtyEight to compile pre-game data automatically
#### &nbsp;&nbsp;&nbsp;&nbsp;- The stat predictions (Goals, shots, crosses, etc.) is done in an R markdown file (`R_StatPreds.Rmd`)
#### &nbsp;&nbsp;&nbsp;&nbsp;- There is a structured backtesting notebook too, to efficiently test new methods or contest structures

### Reccomended Workflow
#### &nbsp;&nbsp;&nbsp;&nbsp;1. Compile data using the `StatFilling.ipynb` file
#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- Data comes from OddsChecker.com, FBRef.com, and the `spi-matches-latest.csv` file downloaded from https://data.fivethirtyeight.com/ (Club Soccer Predictions)
#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- Data also previously came from OddsShark.com, but their model seems to have been broken for a couple weeks now
#### &nbsp;&nbsp;&nbsp;&nbsp;2. After a sufficient number of games have occured, use the R_StatPreds file to create stat predictions
#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- This markdown file cleans and prepares data for an ensemble regression, where the right combination of linear regression, decision trees, bagging, boosting, and random forest regression (found through K-fold cross validation) writes predictions (and RMSEs) to the `Regression_Matrices` directory.
