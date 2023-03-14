# The Marc Of Chains
Ever wondered what Dr Marc Ibrahim is going to send to the class team next? When are the class notes going to be updated? Is tomorrow’s session going to be online or not? Some would say it is unpredictable, maybe even impossible to know.

Not with **The Marc of Chains**: a project set to predict which sequence of words will be sent to the team next using [Markov chains](https://en.wikipedia.org/wiki/Markov_chain#:~:text=A%20Markov%20chain%20or%20Markov,the%20state%20of%20affairs%20now.%22) applied to previously sent messages from previous teams.

Let’s take an example message:

![Are you reccurrent?](https://raw.githubusercontent.com/lebenebou/MarcOfChains/main/pictures/recurrent_joke.png)

Sorry, that must’ve been form my private chat with him. Maybe something more realistic:

![Notes de cours](https://raw.githubusercontent.com/lebenebou/MarcOfChains/main/pictures/notes_de_cours.png)

The Markov chain states are words; given a certain word, the probability of the word to follow can be calculated given its frequency in the message data.

![Word Sequence](https://raw.githubusercontent.com/lebenebou/MarcOfChains/main/pictures/word_sequence.png)

With Dr Ibrahim’s permission, I collected every message he’s ever sent to us on teams in 2021 – 2022 and put them in a text file which can be found in the files section.

## Cleaning The Data

- Convert all uppercase to lowercase
- Fix spelling mistakes and remove apostrophes
- End every sentence with “.”
- Separate every word by a space and consider “.” a word (a state)
- Other minor changes…

After cleaning the data, we should build the core of our Markov model. Each word (state) will have a list of next possible words to follow, the <span style="color: orange;">probability</span> of each word coming next is calculated by its <span style="color: orange">frequency/total</span> occurrences.

**```print(next_possible_words(“faut”))```**

```=> {'regrouper': 0.25, 'faire': 0.25, 'ouvrir': 0.25, 'resoudre': 0.25}```

To generate the next message that will be sent to the team, we must generate a sentence. As we know with Markov chains, an <span style="color: orange;">initial state</span> must be given. Once the <span style="color: orange;">starting word</span> is given, we can keep adding words from the next possible words list until we reach the state “.”.

**```print(generate_sentence(“il”))```**

```=> il faut ouvrir packet tracer sur moodle .```