# titlechaser

A tool for capitalizing English titles using Python natural language processing tools. Based on [spaCy](https://spacy.io). I assume you already have spaCy available somewhere before running the script.

## Usage

First, you will need to get [spaCy](https://spacy.io/docs/usage/), and the [English model](https://spacy.io/docs/usage/models). I recommend putting them in a virtualenv and then running titlechaser inside it:

```bash
python -m venv venv
source venv/bin/activate
pip install spacy
python -m spacy download en
```

If you pass titlechaser arguments on the command line, it will capitalize each of them:

```bash
titlechaser "A Hitchhiker's Guide to the Galaxy"
A Hitchhiker's Guide to the Galaxy
```

If passed no arguments, titlechaser will accept input line-by-line from stdin:

```bash
titlechaser <<< "A Hitchhiker's Guide to the Galaxy"
A Hitchhiker's Guide to the Galaxy
```

## Headline-Style Capitalization Rules

titlechaser is based on the headline-style capitalization rules outlined in the Chicago Manual of Style (16th edition), section 8.157:

1. capitalize the first and last word
2. capitalize nouns, pronouns, adjectives, verbs, adverbs, and subordinating conjunctions
3. lowercase articles, prepositions, and coordinating conjunctions
4. lowercase "to" in an infinitive verb
5. lowercase "as" in all forms

For hyphenated words, titlechaser follows section 8.159:

1. capitalize the first element
2. capitalize all subsequent elements unless they are articles, prepositions or coordinating conjunctions
3. if the first element is a prefix that could not form its own word, do not capitalize the second element unless it is a proper noun or proper adjective
4. capitalize all segments of a spelled-out number

Of course, the rules can be a lot more nuanced than this (although the current edition of Chicago admits fewer exceptions than older editions did). titlechaser is not a replacement for a professional editor, and it doesn't always do exactly what Chicago says. These are the examples given by Chicago sections 8.158 and 8.159:

- Mnemonics That Work Are Better Than Rules That Do Not
- Singing While You Work
- A Little Learning Is a Dangerous Thing
- Four Theories concerning the Gospel according to Matthew
- Taking Down Names, Spelling Them Out, and Typing Them Up
- Tired but Happy
- The Editor as Anonymous Assistant
- From Homo erectus to Homo sapiens: A Brief History
- Defenders of da Vinci Fail the Test: The Name Is Leonardo
- Sitting on the Floor in an Empty Room
- Ten Hectares per Capita, but Landownership and Per Capita Income
- Progress in In Vitro Fertilization
- Under-the-Counter Transactions and Out-of-Fashion Initiatives
- Bed-and-Breakfast Options in Upstate New York
- Record-Breaking Borrowings from Medium-Sized Libraries
- Cross-Stitching for Beginners
- A History of the Chicago Lying-In Hospital
- The E-flat Concerto
- Self-Sustaining Reactions
- Anti-intellectual Pursuits
- Does E-mail Alter Thinking Patterns?
- A Two-Thirds Majority of Non-English-Speaking Representatives
- Ninety-Fifth Avenue Blues
- Atari's Twenty-First-Century Adherents

And here is how titlechaser thinks they should be capitalized (I have bolded the words where titlechaser disagreed with Chicago):

- Mnemonics **that** Work Are Better **than** Rules **that** Do Not
- Singing While You Work
- A Little Learning Is a Dangerous Thing
- Four Theories **Concerning** the Gospel **According** to Matthew
- Taking Down Names, Spelling Them Out, and Typing Them Up
- Tired but Happy
- The Editor as Anonymous Assistant
- From Homo **Erectus** to Homo **Sapiens**: **a** Brief History
- Defenders of **Da** Vinci Fail the Test: **the** Name Is Leonardo
- Sitting on the Floor in an Empty Room
- Ten Hectares per Capita, but Landownership and **per** Capita Income
- Progress in **in** **vitro** Fertilization
- Under-the-Counter Transactions and Out-of-Fashion Initiatives
- Bed-and-Breakfast Options in Upstate New York
- Record-Breaking Borrowings from Medium-Sized Libraries
- Cross-Stitching for Beginners
- A History of the Chicago Lying-**in** Hospital
- The E-**Flat** Concerto
- Self-Sustaining Reactions
- Anti-**Intellectual** Pursuits
- Does E-**Mail** Alter Thinking Patterns?
- A Two-Thirds Majority of Non-English-Speaking Representatives
- Ninety-Fifth Avenue Blues
- Atari's Twenty-First-Century Adherents

As you can see, titlechaser got pretty close, but it tripped up on some notable corner cases. If you're surprised by what titlechaser does, I recommend lowercasing your sentence and plugging it into [displaCy](https://demos.explosion.ai/displacy/) to see how spaCy tags it.

# Miscellaneous NLP links

I do not study NLP academically in any capacity, so this was quite a new and interesting experiment for me. If you, too, are intrigued, here are some of the links I referred to while writing:

- [Penn Treebank POS tagging guidelines](http://repository.upenn.edu/cgi/viewcontent.cgi?article=1603&context=cis_reports). I think these are out of date (they're from 1990) but they provide some good information on how words get tagged and why.
- [CLEAR dependency style](http://www.mathcs.emory.edu/~choi/doc/clear-dependency-2012.pdf). This explains the symbols that spaCy uses to refer to dependencies between words in the parsed sentence structure.
- [displaCy](https://demos.explosion.ai/displacy/). Parse and tag sentences in your browser! Great for debugging.
