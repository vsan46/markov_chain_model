# Two Markov Chain Models

## How the Simulations Work
A Markov Chain simulation models a sequence of events where the probability of the next event depends only on the current state. This "memoryless" property is known as the Markov Property.

Both simulations work on the same two-step principle:

Define States and Transitions: Identify the possible states (e.g., 'Sunny'/'Rainy' or 'the'/'cat'/'dog') and the probabilities of moving from one state to another (the "transition matrix").

Run the Simulation: Start at an initial state and repeatedly "roll the dice" to determine the next state based on the transition probabilities.

### How the Simple Model Works
States: The states are simple: Sunny and Rainy.

Transition Matrix: The transitions dictionary explicitly defines the probabilities. For example, transitions['Sunny']['Rainy'] = 0.2 means there is a 20% chance of moving from 'Sunny' to 'Rainy'.

Simulation: The for loop is the simulation. In each step, it looks at the current_state (e.g., 'Sunny'), gets its probabilities ({'Sunny': 0.8, 'Rainy': 0.2}), and uses random.choices to pick the next state. This new state becomes the current_state for the next loop iteration.

Summary: This model simulates basic weather changes. The "state" is either 'Sunny' or 'Rainy'. The simulation steps through 10 "days," deciding the next day's weather based only on the current day's weather.

[simple_weather_simulation.ipynb](https://github.com/vsan46/markov_chain_model/blob/1a773fb8453e8baff161f30a295e464b00df9eae/simple_weather_simulation.ipynb)


### How the Complex Model Works
This model follows the exact same logic, but the states and transitions are not defined manually; they are learned from data.

States: The states are the individual words in the source_text (e.g., 'the', 'cat', 'sat', 'on', etc.).

Transition Matrix (Training): The train method builds the transition matrix. It reads the text and counts how many times each word follows another. For example, it sees "the cat," "the mat," "the dog" (twice), "the cat," and "the mouse." From this, it calculates the probabilities:

From 'the', the next word is 'cat' (2/6 times), 'mat' (1/6), 'dog' (2/6), or 'mouse' (1/6). These probabilities are stored in self.probabilities.

Simulation (Generation): The generate_text method is the simulation. It starts with a word, looks up its probabilities in the self.probabilities matrix, and uses random.choices to pick the next word. It repeats this process, "walking" through the chain of probabilities to create a new sentence.

Summary: This model uses a Markov Chain to generate new text based on a source text. The "state" is the current word. The model first trains itself by analyzing the source text to build a transition matrix (learning the probability of which word follows any given word). Then, it simulates (generates) new text by hopping from word to word based on those probabilities.

[complex_text_generator.ipynb](https://github.com/vsan46/markov_chain_model/blob/1a773fb8453e8baff161f30a295e464b00df9eae/complex_text_generator.ipynb)
