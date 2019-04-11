---
layout: post
title: "Ep 3: Pay some attention to the man behind the curtain!"
date: 2019-04-10
---
<p>&nbsp;</p>
<blockquote>
<p><em>"I thought Oz was a great Head," said Dorothy.</em></p>
<p><em>"And I thought Oz was a lovely Lady," said the Scarecrow.</em></p>
<p><em>"And I thought Oz was a terrible Beast," said the Tin Woodman.</em></p>
<p><em>"And I thought Oz was a Ball of Fire," exclaimed the Lion.</em></p>
<p><em>"No, you are all wrong," said the little man meekly. "I have been making believe."</em></p>
<p><em>"Making believe!" cried Dorothy. "Are you not a Great Wizard?"</em></p>
<p><em>"Hush, my dear," he said. "Don't speak so loud, or you will be overheard--and I should be ruined. I'm supposed to be a Great Wizard."</em></p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - Frank Baum, The Wonderful Wizard of Oz, 1900</p>
</blockquote>
<p>&nbsp;</p>
<p>Tools for text analysis can feel a bit like magic. Upload Shakespeare&rsquo;s corpora and press a few buttons, and you&rsquo;re well on your way to a seemingly limitless array of fancy graphs, statistics, and interactive visualizations. While these tools are useful, and I am not advocating that interested students shy away from them, I would like to make the case that using these tools without understanding the underlying processes by which they work is a bit like trusting a great and powerful wizard whose true form you may or may not have actually seen.</p>
<p>&nbsp;In the software world, the Wizard of Oz (and many DH applications!) would be referred to as a &ldquo;black box.&rdquo; According to <a href="https://en.wikipedia.org/wiki/Black_box">Wikipedia</a>, &ldquo;a <strong>black box</strong> is a device, system or object which can be viewed in terms of its inputs and outputs...without any knowledge of its internal workings.&rdquo; Black box software is everywhere, and it&rsquo;s a good thing, too&mdash;life would be a lot more challenging if sending an email required us to understand everything that was going on behind the scenes.</p>

<p>When conducting research in the digital humanities, however, black box software is a double-edged sword. The ability to conduct an analysis while remaining relatively blind how the analysis works allows for relative newcomers to the field of DH to explore what is possible in the realm of computational text analysis. In the long run though, this type of software can be incredibly limiting. &nbsp;</p>

<p>You see, behind the pretty interface, there is a lot going on. And although it can be nice to not have to think about all that, it&rsquo;s important to recognize that &ldquo;all that&rdquo; can actually have a pretty large impact on the results of any given analysis. As it happens, most analyses have several parameters that can be changed/adjusted, and these changes can have a pretty drastic effect on the output. Furthermore, the steps that you take in cleaning and processing your text can have <em>even more</em> drastic impacts on the results.</p>

<p>Let&rsquo;s explore. We&rsquo;ll use a simple Cluster Analysis as an example. For those of you who are unfamiliar with this type of analysis, check out <a href="https://ncss-wpengine.netdna-ssl.com/wp-content/themes/ncss/pdf/Procedures/NCSS/Hierarchical_Clustering-Dendrograms.pdf">this resource</a>&nbsp; or, for a more simple take, <a href="https://wheatoncollege.edu/wp-content/uploads/2012/08/How-to-Read-a-Dendrogram-Web-Ready.pdf">this one</a>.</p>

<p>&nbsp;In keeping with the Baum-ian theme of this post, I&rsquo;ve created a corpus that contains the first ten Oz books:</p>
<p>&nbsp;</p>
<ol>
<li><em>The Wonderful WIzard of Oz (1900)</em></li>
<li><em>The Marvelous Land of Oz (1904)</em></li>
<li><em>Ozma of Oz (1907)</em></li>
<li><em>Dorothy and the Wizard in Oz (1908)</em></li>
<li><em>The Road to Oz (1909)</em></li>
<li><em>The Emrald City of Oz (1910)</em></li>
<li><em>The Patchwork Girl of Oz (1913)</em></li>
<li><em>Tik-Tok of Oz (1914)</em></li>
<li><em>The Scarecrow of Oz (1915)</em></li>
<li><em>Rinkitink in Oz (1916)</em></li>
</ol>
<p>&nbsp;</p>
<p>I&rsquo;d like to demonstrate how the choices that one makes in pre-processing data can affect the output of an analysis. Specifically, here, we&rsquo;ll be looking at the effects of <em>stemming</em> vs. <em>not stemming</em> vs. <em>lemmatizing</em>. If you aren&rsquo;t familiar which what these terms are, here&rsquo;s a quick rundown.</p>
<p>&nbsp;<strong>Stemming a corpus</strong> entails truncating words to reach their root. Different stemmers follow slightly different rules, but the general premise stays the same. The suffix of a word is stripped away to leave a root. Sometimes the root is an actual English word, but oftenit is not. &nbsp;For example, &ldquo;helping&rdquo; might become &ldquo;help&rdquo;, but &ldquo;troubling&rdquo; might become &ldquo;troubl.&rdquo; In theory, this is supposed to reduce variation within the corpus that might come from different forms of words that don&rsquo;t necessarily have different meanings.</p>
<p><strong>Lemmatization</strong> is a bit more complex of a process, as it ensures that the shortened form of the word is actually a word. It does this by comparing the word to a dictionary of &ldquo;lemmas,&rdquo; and then replacing the word with its lemma form. A lemma is the &ldquo;canonical&rdquo; or &ldquo;dictionary&rdquo; form of a word. Lemmatization can help prevent the conflation of verbs and nouns (ex: &ldquo;I went for a run&rdquo; vs &ldquo;the clock runs slow&rdquo;), and because of this, it is generally seen as a safer way to reduce word form variation is a corpus.</p>
<p>If these definitions aren&rsquo;t clear (or you just want to read more) check out <a href="https://www.datacamp.com/community/tutorials/stemming-lemmatization-python">this resource.</a> &nbsp;</p>
<p>&nbsp;Anyways, moving on. After accessing all ten text files through the Gutenberg library, I removed stop words, using <a href="https://gist.github.com/sebleier/554280">NLTK&rsquo;s list of English stop words</a>. I then made three different versions of the corpus. The first version was left as is&mdash;stop-worded, but not stemmed or lemmatized. The second version was lemmatized using the NLTK&rsquo;s WordNet Lemmatizer. The third version was stemmed using the SnowBall stemmer.</p>
<p>&nbsp;After that, I ran a Cluster analysis of each of the three versions in Stylo. Below, you&rsquo;ll find the results.</p>

<p>&nbsp;<img src="https://github.com/abigailella/abigailella.github.io/blob/master/Unstemmed.png?raw=true" alt="" width="543" height="415" /></p>
<p>&nbsp;</p>
<p>&nbsp;<img src="https://github.com/abigailella/abigailella.github.io/blob/master/SnowballStemmer.png?raw=true" alt="" width="543" height="415" /></p>
<p>&nbsp;<img src="https://github.com/abigailella/abigailella.github.io/blob/master/WNL.png?raw=true" alt="" width="543" height="414" /></p>

<p>&nbsp;</p>
<p>As you can see, despite the fact that I left all analysis parameters the same, the three versions of the corpus each resulted in a fairly unique output.</p>
<p>Looking at the unstemmed corpus and the WordNet Lemmatizer, it seems that <em>The Wonderful Wizard of Oz</em> is a clear outlier. The Snowball Stemmer graph, however, paints a different picture, suggesting that this title is relatively similar to <em>Rinkitink</em> and <em>Marvelous Land</em>. While Snowball and Wordnet pair <em>Road to Oz</em> and <em>Patchwork Gir</em>l, the Unstemmed corpus dendrogram depicts these titles to be far more distant. I&rsquo;m not going to waste your time by writing out all of the ways in which these graphs are different, but feel free to do that yourself. You get the picture though: the list goes on&hellip;</p>

<p>Now that I&rsquo;ve pointed out a few of these differences, I&rsquo;ll reiterate: <strong>I did the exact same analysis on these three versions</strong>. I used the same package, with the same parameters, on the same texts. The only difference was that I preprocessed these texts in different ways. Clearly, this preprocessing step is a pretty important (and in my opinion, sometimes overlooked) step in computational text analysis. Many &ldquo;black boxed&rdquo; tools give the user little to no opportunity to take part in this step.</p>

<p>At this point, you are probably wondering <em>&ldquo;Okay, so what&rsquo;s the best way to pre-process a corpus?&rdquo;</em> While I&rsquo;d love to give a cut-and-dry answer, I&rsquo;m afraid that there may not be one. Scholarship on whether to stem or lemmatize or neither is pretty slim, and I am certainly not qualified enough to have an answer on the topic. I&rsquo;ll explore this a bit more in my next post, but for now, I&rsquo;ll advise readers to check out <a href="https://mimno.infosci.cornell.edu/papers/schofield_tacl_2016.pdf">this article</a> by David Mimno and Alexandra Schofield, in which they explore the effects that stemming/lemmatization have on topic models. They do so in a way that is far more mathematically rigorous than what I am capable of at the moment. (Working on it, y&rsquo;all&hellip;)</p>

<p>Anyways, read up, and get ready to dive back into the lemmatization vs. stemming debate in Episode 4, forthcoming once I catch up on all the laundry I need to do.</p>

<p>Adieu!&nbsp; &nbsp;</p>

