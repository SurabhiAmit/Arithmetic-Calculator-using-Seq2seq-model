# Seq2seq-model-calculator

Neural networks are widely used to solve sequence-to-sequence prediction tasks. Seq2Seq models are very popular these days because they achieve great results in Machine Translation, Text Summarization, Conversational Modeling and more.

Using sequence-to-sequence modeling I am building a calculator for evaluating arithmetic expressions, by taking an equation as an input to the neural network and producing an answer as it's output.

## Libraries

Tensorflow and Scikit-learn libraries are used for this project.

## Encoder-Decoder

Encoder-Decoder is a successful architecture for Seq2Seq tasks with different lengths of input and output sequences. The main idea is to use two recurrent neural networks, where the first neural network encodes the input sequence into a real-valued vector and then the second neural network decodes this vector into the output sequence. While building the neural network, I specified the  characteristics of this architecture in the Tensorflow model.

## Encoder

The first RNN of the current architecture is called an encoder and serves for encoding an input sequence to a real-valued vector. Input of this RNN is an embedded input batch. Since sentences in the same batch could have different actual lengths, I provided input lengths to avoid unnecessary computations. The final encoder state will be passed to the second RNN (decoder).

>> TensorFlow provides a number of RNN cells ready for use, like GRU and LSTM cells. 
>> I wrapped the cells with DropoutWrapper. Dropout is an important regularization technique for neural networks. Specified input keep probability using the dropout placeholder that I created before.
>> Combined the defined encoder cells with Dynamic RNN. Used the embedded input batches and their lengths here.
>> Used dtype=tf.float32 everywhere.

## Decoder

The second RNN is called a decoder and serves for generating the output sequence. In the simple seq2seq arcitecture, the input sequence is provided to the decoder only as the final state of the encoder. Obviously, it is a bottleneck and Attention techniques can help to overcome it. So far, we do not need them to make our calculator work, but this would be a necessary ingredient for more advanced tasks.

During training, decoder also uses information about the true output. It is fed in as input symbol by symbol. However, during the prediction stage (which is called inference in this architecture), the decoder can only use its own generated output from the previous step to feed it in at the next step. Because of this difference (training vs inference), I created two distinct instances, which will serve for the described scenarios.

