# DL4NLP
Various NLP use cases and problems solved using LSTM, GRUs in Keras

RNNs in Python
How to build the different kinds of RNNs:

 

First, let's look at how to build a vanilla RNN in Keras.

# import libraries
from keras.models import Sequential
from keras.layers import Dense
from keras.layers import SimpleRNN

# define parameters
n_output = # number of classes in case of classification, 1 in case of regression
output_activation = # “softmax” or “sigmoid” in case of classification, “linear” in case of regression

# ---- build RNN architecture ----

# instantiate sequential model
model = Sequential()

# add the first hidden layer
n_cells = #number of neurons to add in the hidden layer
time_steps = # length of sequences
features = # number of features of each entity in the sequence

model.add(SimpleRNN(n_cells, input_shape=(time_steps, features)))

# add output layer
model.add(Dense(n_output, activation=output_activation)

 

Let's look at how to build a many-to-one architecture in Keras.

# import libraries
from keras.models import Sequential
from keras.layers import Dense
from keras.layers import SimpleRNN

# define parameters
n_output = # number of classes in case of classification, 1 in case of regression
output_activation = # “softmax” or “sigmoid” in case of classification, “linear” in case of regression

# instantiate model
model = Sequential()

# time_steps: multiple input, that is, one input at each timestep
model.add(SimpleRNN(n_cells, input_shape=(time_steps, features)))

# single output at output layer
model.add(Dense(n_classes, activation=output_activation))

 

Let's look at how to build a many-to-many (with equal length of input and output sequences) architecture in Keras.

# instantiate model
model = Sequential()

# time_steps: multiple input, that is, one input at each timestep
model.add(SimpleRNN(n_cells, input_shape=(time_steps, features)))

# TimeDistributed(): This function is used when you want your neural network to provide an output at each timestep which is exactly what we want in the many-to-many RNN model.
model.add(TimeDistributed(Dense(n_classes, activation=output_activation)))

 

Next, let's look at how to build an encoder-decoder architecture in Keras.

# instantiate model
model = Sequential()

# encoder with multiple inputs	
model.add(LSTM(n_cells_input, input_shape=(input_timesteps, ...)))

# encoded sequence	
model.add(RepeatVector(output_timesteps))
		
model.add(LSTM(n_cells_output, return_sequences=True))

# TimeDistributed(): multiple outputs at the output layer
model.add(TimeDistributed(Dense(n_classes, activation=output_activation)))

 

Let's look at how to build a one-to-many RNN in Keras.

# instantiate model
model = Sequential()

# time_steps is one in this case because the input consists of only one entity
model.add(SimpleRNN(n_cells, input_shape=(1, features)))

# TimeDistributed(): multiple outputs at the output layer
model.add(TimeDistributed(Dense(n_classes, activation=output_activation)))

Here is a code snippet on how to use bidirectional RNNs in Keras.

# instantiate model
model = Sequential()

# bidirectional RNN layer
model.add(Bidirectional(SimpleRNN(n_cells, input_shape=(time_steps, features))) 

# output layer
model.add(Dense(n_classes, activation = output_activation))

 

Let's see how to build LSTM networks in Keras.

# import LSTM layer
from keras.layers import LSTM

# instantiate model
model = Sequential()

# replace the SimpleRNN() layer with LSTM() layer
model.add(LSTM(n_cells, input_shape=(time_steps, features)))

# output layer
model.add(Dense(n_classes, activation=output_activation))

 

Let's see how to build GRU networks in Keras.

# import LSTM layer
from keras.layers import GRU

# instantiate model
model = Sequential()

# replace the LSTM() layer with GRU() layer
model.add(GRU(n_cells, input_shape=(time_steps, features)))

# output layer
model.add(Dense(n_classes, activation=output_activation))