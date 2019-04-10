# Chess Won Position Predictor

## Summary
This repository contains code to train and use a model which predicts the result of a chess game given a position 
(expressed in Forsyth-Edwards Notation). Additionally, the current model provides the user with a "score" representing
the predicted expected number of points earned by white where a win earns 1 point, a draw earns 0.5 points and a loss earns 0 points.
The model is currently implemented as a random forest classifier with 1000 estimators. There is an additional option to use a 
gradient boosting classifier.

## Current Performance and Caveats
The model was trained and tested on data consisting primarily of positions within 10 plies of either a draw by agreement or resignation
in a high-level chess game (very few of the datapoints proceed all the way to a draw or checkmate). Empirically testing a few datapoints
with Stockfish suggests that, in most datapoints which don't correspond to draws, the winning side has an advantage ranging roughly from 3 
pawns to mate in approximately 15.

With these caveats, the model is currently able to accurately predict the result 67% of the time on unseen test data. More specifically, 
the model predicts wins by white with accuracy of 79%, draws with accuracy of 61% and wins by black with accuracy of 62%. The most common
misclassification is a draw classified as a win by white which occurs in 25% of positions drawn. The best overall accuracy on the
model using a gradient boosting classifier is also 67%.

## Files in this Repository
The actual training and evaluation of the model is contained in the Jupyter Notebook entitled 
Chess_Won_Position.ipynb. This notebook also contains a function called predict_result which takes as input a 
string containing a position in FEN notation and prints the predicted outcome as well as the score. The input features of the training and 
test data is contained in the text file chess_fens3.txt. The target features of the training and test data is contained in the text file 
chess_results2.txt. 

## External Links
The data used is originally from http://www.chessgames.com/.

