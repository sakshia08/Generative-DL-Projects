### NOTES

- Image values = 0 to 255 -> preprocess to scale between 0 and 1
   ** - Better neural network if absolute value of each input < 1
**
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
 		2. Functional API calls - Layer receives input from multiple preceding layers = more **flexible**
 
 	- After flattening the length of the vector = 3072 = (32x32x3).
 	- Softmax activation function in the final layer to ensure that the output is a set of 10 probabilities that sum to 1 which is the likelihood that the image belongs to each class.

- Generate the summary of the model - **keras uses None as the marker for the first dimension to show that it doesn't yet know the number of observations that will be passed into the network.**
  5. Loss Function and optimisers - adam optimiser (most stable) and categorical crossentropy loss function

- So far no data has been shown to the model -> just set up the architecture and compiled the model
- To train against data = call fit method
      - while fitting we gave (xtrain = raw image data, ytrain = one hot encoded class labels, batch size(how many obs will be passed to the network at each training step, epochs (how many times the network will be shown the full training data), shuffle = batches drawn randomly without replacement from the training data at each step).

  - First the weights of the network are initialised to small random values then the network performs series of training steps. At each step, one batch of images is passes thru the network and the errors are back propagated to update the weights.
  -** The larger the batch size, the more stable the gradient calculation.**
  - This continues until all the observations in the dataset have been seen once. This completes the first epoch.
 
  After testing the model we can predict on the test set using the predict method
      - preds is an array of shape [10000, 10] i.e., a vector of 10 class probabilities for each observation
      - we convert this array of probabilies back into a single prediction using numpy's **argmax function**. axis = -1 tells the function to collapse the array over the last dimension (the classes dimension), so that the shape of the preds_single is the [10000, 1] 
