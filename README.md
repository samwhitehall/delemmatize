## What is this?
[Lemmatizing](https://nlp.stanford.edu/IR-book/html/htmledition/stemming-and-lemmatization-1.html) is a common process in Natural Language Processing (NLP) to convert
words from a specific variant into a base form, i.e. the type of word you would
find in a dictionary. For example, to convert "am" to "be".

This is a script to do precisely the opposite; taking a base form of a word, 
and converting it into a specific other grammatical part-of-speech (PoS). For 
example, converting a singular form of a noun into a plural form (NNS).

The algorithm is _crude as heck_ but maybe you will find it useful. I am sure
there are actual well-researched algorithms out there to do this task but I was
too lazy to find one. Maybe it might be good enough for you, or at least help
you get started. 

I developed this for [my OULIPO project](http://oulipo.samwhitehall.com), which 
you should check out if and only if you enjoy experimental poetry.

## How does it work?

1) **Create initial guesses by prefix.** Look at all words in the corpus with
the first three letters of the word.
2) **Apply broad filters.** 
    * Filter out words of a different length (±3).
    * Filter words with a '.' or '-' in.
3) **Filter by lemma match.** Further filter these to words that share the same
lemma.
4) **Filter by PoS tag.** Filter out words which aren't the PoS we're looking
for.
5) **Filter by suffix.** Some PoS should always end with a certain suffix, so 
filter those which don't end with this.
6) **Add regular forms.** Add hypothesis words for what the word would look
like if it is regular and follows patterns.
7) **Filter rare forms.** Remove words which only occur very infrequently in
the corpus.
8) **Pick one.** If there are no matches, just return the original word. If
there are multiple words, pick the most popular.


I did say it was kinda dumb. I've not systematically tested how well it works
(exercise for the reader).

## What do I need?

* **Python 2.7+**: could easily be made Python 3 compatible, I'm sure.
* **spaCy**: an excellent NLP library.
* **docopt**: a tool for parsing command line arguments.
* **some JSON files**: specifically, `nouns.json` and `verbs.json`, each
  containing lists of words.

## How can it be improved?
I'm glad you asked, hypothetical conversationalist. It's not refined in the 
slightest, but if you find it useful and made changes, I'm happy to accept 
PRs. Particularly egregious defects include (but are by no means limited to):

* Not Python 3 compatible.
* The structure (I'm sure nobody wants to have to run a script using JSON 
  files).
* The algorithm, especially its reliance on magic numbers, its ability to
  only manage specific word types, and the general ad hoc way that the
  whole thing works. I'm sure that a more principled/empirically performant
  arrangement of these heuristics exists.
