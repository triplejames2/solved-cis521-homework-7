Download Link: https://assignmentchef.com/product/solved-cis521-homework-7
<br>
<strong> </strong><span style="font-size: 2.61792em; letter-spacing: -1px;">Instructions</span>

In this assignment, you will gain experience working with Markov models on text.

A skeleton file homework7.py containing empty definitions for each question has been provided. Since portions of this assignment will be graded automatically, none of the names or function signatures in this file should be modified. However, you are free to introduce additional variables or functions if needed.

You may import definitions from any standard Python library, and are encouraged to do so in case you find yourself reinventing the wheel.

You will find that in addition to a problem specification, most programming questions also include a pair of examples from the Python interpreter. These are meant to illustrate typical use cases, and should not be taken as comprehensive test suites.

You are strongly encouraged to follow the Python style guidelines set forth in <u>PEP 8</u>, which was written in part by the creator of Python. However, your code will not be graded for style. Once you have completed the assignment, you should submit your file on Eniac using the following turnin command, where the flags -c and -p stand for “course” and “project”, respectively.

You may submit as many times as you would like before the deadline, but only the last submission will be saved. To view a detailed listing of the contents of your most recent submission, you can use the following command, where the flag <sub>-v</sub> stands for “verbose”.

<h1>1.   Markov Models [45 points]</h1>

In this section, you will build a simple language model that can be used to generate random text resembling a source document. Your use of external code should be limited to built-in Python modules, which excludes, for example, NumPy and NLTK.

<ol>

 <li><strong>[5 points] </strong>Write a simple tokenization function tokenize(text) which takes as input a string of text and returns a list of tokens derived from that text. Here, we define a token to be a contiguous sequence of non-whitespace characters, with the exception that any punctuation mark should be treated as an individual token. <em>Hint: Use the built-in constant </em><em>string</em><em>.</em><em>punctuation, found in the </em><em>string</em></li>

</ol>

&gt;&gt;&gt; tokenize(”  This is an example.  “)    &gt;&gt;&gt; tokenize(“‘Medium-rare,’ she said.”) [‘This’, ‘is’, ‘an’, ‘example’, ‘.’] [“‘”, ‘Medium’, ‘-‘, ‘rare’, ‘,’, “‘”,

‘she’, ‘said’, ‘.’]

<ol start="2">

 <li><strong>[5 points] </strong>Write a function ngrams(n, tokens) that produces a list of all G-grams of the specified size from the input token list. Each G-gram should consist of a 0-element tuple (context, token), where the context is itself an &amp;GИ/’-element tuple comprised of the GИ/ words preceding the current token. The sentence should be padded with</li>

</ol>

GИ/ “&lt;START&gt;” tokens at the beginning and a single “&lt;END&gt;” token at the end. If G; /, all contexts should be empty tuples. You may assume that Gд/.

&gt;&gt;&gt; ngrams(1, [“a”, “b”, “c”])             &gt;&gt;&gt; ngrams(3, [“a”, “b”, “c”])

[((), ‘a’), ((), ‘b’), ((), ‘c’),          [((‘&lt;START&gt;’, ‘&lt;START&gt;’), ‘a’),

((), ‘&lt;END&gt;’)]                           ((‘&lt;START&gt;’, ‘a’), ‘b’),

&gt;&gt;&gt; ngrams(2, [“a”, “b”, “c”])             ((‘a’, ‘b’), ‘c’),

[((‘&lt;START&gt;’,), ‘a’), ((‘a’,), ‘b’), ((‘b’, ‘c’), ‘&lt;END&gt;’)]  ((‘b’,), ‘c’), ((‘c’,), ‘&lt;END&gt;’)]

<ol start="3">

 <li><strong>[5 points] </strong>In the NgramModel class, write an initialization method __init__(self, n) which stores the order G of the model and initializes any necessary internal variables.</li>

</ol>

Then write a method update(self, sentence) which computes the G-grams for the input sentence and updates the internal counts. Lastly, write a method

prob(self, context, token) which accepts an &amp;GИ/’-tuple representing a context

and a token, and returns the probability of that token occuring, given the preceding context.

<ol start="4">

 <li><strong>[10 points] </strong>In the NgramModel class, write a method random_token(self, context) which returns a random token according to the probability distribution determined by the given context. Specifically, let 3 ; ⅩM<sub>/</sub>*M<sub>0</sub>*—*M<sub>G</sub>Ⅺ be the set of tokens which can occur in the given context, sorted according to Python’s natural lexicographic ordering, and let .гK: / be a random number between . and /. Your method should return the token M<sub>B</sub> such that</li>

</ol>

<sup>.</sup><sup>BИ/ </sup>/&amp;M<sub>C</sub>Уamlrcvr’гK: <sup>.</sup><sup>B </sup>/&amp;M<sub>C</sub>Уamlrcvr’,

C;/                            C;/

You should use a single call to the random.random() function to generate K.

&gt;&gt;&gt; m = NgramModel(1)                      &gt;&gt;&gt; m = NgramModel(2)

&gt;&gt;&gt; m.update(“a b c d”)                    &gt;&gt;&gt; m.update(“a b c d”)

&gt;&gt;&gt; m.update(“a b a b”)                    &gt;&gt;&gt; m.update(“a b a b”)

&gt;&gt;&gt; random.seed(1)                         &gt;&gt;&gt; random.seed(2)

&gt;&gt;&gt; [m.random_token(())  &gt;&gt;&gt; [m.random_token((“&lt;START&gt;”,))      for i in range(25)]       for i in range(6)]

[‘&lt;END&gt;’, ‘c’, ‘b’, ‘a’, ‘a’, ‘a’, ‘b’,     [‘a’, ‘a’, ‘a’, ‘a’, ‘a’, ‘a’]

‘b’, ‘&lt;END&gt;’, ‘&lt;END&gt;’, ‘c’, ‘a’, ‘b’,      &gt;&gt;&gt; [m.random_token((“b”,))

‘&lt;END&gt;’, ‘a’, ‘b’, ‘a’, ‘d’, ‘d’,              for i in range(6)]

‘&lt;END&gt;’, ‘&lt;END&gt;’, ‘b’, ‘d’, ‘a’, ‘a’]      [‘c’, ‘&lt;END&gt;’, ‘a’, ‘a’, ‘a’, ‘&lt;END&gt;’]

<ol start="5">

 <li><strong>[10 points] </strong>In the NgramModel class, write a method random_text(self, token_count) which returns a string of space-separated tokens</li>

</ol>

chosen at random using the random_token(self, context) method. Your starting context should always be the &amp;GИ/’-tuple (“&lt;START&gt;”, …, “&lt;START&gt;”), and the context should be updated as tokens are generated. If G; /, your context should always be the empty tuple. Whenever the special token “&lt;END&gt;” is encountered, you should reset the context to the starting context.

<ol start="6">

 <li><strong>[5 points] </strong>Write a function create_ngram_model(n, path) which loads the text at the given path and creates an G-gram model from the resulting data. Each line in the file should be treated as a separate sentence.</li>

</ol>

# No random seeds, so your results may vary

&gt;&gt;&gt; m = create_ngram_model(1, “frankenstein.txt”); m.random_text(15)

‘beat astonishment brought his for how , door &lt;END&gt; his . pertinacity to I felt’

&gt;&gt;&gt; m = create_ngram_model(2, “frankenstein.txt”); m.random_text(15)

‘As the great was extreme during the end of being . &lt;END&gt; Fortunately the sun’

&gt;&gt;&gt; m = create_ngram_model(3, “frankenstein.txt”); m.random_text(15)

‘I had so long inhabited . &lt;END&gt; You were thrown , by returning with greater’

&gt;&gt;&gt; m = create_ngram_model(4, “frankenstein.txt”); m.random_text(15)

‘We were soon joined by Elizabeth . &lt;END&gt; At these moments I wept bitterly and’

<ol start="7">

 <li><strong>[5 points] </strong>Suppose we define the perplexity of a sequence of F tokens ⅩP<sub>/</sub>*P<sub>0</sub>*—*P<sub>F </sub>Ⅺ to be</li>

</ol>

ИИИИИИИИИИИИИИИ

ИИИИИИИИИИИИИИИ

,         /

<ul>

 <li>, /&amp;P<sub>/</sub>*P<sub>0</sub>*—*P<sub>F </sub>‘</li>

</ul>

For example, in the case of a bigram model under the framework used in the rest of the assignment, we would generate the bigrams

Ⅹ&amp;P<sub>. </sub>; ⅩQR?PRⅪ*P<sub>/</sub>‘*&amp;P<sub>/</sub>*P<sub>0</sub>‘*—*&amp;P<sub>FИ/</sub>*P<sub>F </sub>‘*&amp;P<sub>F </sub>*P<sub>F)/ </sub>; ⅩCLBⅪ’Ⅺ, and would then compute the perplexity as

GИИИИИИИИИИИИИИ

<ul>

 <li>F,)/ /    ,</li>

</ul>

FD)/

<sub>B;</sub>/ /&amp;PBУPBИ/’

Intuitively, the lower the perplexity, the better the input sequence is explained by the model. Higher values indicate the input was “perplexing” from the model’s point of view, hence the term perplexity.

In the NgramModel class, write a method perplexity(self, sentence) which computes the G-grams for the input sentence and returns their perplexity under the current model. <em>Hint: Consider performing an intermediate computation in log-space and reexponentiating at the end, so as to avoid numerical overflow.</em>


