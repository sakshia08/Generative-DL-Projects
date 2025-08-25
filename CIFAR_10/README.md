### NOTES

- Image values = 0 to 255 -> preprocess to scale between 0 and 1
    - Better neural network if absolute value of each input < 1

1.	Load the data:
 	- x train = [5000, 32, 32, 3] - shape of the tensor (multi-dim array)
 	- 5000 = index of the image in the dataset
 	- 32, 32 = size of the image
 	- 3 = channel (all the images are RGB)
2. Scale the image -> 0 < pixel value < 1
3. One hot encode the integer labelled classes -> change to vectors
 	- if image belongs to 3rd class out of 4 classes - [0 0 1 0]
 	- initial size of ytrain = [5000, 1]
 	- after one hot encoding, the size of ytrain = [5000, 10]
4. Build up the MLP
 	- Structure of NN
 		1. Sequential - Quickly defining a linear stack where one layer follows directly from the previous layer without branching.
 		2. Functional API calls - Layer receives input from multiple preceding layers = more flexible
 
 	- After flattening the length of the vector = 3072 = (32x32x3).
 	- Softmax activation function in the final layer to ensure that the output is a set of 10 probabilities that sum to 1 which is the likelihood that the image belongs to each class.

- Generate the summary of the model - keras uses None as the marker for the first dimension to show that it doesn't yet know the number of observations that will be passed into the network.
