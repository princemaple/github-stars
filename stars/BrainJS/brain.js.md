---
project: brain.js
stars: 14838
description: 🤖 GPU accelerated Neural networks in JavaScript for Browsers and Node.js
url: https://github.com/BrainJS/brain.js
---

brain.js
========

GPU accelerated Neural networks in JavaScript for Browsers and Node.js

About
-----

`brain.js` is a GPU accelerated library for Neural Networks written in JavaScript.

💡 This is a continuation of the **harthur/brain**, which is not maintained anymore. More info

Table of Contents
-----------------

-   Installation and Usage
    -   NPM
    -   CDN
    -   Download
    -   Installation note
    -   Building from source
-   Examples
    -   More Examples
-   Training
    -   Data format
        -   For training with NeuralNetwork
        -   For training with `RNNTimeStep`, `LSTMTimeStep` and `GRUTimeStep`
        -   For training with `RNN`, `LSTM` and `GRU`
        -   For training with `AE`
    -   Training Options
    -   Async Training
    -   Cross Validation
    -   Train Stream
-   Methods
    -   train
    -   run
    -   forecast
-   Failing
-   JSON
-   Standalone Function
-   Options
    -   activation
    -   hiddenLayers
-   Streams
-   Utilities
    -   `likely`
    -   `toSVG`
-   Neural Network Types
    -   Why different Neural Network Types?

Installation and Usage
----------------------

### NPM

If you can install `brain.js` with npm:

npm install brain.js

### CDN

<script src\="//unpkg.com/brain.js"\></script\>

### Download

Download the latest brain.js for browser

### Installation note

`Brain.js` depends on a native module `headless-gl` for GPU support. In most cases installing `brain.js` from npm should just work. However, if you run into problems, this means prebuilt binaries are not able to download from GitHub repositories and you might need to build it yourself.

#### Building from source

Please make sure the following dependencies are installed and up to date and then run:

npm rebuild

##### System dependencies

###### Mac OS X

-   A supported version of Python
-   XCode

###### Ubuntu/Debian

-   A supported version of Python
-   A GNU C++ environment (available via the `build-essential` package on `apt`)
-   libxi-dev
-   Working and up-to-date OpenGL drivers
-   GLEW
-   pkg-config

sudo apt-get install -y build-essential libglew-dev libglu1-mesa-dev libxi-dev pkg-config

###### Windows

-   A supported version of Python **See:** https://apps.microsoft.com/store/search/python
-   Microsoft Visual Studio Build Tools 2022
-   run in cmd: `npm config set msvs_version 2022` **Note: This no longer works in modern versions of npm.**
-   run in cmd: `npm config set python python3` **Note: This no longer works in modern versions of npm.**

\* If you are using `Build Tools 2017` then run `npm config set msvs_version 2017` **Note: This no longer works in modern versions of npm.**

Examples
--------

Here's an example showcasing how to approximate the XOR function using `brain.js`: more info on config here.

💡 A fun and practical introduction to Brain.js

// provide optional config object (or undefined). Defaults shown.
const config \= {
  binaryThresh: 0.5,
  hiddenLayers: \[3\], // array of ints for the sizes of the hidden layers in the network
  activation: 'sigmoid', // supported activation types: \['sigmoid', 'relu', 'leaky-relu', 'tanh'\],
  leakyReluAlpha: 0.01, // supported for activation type 'leaky-relu'
};

// create a simple feed-forward neural network with backpropagation
const net \= new brain.NeuralNetwork(config);

net.train(\[
  { input: \[0, 0\], output: \[0\] },
  { input: \[0, 1\], output: \[1\] },
  { input: \[1, 0\], output: \[1\] },
  { input: \[1, 1\], output: \[0\] },
\]);

const output \= net.run(\[1, 0\]); // \[0.987\]

or more info on config here.

// provide optional config object, defaults shown.
const config \= {
  inputSize: 20,
  inputRange: 20,
  hiddenLayers: \[20, 20\],
  outputSize: 20,
  learningRate: 0.01,
  decayRate: 0.999,
};

// create a simple recurrent neural network
const net \= new brain.recurrent.RNN(config);

net.train(\[
  { input: \[0, 0\], output: \[0\] },
  { input: \[0, 1\], output: \[1\] },
  { input: \[1, 0\], output: \[1\] },
  { input: \[1, 1\], output: \[0\] },
\]);

let output \= net.run(\[0, 0\]); // \[0\]
output \= net.run(\[0, 1\]); // \[1\]
output \= net.run(\[1, 0\]); // \[1\]
output \= net.run(\[1, 1\]); // \[0\]

However, there is no reason to use a neural network to figure out XOR. (-: So, here is a more involved, realistic example: Demo: training a neural network to recognize color contrast.

More Examples
-------------

Brain.js Examples Repo

You can check out this fantastic screencast, which explains how to train a simple neural network using a real-world dataset: How to create a neural network in the browser using Brain.js.

Training
--------

Use `train()` to train the network with an array of training data. The network has to be trained with all the data in bulk in one call to `train()`. More training patterns will probably take longer to train, but will usually result in a network better at classifying new patterns.

### Note

Training is computationally expensive, so you should try to train the network offline (or on a Worker) and use the `toFunction()` or `toJSON()` options to plug the pre-trained network into your website.

### Data format

#### For training with `NeuralNetwork`

Each training pattern should have an `input` and an `output`, both of which can be either an array of numbers from `0` to `1` or a hash of numbers from `0` to `1`. For the color contrast demo it looks something like this:

const net \= new brain.NeuralNetwork();

net.train(\[
  { input: { r: 0.03, g: 0.7, b: 0.5 }, output: { black: 1 } },
  { input: { r: 0.16, g: 0.09, b: 0.2 }, output: { white: 1 } },
  { input: { r: 0.5, g: 0.5, b: 1.0 }, output: { white: 1 } },
\]);

const output \= net.run({ r: 1, g: 0.4, b: 0 }); // { white: 0.99, black: 0.002 }

Here's another variation of the above example. (_Note_ that input objects do not need to be similar.)

net.train(\[
  { input: { r: 0.03, g: 0.7 }, output: { black: 1 } },
  { input: { r: 0.16, b: 0.2 }, output: { white: 1 } },
  { input: { r: 0.5, g: 0.5, b: 1.0 }, output: { white: 1 } },
\]);

const output \= net.run({ r: 1, g: 0.4, b: 0 }); // { white: 0.81, black: 0.18 }

#### For training with `RNNTimeStep`, `LSTMTimeStep` and `GRUTimeStep`

Each training pattern can either:

-   Be an array of numbers
-   Be an array of arrays of numbers

Example using an array of numbers:

const net \= new brain.recurrent.LSTMTimeStep();

net.train(\[\[1, 2, 3\]\]);

const output \= net.run(\[1, 2\]); // 3

Example using an array of arrays of numbers:

const net \= new brain.recurrent.LSTMTimeStep({
  inputSize: 2,
  hiddenLayers: \[10\],
  outputSize: 2,
});

net.train(\[
  \[1, 3\],
  \[2, 2\],
  \[3, 1\],
\]);

const output \= net.run(\[
  \[1, 3\],
  \[2, 2\],
\]); // \[3, 1\]

#### For training with `RNN`, `LSTM` and `GRU`

Each training pattern can either:

-   Be an array of values
-   Be a string
-   Have an `input` and an `output`
    -   Either of which can have an array of values or a string

CAUTION: When using an array of values, you can use ANY value, however, the values are represented in the neural network by a single input. So the more _distinct values_ has _the larger your input layer_. If you have a hundreds, thousands, or millions of floating point values _THIS IS NOT THE RIGHT CLASS FOR THE JOB_. Also, when deviating from strings, this gets into beta

Example using direct strings: Hello World Using Brainjs

  const net \= new brain.recurrent.LSTM();

  net.train(\['I am brainjs, Hello World!'\]);

  const output \= net.run('I am brainjs');
  alert(output);

const net \= new brain.recurrent.LSTM();

net.train(\[
  'doe, a deer, a female deer',
  'ray, a drop of golden sun',
  'me, a name I call myself',
\]);

const output \= net.run('doe'); // ', a deer, a female deer'

Example using strings with inputs and outputs:

const net \= new brain.recurrent.LSTM();

net.train(\[
  { input: 'I feel great about the world!', output: 'happy' },
  { input: 'The world is a terrible place!', output: 'sad' },
\]);

const output \= net.run('I feel great about the world!'); // 'happy'

#### For training with `AE`

Each training pattern can either:

-   Be an array of numbers
-   Be an array of arrays of numbers

Training an autoencoder to compress the values of a XOR calculation:

const net \= new brain.AE(
  {
    hiddenLayers: \[ 5, 2, 5 \]
  }
);

net.train(\[
  \[ 0, 0, 0 \],
  \[ 0, 1, 1 \],
  \[ 1, 0, 1 \],
  \[ 1, 1, 0 \]
\]);

Encoding/decoding:

const input \= \[ 0, 1, 1 \];

const encoded \= net.encode(input);
const decoded \= net.decode(encoded);

Denoise noisy data:

const noisyData \= \[ 0, 1, 0 \];

const data \= net.denoise(noisyData);

Test for anomalies in data samples:

const shouldBeFalse \= net.includesAnomalies(\[0, 1, 1\]);
const shouldBeTrue \= net.includesAnomalies(\[0, 1, 0\]);

### Training Options

`train()` takes a hash of options as its second argument:

net.train(data, {
  // Defaults values --> expected validation
  iterations: 20000, // the maximum times to iterate the training data --> number greater than 0
  errorThresh: 0.005, // the acceptable error percentage from training data --> number between 0 and 1
  log: false, // true to use console.log, when a function is supplied it is used --> Either true or a function
  logPeriod: 10, // iterations between logging out --> number greater than 0
  learningRate: 0.3, // scales with delta to effect training rate --> number between 0 and 1
  momentum: 0.1, // scales with next layer's change value --> number between 0 and 1
  callback: null, // a periodic call back that can be triggered while training --> null or function
  callbackPeriod: 10, // the number of iterations through the training data between callback calls --> number greater than 0
  timeout: number, // the max number of milliseconds to train for --> number greater than 0. Default --> Infinity
});

The network will stop training whenever one of the two criteria is met: the training error has gone below the threshold (default `0.005`), or the max number of iterations (default `20000`) has been reached.

By default, training will not let you know how it's doing until the end, but set `log` to `true` to get periodic updates on the current training error of the network. The training error should decrease every time. The updates will be printed to the console. If you set `log` to a function, this function will be called with the updates instead of printing to the console. However, if you want to use the values of the updates in your own output, the `callback` can be set to a function to do so instead.

The learning rate is a parameter that influences how quickly the network trains. It's a number from `0` to `1`. If the learning rate is close to `0`, it will take longer to train. If the learning rate is closer to `1`, it will train faster, but training results may be constrained to a local minimum and perform badly on new data.(_Overfitting_) The default learning rate is `0.3`.

The momentum is similar to learning rate, expecting a value from `0` to `1` as well, but it is multiplied against the next level's change value. The default value is `0.1`

Any of these training options can be passed into the constructor or passed into the `updateTrainingOptions(opts)` method and they will be saved on the network and used during the training time. If you save your network to json, these training options are saved and restored as well (except for callback and log, callback will be forgotten and log will be restored using console.log).

A boolean property called `invalidTrainOptsShouldThrow` is set to `true` by default. While the option is `true`, if you enter a training option that is outside the normal range, an error will be thrown with a message about the abnormal option. When the option is set to `false`, no error will be sent, but a message will still be sent to `console.warn` with the related information.

### Async Training

`trainAsync()` takes the same arguments as train (data and options). Instead of returning the results object from training, it returns a promise that when resolved will return the training results object. Does NOT work with:

-   `brain.recurrent.RNN`
-   `brain.recurrent.GRU`
-   `brain.recurrent.LSTM`
-   `brain.recurrent.RNNTimeStep`
-   `brain.recurrent.GRUTimeStep`
-   `brain.recurrent.LSTMTimeStep`

const net \= new brain.NeuralNetwork();
net
  .trainAsync(data, options)
  .then((res) \=> {
    // do something with my trained network
  })
  .catch(handleError);

With multiple networks you can train in parallel like this:

const net \= new brain.NeuralNetwork();
const net2 \= new brain.NeuralNetwork();

const p1 \= net.trainAsync(data, options);
const p2 \= net2.trainAsync(data, options);

Promise.all(\[p1, p2\])
  .then((values) \=> {
    const res \= values\[0\];
    const res2 \= values\[1\];
    console.log(
      \`net trained in ${res.iterations} and net2 trained in ${res2.iterations}\`
    );
    // do something super cool with my 2 trained networks
  })
  .catch(handleError);

### Cross Validation

Cross Validation can provide a less fragile way of training on larger data sets. The brain.js api provides Cross Validation in this example:

const crossValidate \= new brain.CrossValidate(() \=> new brain.NeuralNetwork(networkOptions));
crossValidate.train(data, trainingOptions, k); //note k (or KFolds) is optional
const json \= crossValidate.toJSON(); // all stats in json as well as neural networks
const net \= crossValidate.toNeuralNetwork(); // get top performing net out of \`crossValidate\`

// optionally later
const json \= crossValidate.toJSON();
const net \= crossValidate.fromJSON(json);

Use `CrossValidate` with these classes:

-   `brain.NeuralNetwork`
-   `brain.RNNTimeStep`
-   `brain.LSTMTimeStep`
-   `brain.GRUTimeStep`

An example of using cross validate can be found in cross-validate.ts

Methods
-------

### `train(trainingData)` -> trainingStatus

The output of `train()` is a hash of information about how the training went:

{
  error: 0.0039139985510105032,  // training error
  iterations: 406                // training iterations
}

### `run(input)` -> prediction

Supported on classes:

-   `brain.NeuralNetwork`
-   `brain.NeuralNetworkGPU` -> All the functionality of `brain.NeuralNetwork` but, ran on GPU (via gpu.js in WebGL2, WebGL1, or fallback to CPU)
-   `brain.recurrent.RNN`
-   `brain.recurrent.LSTM`
-   `brain.recurrent.GRU`
-   `brain.recurrent.RNNTimeStep`
-   `brain.recurrent.LSTMTimeStep`
-   `brain.recurrent.GRUTimeStep`

Example:

// feed forward
const net \= new brain.NeuralNetwork();
net.fromJSON(json);
net.run(input);

// time step
const net \= new brain.LSTMTimeStep();
net.fromJSON(json);
net.run(input);

// recurrent
const net \= new brain.LSTM();
net.fromJSON(json);
net.run(input);

### `forecast(input, count)` -> predictions

Available with the following classes. Outputs a array of predictions. Predictions being a continuation of the inputs.

-   `brain.recurrent.RNNTimeStep`
-   `brain.recurrent.LSTMTimeStep`
-   `brain.recurrent.GRUTimeStep`

Example:

const net \= new brain.LSTMTimeStep();
net.fromJSON(json);
net.forecast(input, 3);

### `toJSON() -> json`

Serialize neural network to json

### `fromJSON(json)`

Deserialize neural network from json

Failing
-------

If the network failed to train, the error will be above the error threshold. This could happen if the training data is too noisy (most likely), the network does not have enough hidden layers or nodes to handle the complexity of the data, or it has not been trained for enough iterations.

If the training error is still something huge like `0.4` after 20000 iterations, it's a good sign that the network can't make sense of the given data.

### RNN, LSTM, or GRU Output too short or too long

The instance of the net's property `maxPredictionLength` (default 100) can be set to adjust the output of the net;

Example:

const net \= new brain.recurrent.LSTM();

// later in code, after training on a few novels, write me a new one!
net.maxPredictionLength \= 1000000000; // Be careful!
net.run('Once upon a time');

JSON
----

Serialize or load in the state of a trained network with JSON:

const json \= net.toJSON();
net.fromJSON(json);

Standalone Function
-------------------

You can also get a custom standalone function from a trained network that acts just like `run()`:

const run \= net.toFunction();
const output \= run({ r: 1, g: 0.4, b: 0 });
console.log(run.toString()); // copy and paste! no need to import brain.js

Options
-------

`NeuralNetwork()` takes a hash of options:

const net \= new brain.NeuralNetwork({
  activation: 'sigmoid', // activation function
  hiddenLayers: \[4\],
  learningRate: 0.6, // global learning rate, useful when training using streams
});

### activation

This parameter lets you specify which activation function your neural network should use. There are currently four supported activation functions, **sigmoid** being the default:

-   sigmoid
-   relu
-   leaky-relu
    -   related option - 'leakyReluAlpha' optional number, defaults to 0.01
-   tanh

Here's a table (thanks, Wikipedia!) summarizing a plethora of activation functions — Activation Function

### hiddenLayers

You can use this to specify the number of hidden layers in the network and the size of each layer. For example, if you want two hidden layers - the first with 3 nodes and the second with 4 nodes, you'd give:

hiddenLayers: \[3, 4\];

By default `brain.js` uses one hidden layer with size proportionate to the size of the input array.

Streams
-------

Use https://www.npmjs.com/package/train-stream to stream data to a NeuralNetwork

Utilities
---------

### `likely`

const likely \= require('brain/likely');
const key \= likely(input, net);

Likely example see: simple letter detection

### `toSVG`

<script src\="../../src/utilities/svg.js"\></script\>

Renders the network topology of a feedforward network

document.getElementById('result').innerHTML \= brain.utilities.toSVG(
  network,
  options
);

toSVG example see: network rendering

The user interface used:

Neural Network Types
--------------------

-   `brain.NeuralNetwork` - Feedforward Neural Network with backpropagation
-   `brain.NeuralNetworkGPU` - Feedforward Neural Network with backpropagation, GPU version
-   `brain.AE` - Autoencoder or "AE" with backpropogation and GPU support
-   `brain.recurrent.RNNTimeStep` - Time Step Recurrent Neural Network or "RNN"
-   `brain.recurrent.LSTMTimeStep` - Time Step Long Short Term Memory Neural Network or "LSTM"
-   `brain.recurrent.GRUTimeStep` - Time Step Gated Recurrent Unit or "GRU"
-   `brain.recurrent.RNN` - Recurrent Neural Network or "RNN"
-   `brain.recurrent.LSTM` - Long Short Term Memory Neural Network or "LSTM"
-   `brain.recurrent.GRU` - Gated Recurrent Unit or "GRU"
-   `brain.FeedForward` - Highly Customizable Feedforward Neural Network with backpropagation
-   `brain.Recurrent` - Highly Customizable Recurrent Neural Network with backpropagation

### Why different Neural Network Types

Different neural nets do different things well. For example:

-   A Feedforward Neural Network can classify simple things very well, but it has no memory of previous actions and has infinite variation of results.
-   A Time Step Recurrent Neural Network _remembers_, and can predict future values.
-   A Recurrent Neural Network _remembers_, and has a finite set of results.

Get Involved
------------

### W3C machine learning standardization process

If you are a developer or if you just care about how ML API should look like - please take a part and join W3C community and share your opinions or simply support opinions you like or agree with.

Brain.js is a widely adopted open source machine learning library in the javascript world. There are several reasons for it, but most notable is **simplicity of usage while not sacrificing performance**. We would like to keep it also simple to learn, simple to use and performant when it comes to W3C standard. We think that current brain.js API is quite close to what we could expect to become a standard. And since supporting doesn't require much effort and still can make a huge difference feel free to join W3C community group and support us with brain.js like API.

Get involved into W3C machine learning ongoing standardization process here. You can also join our open discussion about standardization here.

Issues
------

If you have an issue, either a bug or a feature you think would benefit your project let us know and we will do our best.

Create issues here and follow the template.

### brain.js.org

Source for `brain.js.org` is available at Brain.js.org Repository. Built using awesome `vue.js` & `bulma`. Contributions are always welcome.

Contributors
------------

This project exists thanks to all the people who contribute. \[Contribute\].

Backers
-------

Thank you to all our backers! 🙏 \[Become a backer\]

Sponsors
--------

Support this project by becoming a sponsor. Your logo will show up here with a link to your website. \[Become a sponsor\]
