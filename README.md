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
#### -There are two lineup optimizers, one for Showdown contest, and one for Classic contests
#### -There is a file (StatFilling.ipynb) that scrapes FBRef, Odds Sites, and FiveThirtyEight to compile pre-game data automatically
#### -The stat predictions (Goals, shots, crosses, etc.) is done in an R markdown file (R_StatPreds.Rmd)
#### -There is a structured backtesting notebook too, to efficiently test new methods or contest structures
