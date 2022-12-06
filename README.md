# Music-Generator
This project casts its focus on automatic music generation via two popular approaches:
* WaveNet
* LSTM

The remarkable ability of deep learning networks to automatically extract features from the dataset makes them great candidates for automatic music generation. Both WaveNet and LSTM are examples of deep learning networks.

`"If I were not a physicist, I would probably be a musician. I often think in music. I live my daydreams in music. I see my life in terms of music"` - Albert Einstein

## WaveNet
WaveNet is a deep learning based generative model for raw audio developed by Google DeepMind. The main objective of WaveNet is to generate new samples from the original distrubution of data, making it a Generative model. The structure of WaveNet is similar to a language model from NLP. Instead of predicting the next word from a sentence, we predict the next note from a sequence of notes and chords.

### Input and Output
WaveNet takes a chunk of raw audio as input. Raw audio refers to the representation of a wave in the time-series domain, where an audio wave is recorded at different intervals of time, which depends on the sampling rate. Given a sequence of notes, we predict the next successive note, which serves as the output.

### Architecture
The building blocks of WaveNet are `Casual Dilated 1D Convolution Layers`. A convolution is a mathematical operation that is essentially a linear combination of a kernel and portions of the image. This is done in order to drastically reduce the number of inputs. In image processing, we would require 2D convolution, but in our case a 1D convolution suffices. The kernel scans the sequence of notes.

### Types of convolution

* Casual 1D convolution - Low receptive field (the number of inputs influencing an output)
!["casual convolution"](./images/casual_conv.png)

* Dilated 1D Casual convolution - We increaste the dilation rate exponentially at each hidden layer, which allows the output to be influenced by more input variables, giving us a high receptive field<br>
!["dilated convolution"](./images/dilated_conv.png)

### Steps
1. From a collection of MIDI files, we collect notes and chords all into one list. There is no reason for us to separate the notes from different songs.
2. We eliminate the notes that appear rarely to avoid outliers and simplify the training process.
!["frequency"](./images/frequency.png)<br>
(In this case, there were over 700 notes which occured less than 250 times, we recommend eliminating notes that fall under this bracket with a threshold of around 40)
3. Prepare input-output pairs for the model. Input - sequence of notes, Output - successive note
4. Convert the notes into numbers via a one-to-one mapping for the model
5. Build the model
6. Compose new music
7. Convert eh numbers back to notes