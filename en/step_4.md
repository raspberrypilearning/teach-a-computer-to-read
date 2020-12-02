## Build your model

Now that you have images prepared, it's time to build a model to recognise them. The **image classifier** you'll build is a kind of **neural network**. Neural networks get their name because they behave a little like our brains, which are made of neurons. However, a neural network that you build in a computer uses **nodes** instead of neurons. The nodes are organised into **layers**, with every node in a layer being connected to every node in the next layer. 

The first layer takes the input, in this case the image of a number, and the last layer provides the output, in this case the likelihood that the input is each of the numbers from zero to nine. Treat the highest likelihood as the model's prediction, or best guess, as to what the image is.

Each node learns a rule, and produces a measure of the strength of the match from its inputs to the rule it has learned, which it passes on to every node it is connected to as an input. Each node is connected to every node in the next layer.

![A single black circle connected by arrows to each circle in a column of three pink circles. Each of those circles is in turn connected by arrows to both circles in a column of two pink circles, each of which is connected by arrows to all of the circles in a column of four pink circles. Finally, those four circles are connected by arrows to two green circles.](images/neural_network_diagram.png)

Your model has four layers:

  + The first will take the image in and convert it to a flattened list of numbers, but it won't actually learn any rules. The other three layers will. 
  + The second layer receives the flattened image as an input and will create simple rules. Maybe these rules detect things like a curve in the top right of the image, or a curve in the bottom left of the image. The second layer will pass its outputs to the third layer as that layer's inputs. 
  + The third layer might contain a rule that combines both of those nodes as inputs and detects a curve in *both* the top right and bottom left of an image. 
  + Finally the fourth layer, the output layer, might use the input from that third layer node to make a strong prediction that the number is an eight. 
  
While it's helpful to have some idea of how the network 'thinks', it's not worth spending too much time trying to figure out the sorts of rules it might create. The rules created by machine learning neural networks are usually quite strange, and make little sense to humans, but work very well for machines. 

--- task ---
In the next empty cell in the notebook, create your model with one `Flatten` layer, to take a 28 by 28 pixel image and convert it into a single list of 784 (28 times 28) numbers, as well as three `Dense` layers to create rules and provide your outputs. The last layer must have ten nodes, as there are ten numbers. For the others, choose 500 and 300. These are good sizes for this problem, but once you've got the model trained with them you can try others and see what difference it makes.

```python
model = tf.keras.Sequential([
                                    tf.keras.layers.Flatten(input_shape=(28,28)),
                                    tf.keras.layers.Dense(500, activation='relu'),
                                    tf.keras.layers.Dense(300, activation='relu'),
                                    tf.keras.layers.Dense(10, activation= 'softmax')
                                    ])
```

--- /task ---

The `activation='relu'` you see in the dense layers above is a particular function — called an activation function — that the outputs of the nodes in the layer are passed through before being passed as inputs to the next layer. The function is run for each node, and it decides whether or not the node is used as part of the input to the next layer. Relu is the default activation function, the one you pick when you don't have a reason to pick another. Softmax, the other activation function used here, converts the numbers in the final layer into probabilities that add up to 100 percent. The greatest of these probabilities is the most likely guess for the number shown in the image given to your model.

--- save ---
