## Convert PGN-string into vector:

The code processes a list of chess moves from a file, simulates the course of the game and saves the resulting board states in a CSV file. Each chessboard is converted into a numerical vector form that can be used for machine learning.
First, a chessboard is implemented as a data structure:
![image](https://github.com/user-attachments/assets/dafa72e7-3be9-4b41-8a9b-388d0a97e709)

It consists of an 8×8 matrix in which empty squares are represented by dots and chess pieces by their respective characters. In addition, the player whose turn it is is recorded. The board is converted into a numerical representation by assigning numerical values to the individual pieces. A white pawn is coded as -1 and a black pawn as 1, while the current player is stored as additional information (0 for white, 1 for black):
![image](https://github.com/user-attachments/assets/eed2e9fe-9727-41ef-9df8-142f0995cbb8)

The processing of the moves begins by reading in a text file containing a sequence of chess moves. These moves are analyzed and interpreted according to defined rules. For each move, the corresponding piece is placed on the virtual chessboard, ensuring that black and white are correctly distinguished. After each move, the current board state is converted into a number vector and written to a CSV file. The game result is also saved, reflecting either a win for White (1-0), a win for Black (0-1) or a draw.
During processing, the system checks whether the moves are valid. If an invalid move occurs, a warning is issued. The end result is a CSV file containing a numerical representation for each board, supplemented by the final game result. This data structure could be used for machine learning, for example, to recognize patterns in chess games or to train an AI.

## Training AI: 

The given code implements a neural network to classify chess games based on a CSV file with game information. First, the necessary libraries are imported, including pandas for data processing, scikit-learn for splitting the data and converting the labels, tensorflow.keras for creating and training the model, and matplotlib and networkx for visualization.
The data is loaded from a CSV file, whereby the column with the labels (Label:1-0) is separated from the input features (X). The target values (y) are then converted into numerical categories and converted into one-hot format to make them usable for the neural network. The data is then split into a training set and a test set.
The neural network is created using the Keras Sequential API. It consists of an input layer based on the number of input features, two hidden layers with 64 and 32 neurons respectively, and an output layer whose size corresponds to the number of classification possibilities. The activation function in the hidden layers is ReLU, while softmax is used in the output layer to generate probabilities for the different classes. The model is compiled with the categorical_crossentropy loss function and the adam optimizer.
When training the model, an early stopping mechanism is used, which automatically terminates the training if the validation loss values do not improve over several epochs. After training, the model is saved and then reloaded to make predictions on the test dataset.
Finally, the networkx library is used to create a directed graph that visualizes the structure of the neural network. 
![image](https://github.com/user-attachments/assets/dc44d258-3500-4470-8156-58b5e66a4a95)

The neurons of the different layers are shown as nodes and the connections between them as weighted edges. A commented-out code section also shows a way to visualize the connections in color.

## Prediction based on trained model

The code loads a previously trained neural network to make predictions about the outcome of chess games. New game data is read in from a CSV file and a prediction is made for each game.

First, the saved model my_model.h5, which was previously trained, is loaded. New game data is then imported from the chess_data4.csv file, whereby the Label:1-0 column is removed as it contains the actual results and is not required for the prediction.

A LabelEncoder is created to encode the possible prediction classes (black or white). A prediction is then made for each game in the data: The model receives a single line of the game data as input and outputs a probability distribution for the possible outcomes. The most probable value is determined and translated back into the corresponding player color (black or white) using the LabelEncoder.

In addition, the system checks which player's turn it is. This is done using the penultimate column of the data set, with a value of 0 indicating a white player and 1 indicating a black player. Finally, the predicted result and the probabilities of the various options are output.

The code therefore makes it possible to predict the outcome of individual games and provides an assessment based on the data provided.
