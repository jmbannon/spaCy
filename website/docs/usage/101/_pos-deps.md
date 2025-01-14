After tokenization, spaCy can **parse** and **tag** a given `Doc`. This is where
the statistical model comes in, which enables spaCy to **make a prediction** of
which tag or label most likely applies in this context. A model consists of
binary data and is produced by showing a system enough examples for it to make
predictions that generalize across the language – for example, a word following
"the" in English is most likely a noun.

Linguistic annotations are available as
[`Token` attributes](/api/token#attributes). Like many NLP libraries, spaCy
**encodes all strings to hash values** to reduce memory usage and improve
efficiency. So to get the readable string representation of an attribute, we
need to add an underscore `_` to its name:

```python
### {executable="true"}
import spacy

nlp = spacy.load("en_core_web_sm")
doc = nlp("Apple is looking at buying U.K. startup for $1 billion")

for token in doc:
    print(token.text, token.lemma_, token.pos_, token.tag_, token.dep_,
            token.shape_, token.is_alpha, token.is_stop)
```

> - **Text:** The original word text.
> - **Lemma:** The base form of the word.
> - **POS:** The simple part-of-speech tag.
> - **Tag:** The detailed part-of-speech tag.
> - **Dep:** Syntactic dependency, i.e. the relation between tokens.
> - **Shape:** The word shape – capitalization, punctuation, digits.
> - **is alpha:** Is the token an alpha character?
> - **is stop:** Is the token part of a stop list, i.e. the most common words of
>   the language?

| Text    | Lemma   | POS     | Tag   | Dep        | Shape   | alpha   | stop    |
| ------- | ------- | ------- | ----- | ---------- | ------- | ------- | ------- |
| Apple   | apple   | `PROPN` | `NNP` | `nsubj`    | `Xxxxx` | `True`  | `False` |
| is      | be      | `VERB`  | `VBZ` | `aux`      | `xx`    | `True`  | `True`  |
| looking | look    | `VERB`  | `VBG` | `ROOT`     | `xxxx`  | `True`  | `False` |
| at      | at      | `ADP`   | `IN`  | `prep`     | `xx`    | `True`  | `True`  |
| buying  | buy     | `VERB`  | `VBG` | `pcomp`    | `xxxx`  | `True`  | `False` |
| U.K.    | u.k.    | `PROPN` | `NNP` | `compound` | `X.X.`  | `False` | `False` |
| startup | startup | `NOUN`  | `NN`  | `dobj`     | `xxxx`  | `True`  | `False` |
| for     | for     | `ADP`   | `IN`  | `prep`     | `xxx`   | `True`  | `True`  |
| \$      | \$      | `SYM`   | `$`   | `quantmod` | `$`     | `False` | `False` |
| 1       | 1       | `NUM`   | `CD`  | `compound` | `d`     | `False` | `False` |
| billion | billion | `NUM`   | `CD`  | `probj`    | `xxxx`  | `True`  | `False` |

> #### Tip: Understanding tags and labels
>
> Most of the tags and labels look pretty abstract, and they vary between
> languages. `spacy.explain` will show you a short description – for example,
> `spacy.explain("VBZ")` returns "verb, 3rd person singular present".

Using spaCy's built-in [displaCy visualizer](/usage/visualizers), here's what
our example sentence and its dependencies look like:

import DisplaCyLongHtml from 'images/displacy-long.html'; import { Iframe } from
'components/embed'

<Iframe title="displaCy visualization of dependencies and entities" html={DisplaCyLongHtml} height={450} />
