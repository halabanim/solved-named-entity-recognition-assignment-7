Download Link: https://assignmentchef.com/product/solved-named-entity-recognition-assignment-7
<br>
Since you have read Jurafsky and Martin chapter <a href="https://web.stanford.edu/~jurafsky/slp3/21.pdf">21</a>, you know that Named Entity Recognition is the task of finding and classifying named entities in text. This task is often considered a sequence tagging task, like part of speech tagging, where words form a sequence through time, and each word is given a tag. Unlike part of speech tagging however, NER usually uses a relatively small number of tags, where the vast majority of words are tagged with the ‘non-entity’ tag, or O tag.

Your task is to implement your own named entity recognizer. Relax, you’ll find it’s a lot easier than it sounds, and it should be very satisfying to accomplish this. There will be two versions of this task: the first, the constrained version, is the required entity tagger that you implement using scikit learn, filling out the stub that we give you. The second is an unconstrained optional version where you use whatever tool, technique, or feature you can get your hands to get the best possible score on the dataset. There will be a leaderboard for each version.

As with nearly all NLP tasks, you will find that the two big points of variability in NER are (a) the features, and (b) the learning algorithm, with the features arguably being the more important of the two. The point of this assignment is for you to think about and experiment with both of these. Are there interesting features you can use? What latent signal might be important for NER? What have you learned in the class so far that can be brought to bear?

Get a headstart on common NER features by looking at Figure 21.5 in the textbook.

<h2 id="the-data">The Data</h2>

The data we use comes from the Conference on Natural Language Learning (CoNLL) 2002 shared task of named entity recognition for Spanish and Dutch. The <a href="http://www.aclweb.org/anthology/W02-2024">introductory paper to the shared task</a> will be of immense help to you, and you should definitely read it. You may also find the <a href="https://www.clips.uantwerpen.be/conll2002/ner/">original shared task page</a> helpful. We will use the Spanish corpus (although you are welcome to try out Dutch too).

The tagset is:

<ul>

 <li><em>PER</em>: for Person</li>

 <li><em>LOC</em>: for Location</li>

 <li><em>ORG</em>: for Organization</li>

 <li><em>MISC</em>: for miscellaneous named entities</li>

</ul>

The data uses BIO encoding (called IOB in the textbook), which means that each named entity tag is prefixed with a <code class="highlighter-rouge">B-</code>, which means beginning, or an <code class="highlighter-rouge">I-</code>, which means inside. So, for a multiword entity, like “James Earle Jones”, the first token “James” would be tagged with “B-PER”, and each subsequent token is “I-PER”. The O tag is for non-entities.

We strongly recommend that you study the training and dev data (no one’s going to stop you from examining the test data, but for the integrity of your model, it’s best to not look at it). Are there idiosyncracies in the data? Are there patterns you can exploit with cool features? Are there obvious signals that identify names? For example, in some Turkish writing, there is a tradition of putting an apostrophe between a named entity and the morphology attached to it. A feature of <code class="highlighter-rouge">isApostrophePresent()</code> goes a long way. Of course, in English and several other languages, capitalization is a hugely important feature. In some African languages, there are certain words that always precede city names.

The data is packaged nicely from <a href="http://www.nltk.org/">NLTK</a>. Get installation instructions here: <a href="http://www.nltk.org/install.html">installing NLTK</a>.

You will be glad to hear that the data is a mercifully small download. See the <a href="http://www.nltk.org/data">NLTK data</a> page for for download options, but one way to get the conll2002 data is:

<h2 id="evaluation">Evaluation</h2>

There are two common ways of evaluating NER systems: phrase-based, and token-based. In phrase-based, the more common of the two, a system must predict the entire span correctly for each name. For example, say we have text containing “James Earle Jones”, and our system predicts “[PER James Earle] Jones”. Phrase-based gives no credit for this because it missed “Jones”, whereas token-based would give partial credit for correctly identifying “James” and “Earle” as B-PER and I-PER respectively. We will use phrase-based to report scores.

The output of your code must be <code class="highlighter-rouge">word gold pred</code>, as in:

Here’s how to get scores (assuming the above format is in a file called <code class="highlighter-rouge">results.txt</code>):

(The python version of conlleval doesn’t calculate the token-based score, but if you really want it, you can use the <a href="https://www.clips.uantwerpen.be/conll2000/chunking/output.html">original perl version</a>. You would use the <code class="highlighter-rouge">-r</code> flag.)

<h2 id="other-resources">Other resources</h2>

Here are some other NER frameworks which you are welcome to run in the unconstrained version:

<ul>

 <li><a href="https://github.com/CogComp/cogcomp-nlp/tree/master/ner">CogComp NER</a>, one of the best taggers</li>

 <li><a href="https://github.com/glample/tagger">LSTM-CRF</a>, recent neural network tagger</li>

 <li><a href="https://nlp.stanford.edu/software/CRF-NER.shtml">Stanford NER</a>, Stanford’s tried and true tagger</li>

 <li><a href="https://spacy.io/usage/training">spaCy</a></li>

 <li><a href="https://github.com/percyliang/brown-cluster">Brown clustering software</a>. You might find it useful.</li>

 <li><a href="http://crscardellino.me/SBWCE/">Spanish text and vectors</a></li>

 <li><a href="http://www.statmt.org/europarl/">Europarl corpora</a>, look for the English-Spanish parallel text</li>

</ul>

Note: you are not allowed to use pre-trained NER models even in the unconstrained version. Please train your own. You are allowed to use pre-trained embeddings.

<h2 id="baselines">Baselines</h2>

The version we have given you gets about 49% F1 right out of the box. We made some very simple modifications, and got it to 60%. This is a generous baseline that any thoughtful model should be able to beat. The state of the art on the Spanish dataset is about 85%. If you manage to beat that, then look for conference deadlines and start writing, because you can publish it.

As always, beating the baseline alone with earn you a B on the project. In order to earn an A, demonstrate that you have thought about the problem carefully, and come up with solutions beyond what was strictly required. Extra credit for the top of the leaderboard etc.

<h2 id="deliverables">Deliverables</h2>

<h2 id="recommended-readings">Recommended readings</h2>

<ul>

 <li>Jurafsky and Martin chapter <a href="https://web.stanford.edu/~jurafsky/slp3/21.pdf">21</a></li>

 <li><a href="http://cogcomp.org/papers/RatinovRo09.pdf">Design Challenges and Misconeptions in Named Entity Recognition</a> a very highly cited NER paper from a Penn professor</li>

 <li><a href="https://aclanthology.info/pdf/N/N07/N07-2046.pdf">Entity Extraction is a Boring Solved Problem – or is it?</a></li>

 <li><a href="https://arxiv.org/abs/1603.01360">Neural Architectures for Named Entity Recognition</a>, a popular recent paper on… just read the title.</li>

 <li><a href="http://www.aclweb.org/anthology/W02-2024">Introductory paper to CoNLL 2002 shared task</a></li>

</ul>

5/5 - (1 vote)

Here are the materials that you should download for this assignment:

<ul>

 <li><a href="http://computational-linguistics-class.org/downloads/hw7/ner.py">Code stub</a>.</li>

 <li><a href="http://computational-linguistics-class.org/downloads/hw7/conlleval.py">conlleval.py</a>: eval script</li>

</ul>

<pre class="highlight"><code>$ python -m nltk.downloader conll2002</code></pre>

<pre class="highlight"><code>La B-LOC B-LOCCoruña I-LOC I-LOC, O O23 O Omay O O( O OEFECOM B-ORG B-ORG) O O. O O</code></pre>

<pre class="highlight"><code># Phrase-based score$ python conlleval.py results.txt</code></pre>

Here are the deliverables that you will need to submit:

<ul>

 <li>Code, as always in Python 3.</li>

 <li>Constrained results (in a file called <code class="highlighter-rouge">constrained_results.txt</code>)</li>

 <li>Optional unconstrained results (in a file called <code class="highlighter-rouge">unconstrained_results.txt</code>)</li>

 <li>PDF Report (called writeup.pdf)</li>