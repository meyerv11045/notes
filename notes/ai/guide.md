# AI: A Guide for Thinking Humans

## Neural Networks

- back-propagation is a way to take an error observed at the output units and to “propagate” the blame for that error backward so as to assign proper blame to each of the weights in the network. 
    - Allows back-propagation to determine how much to change each weight in order to reduce the error. 
- Learning in neural networks simply consists in gradually modifying the weights on connections so that each output’s error gets as close to 0 as possible on all training examples
- Backprop overcame the learning limitations of perceptron
- these subsymbolic systems are less brittle on difficult tasks like object recognition compared to symbolic systems however at the cost of explainability/understandability
- Introduction of ImageNet competition in 2012 which was then effectively solved by CNNs in 2017 with a top-5 accuracy of 98% (82% top-1 accuracy)
- unlike CNNs, human perception is highly regulated by the context of the situation 
    - human perception system has more feedback connections than simply feedforward connections 
- adversarial attacks are a huge flaw in DNNs and beg the question are DNNs even learning the things we want?
- a prerequisite to trustworthy moral reasoning is general common sense
    - an understanding of causality is important for common sense as is the ability to make analogies
- understanding limitations of neural networks through studying adversarial attacks

## Reinforcement Learning

- The Q-learning algorithm is a way to assign values to actions in a given state, including those actions that don’t lead directly to rewards but that set the stage for the relatively rare states in which the agent does receive rewards.
    - In an episode of Q-learning, at each iteration the learning agent: figures out its current state, looks up that state in the Q-table, uses the values in the table to choose an action, performs that action, possibly receives a reward, and—the learning step—updates the values in its Q-table.
    - The neural network’s job is to learn what values should be assigned to actions in a given state (acts as the Q-table). Deep Q-Network aka DQN
        - DQN's input is the state and output is the estimated values for each possible action
    - Learning step: adjusting the network weights (via back-propagation) so as to minimize the difference between the current and the previous iteration’s outputs
        - learning a guess from a better guess
        - temporal difference learning- the network learns to make its outputs consistent from one iteration to the next, assuming that later iterations give better estimates of value than earlier iterations
- succcesfull transfer of learned skills in simulation to real world is open problem
- episode- 1 play of the game
- iteration- 1 action and state pair 
- The system doesn’t always choose the action with the highest estimated value in order to balance between exploration and exploitation
- Standard Search for Checkers and Chess: at a given turn, create a partial game tree using the current board position as the root; apply an evaluation function to the furthest layer in the tree and then use the minimax algorithm to propagate the values up the tree in order to determine which move to make
    - Checkers: 6 possible moves; Chess: 35 possible moves; Go: 250 possible moves
    - Go's increased number of possible moves combined with the difficulty in making a good evalution function makes it infeasible to apply this same search strategy to the game
- AlphaGo that beat Lee Sedol used both used an intricate mix of deep Q-learning, “Monte Carlo tree search,” supervised learning, and specialized Go knowledge
    - book has pretty good explanation of how the 3 work together to produce SOA results
    - CNN is used as the evaluation function to kickstart the monte carlo tree search (non exhaustive but rather based on acculumated statistics from random moves chosen probabilistically)
- AlphaZero, unlike its predecessor, it started off with “zero” knowledge of Go besides the rules and was able to beat its predeccesor in all games
-  Charades could be considered a more challenging domain for AI than even Go since it requires sophisticated visual, linguistic, and social understanding
- deep q-learning is terrible at generalizing and seems to be learn very superficial solutions without any actual understanding:
    - shifting the paddle a few pixels up and using a previously trained superhuman agent gives poor results
    - hints that the system didn't even learn the concept of paddle or really anything in the game (overattribution to say it did)
    - also vulnerable to adversarial changes to the state inputs to damage the ability to play well 
- For humans, a crucial part of intelligence is, rather than being able to learn any particular skill, being able to learn to think and to then apply our thinking flexibly to whatever situations or challenges we encounter

## Barrier of Meaning

- Neural networks don't have any understanding of what they are processing (barrier of meaning)
- intuitive physics— the basic knowledge and beliefs humans share about objects and how they behave
- intuitve psychology-- ability to sense and predict the feelings, beliefs, and goals of others
- intuituve biology-- knowledge that biological organisms differ from inanimate objects
- These core bodies of intuitive knowledge constitute the foundation for human cognitive development, underpinning all aspects of learning and thinking, such as our ability to learn new concepts from only a few examples, to generalize these concepts, and to quickly make sense of situations and decide what actions we should take in response
- humans have mental models of important aspects of the world, based on your knowledge of physical and biological facts, cause and effect, and human behavior. These models—representations of how the world works—allow you to mentally “simulate” situations
    - Lawrence Barsalou's "Perceptual Symbol Systems" (1999) in Behavioral and Brain Sciences & "Grounded Cognition" in the Annual Review of Psychology
    - integral part of understanding a situation is being able to use your mental models to imagine different possible futures.
    - simulations appear central to the representation of meaning
    - we understand abstract concepts in terms of core physical knowledge
        - Ex: warm physical feeling and thinking of social warmth activate same brain regions
        - we understand lots of abstract concepts in terms of metaphors relating them to physical knowlege 
            - this could be why more abstract concepts like math can be harder for people to grasp, especially in the absence of using metaphors to teach the concepts
    - analogy making in a very general sense as “the perception of a common essence between two things
    - without concepts there can be no thought, and without analogies there can be no concepts
    - Marvin Minksy's "Decentralized Minds"
    - essentially everyone in AI research agrees that core “commonsense” knowledge (core intuitive knowledge) and the capacity for sophisticated abstraction and analogy are among the missing links required for future progress in AI

## Knowledge, Abstraction, and Analogy

- Works on intuituve physics 
    - N. Watters et al. "Visual Interaction Networks"
    - T.D. Ullman et al. "Mind Game: Game Engines as an Architecture for Intuitive Physics"
    - KK. Kansky eet al. "Schema Networks: Zero-Shot Transfer with a Generative Causal Model of Intuitive Physics"
- For discussion on what is missing in deep learning: G. Marcus "Deep Learning: A Critical Appraisal"
- Bongard problems are good tests of abstraction ability
    - H. E. Foundais "Phaeaco: A Cognitive Architecture Inspired by Bongard's Problems"
- metacognition- the ability to perceive and reflect on one’s own thinking
- “We should be afraid. Not of intelligent machines. But of machines making decisions that they do not have the intelligence to make. I am far more afraid of machine stupidity than of machine intelligence. Machine stupidity creates a tail risk. Machines can make many many good decisions and then one day fail spectacularly on a tail event that did not appear in their training data. This is the difference between specific and general intelligence” -Sendhil Mullainathan
- “People worry that computers will get too smart and take over the world, but the real problem is that they’re too stupid and they’ve already taken over the world” -pedro domingos