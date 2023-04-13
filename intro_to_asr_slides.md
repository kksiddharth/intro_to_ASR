---
theme: uncover
class:
- lead
marp: true
paginate: true
footer: 'SIddharth KK'
header: 'Introduction to Speech Recognition'
---

<!-- Title slide -->
<!-- _class: invert -->
# Speech Recognition and Processing
##### Siddharth Krishna Kumar
<!-- Background image -->
![bg](https://usabilitygeek.com/wp-content/uploads/2018/05/automatic-speech-recognition-lead.jpg)
<!-- _transition: fade -->
---

<!-- Overview slide -->
## Agenda

* How do you define a speech signal ?
* What is speech recognition ?
* What are the kinds of ASR systems ?
* Modular view of the system and hands on deep dive.
* What all cool stuff can you do with speech ?

<!-- _transition: drop -->

---

## How do you define a speech signal
* Sampling Rate 
* Bits per Sample or Bit Rate
* Number of channels
* File encoding

<!-- _transition: drop -->

---
<!-- Speech recognition slide -->
## What is Speech Recognition

* _Automatic speech recognition is like having a really cool robot that can listen to you when you talk, and then write down what you say!_

* _The task is to recognize a sequence of words present in the speech signal. Information is encoded temporally_
<!-- _transition: drop -->

---

![Image description](https://pimages.toolbox.com/wp-content/uploads/2022/04/14152224/116.png)
<!-- _transition: drop -->

---
### Requires knowledge of - 
* Speech Production
* Speech Perception
* Linguistic information
* Grammar of the language


<!-- _transition: drop -->
---
### Types of Speech Recognition systems
* Few phrases/commands – _[Yes, No]_
* Isolated Phones – _[yeh, eh, es, Nuh, oh]_
* Isolated words 
* Continuous Speech (Small Vocabulary)
* Continuous Speech (Large Vocabulary)

<!-- _transition: drop -->

---
### How to build the above mentioned ASR systems
<!-- _transition: drop -->

---

#### DTW [ Dynamic Time Warping ] 
$$D(i,j) = d(x_i, y_j)$$ 
$$DTW(X,Y) = \sqrt{\sum_{k=1}^{K} w_k \cdot d_{k}^2}$$
![DTW](https://static.wixstatic.com/media/3eee0b_eb84995a919c410bb0e1d5adc9875549~mv2.png/v1/fill/w_600,h_200,al_c,q_85,usm_0.66_1.00_0.01,enc_auto/3eee0b_eb84995a919c410bb0e1d5adc9875549~mv2.png)

<!-- _transition: drop -->

---

#### Support Vector Machines
1. _SVM trained to classify input speech feature vectors into predefined categories, such as different phonemes or words._ 
2. _Used for keyword spotting_
![bg right](https://static.javatpoint.com/tutorial/machine-learning/images/support-vector-machine-algorithm.png)


<!-- _transition: drop -->

---

#### Hidden Markov Models (HMM)
![HMM image](https://www.researchgate.net/publication/348706070/figure/fig11/AS:983119146545173@1611405278984/Example-of-hidden-Markov-Model-in-the-ASR-context.ppm)


<!-- _transition: drop -->


---

#### DNN based HMM model (Deep Neural Network)
![DNN-HMM image](https://media.springernature.com/lw685/springer-static/image/chp%3A10.1007%2F978-1-4471-5779-3_6/MediaObjects/301869_1_En_6_Fig1_HTML.gif)


<!-- _transition: drop -->

---

#### Encoder-Decoder models with CTC Loss
![CTC image](https://www.researchgate.net/profile/Natalia-Tomashenko/publication/336086784/figure/fig1/AS:809002619387904@1569892663207/Universal-end-to-end-deep-neural-network-model-architecture-for-ASR-NER-and-SF-tasks_Q640.jpg)


<!-- _transition: drop -->

---

#### Whisper - OpenAI, multi task model

![Whisper](https://openaicom.imgix.net/d9c13138-366f-49d3-b8bd-cb3f5a973a5b/asr-summary-of-model-architecture-desktop.svg?fm=auto&auto=compress,format&fit=min&w=3840&h=3103)


<!-- _transition: drop -->

---
#### Block Diargam of an ASR system

![ASR Block](https://www.researchgate.net/publication/271764127/figure/fig1/AS:295043781939203@1447355327831/Block-diagram-of-an-ASR-system8.png)

<!-- _transition: drop -->

---

## General Flow 
* Record Speech Signal
* Remove Noise and other effects
* Extract relevant phonetic information
* Recognize phones and construct best possible words and sentences from recognized phones
* Convert recognized sentence to human readable format
<!-- _transition: drop -->

---

<!-- Speech recognition slide -->
#### Stage 1 - Speech preprocessing and Feature extraction

* How can we convert a speech signal to a computer understandable form ?
* MFCC is a popular feature used in speech applications
* They are highly discriminative and can capture important aspects of speech, such as formant structure and speaker characteristics.

<!-- _transition: drop -->

---

![mfcc](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FTsu71%2FbtqETBgoxsP%2F7rgu73Uyc3isPddR9q1ZOK%2Fimg.png)

<!-- _transition: drop -->

---
### How to compute MFCC
![mfcc1](https://www.researchgate.net/publication/338006282/figure/fig1/AS:847780012650496@1579137914721/steps-of-MFCC-Feature-Extraction-The-spectrum-produced-from-the-human-vocal-tract-and-it.ppm)

<!-- _transition: drop -->

---
### Stage 2 - Decoder block
The overall picture for decoding-graph creation is that we are constructing the graph HCLG = H o C o L o G. This graph is considered as an FST (Finite State Transducer) hence the decoded graph will be “hclg.fst”

<!-- _transition: drop -->

---
#### How to understand this in simple terms
* G denotes Grammar of the language [ How it is spoken ]
* L denotes Lexicon of the language [ Rules of how a word is pronounced ]
* C denotes Context Dependancy
* H denotes the trained model [ Neural or statistical model that can recognise a phone]

<!-- _transition: drop -->

---

### Grammar of a language, or Language model
* Models the rules of how a language can be spoken
* Can be determined statistically
* Can be word level, or sub word level - For agglutenated languages
* Unigram, bigram, trigram

<!-- _transition: drop -->

---

### Lexicon of a language, or Pronunciation model
* Models how the words are pronounced
* Consistent and Non-consistent languages
* Requires in depth phonetic understanding of a language

<!-- _transition: drop -->

---

#### Context dependancy 
* If a language has 40 phones, then if we consider a tri phone model - `40^3`
![c-fst](https://maelfabien.github.io/assets/images/asr_24.png)

<!-- _transition: drop -->

---

### Stage 3 - Decoding graph and converting o/p sequence in human readable form

* In simple terms, shortest path in graph that returns the sequence of phones
* Sequence of phones to words, for continous/isolated word recognition
* Post proessing, Punctuation/ITN

<!-- _transition: drop -->

---
![decode](https://www.researchgate.net/publication/224246438/figure/fig1/AS:670002508201985@1536752454123/A-block-diagram-of-the-two-stage-ASR-decoding.png)

<!-- _transition: drop -->

---

### Simple example of lattice decoding

![viterbi](https://www.researchgate.net/publication/265183482/figure/fig9/AS:669369730351109@1536601588172/Computing-the-lattice-based-Viterbi-confidence-for-a-detection-of-term-GOOGLE-The.png)

<!-- _transition: drop -->

---
<!-- Speech processing slide -->
#### Speech is cool, you can build so much more

* Enhancement/Denoising
* Key Word Spotting
* Speaker Recognition
* Speech Diarization
* Speech Synthesis
* Speaker Analytics

<!-- Background image -->
![bg right](https://medienportal.siemens-stiftung.org/view/101913/sprache_als_hochkomplexes_schallsignal.jpg)

<!-- _transition: drop -->

---

<!-- Conclusion slide -->
## Questions ?

<!-- _transition: drop -->