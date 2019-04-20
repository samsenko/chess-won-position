# Chess Won Position Predictor

## Summary
This repository contains code to train and use a model which predicts the result of a chess game given a position 
(expressed in Forsyth-Edwards Notation). Additionally, the current model provides the user with a "score" representing
the predicted expected number of points earned by white where a win earns 1 point, a draw earns 0.5 points and a loss earns 0 points.
The model is currently implemented as a random forest classifier with 1000 estimators. There is an additional option to use a 
gradient boosting classifier.

## Model Performance
The model was trained and tested on data consisting primarily of positions within 10 plies of either a draw by agreement or resignation
in a high-level chess game (very few of the datapoints proceed all the way to a draw or checkmate). Empirically testing a few datapoints
with Stockfish suggests that, in most datapoints which don't correspond to draws, the winning side has an advantage ranging roughly from 3 
pawns to mate in approximately 15.

With these caveats, the model is currently able to accurately predict the result 69% of the time on unseen test data. More specifically, 
the model predicts wins by white with accuracy of 77%, draws with accuracy of 61% and wins by black with accuracy of 69%. The best overall accuracy on the model using a gradient boosting classifier is 66%.

To better assess the performance of the model, it was also tested using 10-fold cross validation on the train data. This saw a mean accuracy score of 73% and a 95% confidence interval of 73% +/- 5%. A paired student's T-Test was used to compare this model to two simpler models: randomly guessing and predicting based entirely off of material advantage. We found very strong evidence that our model significantly outperforms both of these simpler models (p < 0.001 for both of them). This suggests that our model is capable of taking into account both the material of both sides as well as the strength of each side's position. 

## Files in this Repository
The actual training and evaluation of the model is contained in the Jupyter Notebook entitled 
Chess_Won_Position.ipynb. This notebook also contains a function called predict_result which takes as input a 
string containing a position in FEN notation and prints the predicted outcome as well as the score. The input data is contained in the file chess_fens3.txt. The targets are contained in the text file chess_results2.txt. 

## Future Work
Based off of our tests, it appears that the model could be further improved by increasing the amount of data the model is trained on. Additionally, it would be interesting to use the model as the basis for a chess-playing AI (for example by using Monte Carlo tree search using this model applied to a possible position combined with the similarity of this position to previously explored positions and the average result of searches going through this position to select moves during the search).

## External Links
The data used is originally from http://www.chessgames.com/.

