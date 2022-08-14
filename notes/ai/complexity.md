# Complexity

- Reductionism- belief that a whole can be understood completely by understanding its parts and the nature of their sum
    - Rene Descartes 
    - Opposed by phenomena like intelligencewhere complex behavior arrives from large collections of simple components
- Santa Fe Institute created for study of complex systems that require inherently interdisciplinary environment
    - Founded on idea of antireductionism when solving important problems
    - Melanie Mitchell
        - Her adviser, cognitive scientist Douglas Hofstadter @ UMich
- Complex Systems ~ Emergent Computation
- How do we move beyond the traditional paradigm of reductionism toward a new understanding of seemingly irreducibly complex systems?
- four subject areas that are fundamental to the study of complex systems: 
    - information
    - computation
    - dynamics and chaos 
    - evolution
- "Science has explored the microcosmos and the macrocosmos; we have a good sense of the lay of the land. The great unexplored frontier is complexity." - Heinz Pagels, *The Dreams of Reason*
- What we now call “complex systems” can trace its ancestry to cybernetics and the related field of systems science

## Ch. 1 What is Complexity?

- What if we are viewing intelligence from the wrong persepctive
    - Its possible we see intelligence as too singular an end objective that we can engineer models to produce
    - Maybe we need lots of smaller models with simple functionality that interact to create a collective intelligence
        - we can view neural nets from this persepctive since they are made of lots of simple neurons interacting
            - however the limitation of neural nets is that the neuron interactions are very rigid with predifined connections due to the model's architecture. this isn't quite the way the neurons in the brain are connected and could explain some of the shortcomings of neural nets when it comes to true intelligence
    - Maybe a better persepective is that what we consider intelligence is an emergent property of complex systems and that it is not relegated to only a single animal/human brain but can rather include networks of simpler orgnisms such as ants or humans that form a collective "intelligence"
    - Understading the mechanisms that allow ant colonys to express a collective intelligence is still an active area of research
        - Ants have social organizations that allow a colony to collectively do things that increase the survival probability of the community as a whole. Humans are similar with the entire emergence of farming and cities and medicine. Without our social structures, human survival on our own, like ants on their own, is much harder and a lower probability
    - Key aspect of complex systems is the lack of a central controller to organize the simple entities
    - The word *complex* comes from the Latin root *plectere*: to weave, entwine
    - *complex system*: **a system in which large networks of components with no central control and simple rules of operation give rise to complex collective behavior, sophisticated information processing, and adaptation via learning or evolution**
    - Self-organizing Systems- organized behavior arises without an internal or exter- nal controller or leader 
    -  Since simple rules produce complex behavior in hard-to-predict ways, the macroscopic behavior of such systems is sometimes called *emergent*. 
    - alternative definition of a *complex system*: **a system that exhibits nontrivial emergent and self-organizing behaviors**.
    - The central question of the sciences of complexity is how this emergent self-organized behavior comes about
    - *The proper domain of computer science is information processing writ large across all of nature.* —Chris Langton (Quoted in Roger Lewin, *Complexity: Life at the Edge of Chaos*)

### Insect Colonies

- An ant colony, for instance, can consist of hundreds to millions of individual ants, each one a rather simple creature that obeys its genetic imperatives to seek out food, respond in simple ways to the chemical signals of other ants in its colony, fight intruders, and so forth
- build sophisticated colonies, can even build bridges with their bodies for others in the colony to cross
- how did biological evolution produce creatures with such an enormous contrast between their individual simplicity and their collective sophistication?

### The Brain

- global behavior of the brain of perception and conciousness are due to the interactions of billions of simple neurons
- A neuron fires when it receives enough signals from other neurons through its dendrites. *Firing* consists of sending an electric pulse through the axon, which is then converted into a chemical signal via chemicals called *neurotransmitters*. This chemical signal in turn activates other neurons through their dendrites. The firing frequency and the resulting chemical output signals of a neuron can vary over time according to both its input and how much it has been firing recently.
- individuals (neurons or ants) perceive signals from other individuals, and a sufficient summed strength of these signals causes the individuals to act in certain ways that produce additional signals. The overall effects can be very complex.
- unsolved questions:
    - what do neuronal signals mean?
    - How do neurons interact to produce global cognitive behavior?
    - How do the interactions cause the brain to think thoughts and learn new thigs?
    - How did this all emerge from evolution?

### The Immune System

- Complex response to inaders caused by a cascade of signals once a independent cell detects an invader
- We do not yet know precisely how the system avoids attacking the body; or what gives rise to flaws in the system, such as autoimmune diseases, in which the system does attack the body; or the detailed strategies of the human immunodeficiency virus (HIV), which is able to get by the defenses by attacking the immune system itself
    - Figuring out how complex systems like these work is the key to solving many health related issues
    - AI could be critical to the future of healthcare with respect to understanding the body, how its cells work, and the interactions between the systems in the cells

### Economies

- Adam Smith's *invisible hand* that sef-corrects the markets is an example of a complex system at work
    - self-interested individuals make buy/sell decisions that interact to form very hard to predict market behavior

### The Internet

- complex systems scientists have discovered that the network as a whole has many unexpected large-scale properties involving its overall structure, the way in which it grows, how information propagates over its links, and the coevolutionary relationships between the behavior of search engines and the Web’s link structure, all of which lead to what could be called “adaptive” behavior for the system as a whole



## Ch. 2 Dynamics, Chaos, and Prediction

- "It makes me so happy. To be at the beginning again, knowing almost nothing. . . . The ordinary-sized stuff which is our lives, the things people write poetry about—clouds—daffodils—waterfalls...these things are full of mystery, as mysterious to us as the heavens were to the Greeks...It’s the best possible time to be alive, when almost everything you thought you knew is wrong." —Tom Stoppard, *Arcadia*
- Dynamical Systems Theory (dynamics)- describing and predicting behavior of systems with complex changing behavior at the macroscopic level, emerging from the collective actions of many interacting components
    - describe the general ways systems can change, what types of macroscopic behavior are possible, and what kinds of predictions about that behavior can be made
    - Chaos theory is a fasciating subfield of it
    - Started with Artistotle
- Aristotle proposed a law of motion which stated that rest is the natural state of objects
    - This seems to make intuitive sense based on our experience in the day to day world so it is no suprise that this dominated western thinking for hundreds of years until Galileo did experiments and proposed that rest is not the natural state of objects, rather it takes force to stop a moving object. this would be an unintuitive result without the knowledge of air resistance and other hard to see forces that affect all our observations on earth. 
    - galileo launched the scientific revolution with experimental observations at its core
    - newton came right after galileo and invented the science of dynamics (also inventing calculus to describe motion and change along the way)
- Classical Mechanics: Newton's work
    - Kinematics- describes *how* things move
    - Dynamics- describes *why* things follow the laws of kinematics
- Newton's laws are foundation of dynamics:
    1. Constant motion: Any object not subject to a force moves with unchanging speed.
    2. Inertial mass: When an object is subject to a force, the resulting change in its motion is inversely proportional to its mass.
    3. Equal and opposite forces: If object A exerts a force on object B, then object B must exert an equal and opposite force on object A.
- Newtonian mechanics produced a picture of a “clockwork universe,” one that is wound up with the three laws and then runs its mechanical course. The mathematician Pierre Simon Laplace saw the implication of this clockwork view for prediction: in 1814 he asserted that, given Newton’s laws and the current position and velocity of every particle in the universe, it was possible, in principle, to predict everything for all time.
    - Discovery of quantum mechanics demonstrated this idea was not possible 
    - Understanding of chaotic systems (small changes in initial conditions = large changes in resulting behavior; aka sensitive dependence on initial conditions) further demonstrated the idea was not possible
        - small errors in measurement of initial conditons would lead to large errors in long term predictions of behavior 
        - observed before quantum mechanics discovered: Poincare (founder of dynamical systems theory) in 19th century tried to solve 3 body problem of gravitation but was unsuccesful (invented algebraic topology in the process lol)
            - predict the motion of 3 objects exerting gravitational force on one anothe
- Poincare prediccted sensitive depen- dence on initial conditions would make weather prediction impossible
    - Meteorologist Edward Lorenz demonstrated in 60s that even simple computer models of weather were subject to sensitigve depedence on initial conditions
    - even now, weather predicitions dont go beyond a week into the future very succesfully
    - It is not yet known whether this limit is due to fundamental chaos in the weather, or how much this limit can be extended by collecting more data and building even better models. TODO: look into deepmind's paper on predicting the weather to see if more data and better models is able to overcome the perceived sensitve dependence on initial conditions 

### Linearity vs. Nonlinearity

- a linear system can be understood by understanding its parts individually and then putting them together
    - a reductionist's dream
- a nonlinear system's whole is different from the sum of its parts

### Logistic Map

- $x_{t+1} = R x_t (1 - x_t)$
- Type of attractor is one way of characterizing the behavior of a system
- The logistic map is an extremely simple equation and is completely deterministic: every $x_t$ maps onto one and only one value of $x_{t+1}$. And yet the chaotic trajectories obtained from this map, at certain values of *R*, look very random—enough so that the logistic map has been used as a basis for generating pseudo-random numbers on a computer. 
    - Thus apparent randomness can arise from very simple deterministic systems.
- In short, the presence of chaos in a system implies that perfect prediction *à la* Laplace is impossible not only in practice but also *in principle*, since we can never know *x*0 to infinitely many decimal places. This is a profound negative result that, along with quantum mechanics, helped wipe out the optimistic nineteenth-century view of a clockwork Newtonian universe that ticked along its predictable path.
- deeper studies of the logistic map and related maps have resulted in an equally surprising and profound positive result—the discovery of universal characteristics of chaotic systems.
    - even though “prediction becomes impossible” at the detailed level, there are some higher-level aspects of chaotic systems that are indeed predictable.
- The logistic map is a simplified model of population growth, but the detailed study of it and similar model systems resulted in a major revamp- ing of the scientific understanding of order, randomness, and predictability. This illustrates the power of *idea models*—models that are simple enough to study via mathematics or computers but that nonetheless capture fundamental properties of natural complex systems

## Ch. 3 Information

- Why the second law should distinguish between past and future while all the other laws of nature do not is perhaps the greatest mystery in physics
- making a measurement to gain information entails an increase of entropy since acquiring info requires expending work
- In his 1948 paper “A Mathematical Theory of Communication,” Claude Shannon (working @ Bell labs) gave a narrow definition of information and proved a very important theorem, which gave the maximum possible transmission rate (channel capacity) of information over a given channel (wire or other medium), even if there are errors in transmission caused by noise on the channel
    - Shannon Entropy- entropy of the message source that information content is defined in terms of
    - a message can be any unit of communi- cation, be it a letter, a word, a sentence, or even a single bit
    - the entropy (and thus information content) of a source is defined in terms of message probabilities
- Shannon's results led to the development of coding theory for data compression and was also applied to many other fields like crytography, bioinformatics, and ai
- *Information*, as narrowly defined by Shannon, concerns the predictability of a message source
- information theoretic notions such as entropy, information content, mutual information, information dynamics, and others have played central though controversial roles in attempts to define the notion of complexity and in characterizing different types of complex systems.

## Ch. 4 Computation

- 3 big questions on mathematics proposed by David Hilbertin 1900:
    1. Is mathematics complete? given a finite set of axioms, can every mathematical statement be proved/disproved
    2. Is mathematics consistent? can only true statements be proved (proving 1 + 1 = 3 would mean its inconsistent)
    3. Is every statement in mathematics decidable? there is an algorithm that can be applied to every statement that will tell us in finite time whether the statement is true/false
        - decision problem connected to Gottfried Leibniz
- In 1930, Godel presented his incompleteness theorem stating if mathematics is consistent, then it is incomplete and if it is complete, then it is inconsistent
    - Gödel gave an example of a mathematical statement that can be translated into English as: “This statement is not provable.” Let’s call this statement “Statement *A*.” Now, suppose Statement *A* could indeed be proved. But then it would be false (since it states that it cannot be proved). That would mean a false statement could be proved—arithmetic would be inconsistent. Okay, let’s assume the opposite, that Statement *A* cannot be proved. That would mean that Statement *A* is true (because it asserts that it cannot be proved), but then there is a true statement that cannot be proved— arithmetic would be incomplete. Ergo, arithmetic is either inconsistent or incomplete.
        - Godel essentially translated this statement into a mathematical proof
    - This answered the first two questions proposed by Hilbert (shocking many mathematicians in the process)
- Turing demonstrated the answer is no to Hilbert's 3rd question by defining the Turing machine

### Turing Machines

- Consist of 3 parts:
    1. Tape divided into squares/cells on which symbols can be written on and read from (infinitely long in both directions)
    2. Movable read/write tape head that can read symbols from the tape and write symbols to the tape
    3. A set of rules that tell the head what to do next
- Head starts in a special start state and at a particular tape cell
- At each time step, the head reads the symbol at its current tape cell. The head then follows the rule that corresponds to that symbol and the head’s current state. The rule tells the head what symbol to write on the current tape cell (replacing the previous symbol); whether the head should move to the right, move to the left, or stay put; and what the head’s new state is. When the head goes into a special **halt** state, the machine is done and stops.
- The input to the machine is the set of symbols written on the tape before the machine starts. The output from the machine is the set of symbols written on the tape after the machine halts.

### Universal Turing Machines

- A universal turing machine $U$ can emulate a Turing machine $M$ running on an input $I$
- $U$ starts with a tape that encodes the input $I$ and the machine $M$
- At each step *U* reads the current symbol in *I* from the input part of the tape, decodes the appropriate rule from the *M* part of the tape, and carries it out on the input part, all the while keeping track (on some other part of its tape) of what state *M* would be in if *M* were actually running on the given input.
- When *M* would have reached the **halt** state, *U* also halts, with the input (now output) part of its tape now containing the symbols *M* would have on its tape after it was run on the given input *I*.
- Led to the development a decade later of programmable computers that developed into the modern computers we have today

### Turing's Solution to the Decision Problem

- Relies on fact that a turing machie $M_1$ (encoded on a tape) can be fed as input to another Turing machine $M_2$
- By the assumption that the answer is yes to the decision problem, there is some definite procedure that, given *M* and *I* as input, will decide whether or not this particular statement is true. Turing’s proof shows that this assumption leads to a contradiction.
    - assuming answer is yes is equivalent to saying we can design a turing machine $H$ to detect infinite loop (detect if a program halts, aka the halting problem)
- Turing proved by contradiction that there is no algorithm that can solve the halting problem wich demonstrates the answer to the decision problem (does every mathematical statement have an algorithm that can decide its truth value) is no
- Turing used similar techniques as Godel in his proof-- encoding mathematical statemenets. 
    - He encoded them as Turing machines so that they can run each other
- Summary of turing's accomplishments:
    1. he rigorously *defined* the notion of “definite procedure.” 
    2. his definition, in the form of Turing machines, laid the groundwork for the invention of electronic programmable computers. 
    3. he showed what few people ever expected: there are limits to what can be computed.

## Ch. 5 Evolution

- "In a single stroke, the idea of evolution by natural selection unifies the realm of life, meaning, and purpose with the realm of space and time, cause and effect, mechanism and physical law." --Daniel Dennett
- Darwin did not come up with the idea of evolution all on his own
    - George Louis Leclerc de Buffon proposed idea of evolution 100 years before Darwin
    - Jean-Baptiste Lamarck was a prominent pre-darwin evolutionist, though his ideas were rejected by his contemporaries (including fellow evolutionists). they did turn out to be wrong but they influenced Darwin
    - SImilarly, Darwin's grandfather also belived in evolution of species from a single ancestor
    - Science is not an act of lone genius, rather we stand on the shoulders of giants to see further ahead
- HMS Beagle voyage gave him exposure to the following ideas from books/readings and physical measurements/observations
    - Gradual change over long periods can produce very large effects (Charles Lyell’s *Principles of Geology*)
    - Population growth combined with limited resources creates a struggle for existence (Thomas Malthus’s *Essay on the Principle of Population*)
    - Collections of individuals acting in self-interested ways produce global benefit (Adam Smith's Wealth of Nations and the invisible hand)
    - Life seems to allow almost infinite variation, and a species’ particular traits seem designed for the very environment in which the species lives.
    - Species branch out from common ancestors.
- Eventually arrived at a coherent theory of evolution by natural selection:
    - Individual organisms have more offspring than can survive, given limited food resources. 
    - The offspring are not exact copies of the parents but have some small amount of random variation in their traits. 
    - The traits that allow some offspring to survive and reproduce will be passed on to further offspring, thus spreading in the population. 
    - Very gradually, through reproduction with random variation and individual struggles for existence, new species will be formed with traits ideally adapted to their environments
- Alfred Russell Wallace had also come up with the idea of evolution by natural selection at the same time and independetly. this led to them publishing their work together
    - A year later darwin published his book *On the Origin of Species*
- Major ideas of Darwin's theory:
    - Evolution has occurred; that is, all species descend from a common ancestor. The history of life is a branching tree of species.
    - Natural selection occurs when the number of births is greater than existing resources can support so that individuals undergo competition for resources.
    - Traits of organisms are inherited with variation. The variation is in some sense *random*—that is, there is no force or bias leading to variations that increase fitness (though, as I mentioned previously, Darwin himself accepted Lamarck’s view that there are such forces). Variations that turn out to be adaptive in the current environment are likely to be *selected*, meaning that organisms with those variations are more likely to survive and thus pass on the new traits to their offspring, causing the number of organisms with those traits to increase over subsequent generations.
    - Evolutionary change is constant and gradual via the accumulation of small, favorable variations.
- Entropy decreases (living systems become more organized as opposed to less as 2nd law of thermodynamics says would happen for an isolated system) because natural selection performs work (the energy for this work comes from individual organisms metabolizing energy from their environments)
- Darwin's theory predated the discovery of DNA (the mechanism explaining how traits get passed from parent to offspring and how variation in those traits occur- mutations/errors during dna repair or replication)
- Mendel’s experiments contradicted the widely believed notion of “blending inheritance”— that the offspring’s traits typically will be an average of the parents’ traits.
- Darwinism and Mendelism were thought to be opposing schools of view until reconciled in the 1920s
    - The Modern Synthesis- wasn't until statistics was developed (by Ronald Fisher & Francis Galton) and applied, that a mathematical framework (population genetics) was concieved that demonstrated the two evidence based theories complemented each other
- Modern Synthesis principles:
    - Natural selection is the major mechanism of evolutionary change and adaptation.
    - Evolution is a gradual process, occurring via natural selection on very small random variations in individuals. Variation of this sort is highly abundant in populations and is not biased in any direction (e.g., it does not intrinsically lead to “improvement,” as believed by Lamarck). The source of individual variation is random genetic mutations and recombinations.
    - Macroscale phenomena, such as the origin of new species, can be explained by the microscopic process of gene variation and natural selection.
- molecular basis of genes- DNA -was not discovered until afterwards (post 1930s and published in 1950s) 
    - furthermore the mechnism by which variation arises-- mutation during DNA replication/repair was discovered after that
- paleontologists disputed the idea of gradual change from darwins theory of evolution due to what appeared to be big leaps in the fossil record. also new tech is making this idea of gradual change due to natural selection come under increasing scrutiny
    - also attacked the idea that all traits were the result of adaptations strictly required for survival and reproduction

## Ch. 6 Genetics

- Transcription: RNA polymerase splits a strand of DNA and creates an anticopy of mRNA (gene is transcribed as mRNA)
- Translation: mRNA leaves the nucleus and goes to a ribosome in the cytoplasm where tRNA is fed in and used to make the protein coded for by the piece of mRNA 
    - when the ribosome gets the stop codon, the protein is released into the cytoplasm where it then goes to perform its function
- The transcription and translation of a gene is called the gene’s *expression* and a gene is *being expressed* at a given time if it is being transcribed and translated.
- All this happens continually and simultaneously in thousands of sites in each cell, and in all of the trillions of cells in your body
- All this complex cellular machinery—the mRNA, tRNA, ribosomes, polymerases, and so forth—that effect the transcription, translation, and replication of DNA are themselves encoded in that very DNA
    - The DNA contains coded versions of its own decoders
- The processes sketched above were understood in their basic form by the mid-1960s

## Ch. 7 Defining and Measuring Complexity

- there is not yet a single science of complexity but rather several different sciences of complexity with different notions of what complexity means
- Science often makes progress by inventing new terms to describe incompletely understood phenomena; these terms are gradually refined as the science matures and the phenomena become more completely understood.
- The diversity of measures that have been proposed indicates that the notions of complexity that we’re trying to get at have many different interacting dimensions and probably can’t be captured by a single measurement scale.

### Size

- Doesn't capture complexity in genomes
- For instance, Humans have 250 times as many base pairs as yeast but an amoeba has 225 times as many base pairs as humans 

### Entropy

- Doesn't capture our intuituve concept of complexity
- A completely random genome would have more complexity than the human genome if using shannon entropy as the measure of complexity
    - though using just the string of base bairs as messages doesn't really capture the idea that the string encodes complexity. the string itself can be arbitrarily "complex" by whatever measure you use, its the resulting behaviors that emerge when the string of dna is used in an organism that we actually want to measure the complexity of

### Logical Depth

- Proposed in early 80s by mathematician Charles Benett
- More complex objects are harder to construct. 
- Measure the number of steps of the Turing machine needed to construct the description of an object,
- Theoretical properties match our intuitions of complexity
- No practical way of measuring this for any natural object of interest

### Thermodynamic Depth

- Proposed in late 80s by Seth Llyod and Heiz Pagels
- Determine “the most plausible scientifically determined sequence of events that lead to the thing itself,” and measure “the total amount of thermodynamic and informational resources required by the physical construction process.”
- Great theoretical properties, not very useful in practice

### Computational Capacity

- The sophistication of what they can compute
- Stephen Wolfram proposed systems are complex if their computational abilities are equivalent to a turing machine

### Statistical Complexity

- Proposed by physicists Jim Crutchfield and Karl Young
- The minimum amount of information about the past behavior of a system that is needed to optimally predict the statistical behavior of the system in the future
- predicting the statis- tical behavior consists of constructing a model of the system, based on observations of the messages the system produces, such that the model’s behavior is *statistically* indistinguishable from the behavior of the system itself.
    - ML could play a role here in constructing a model of the system from training information (how much training information and how many params to predict the system's behavior could be a good measure of complexity)
    - would still be limited by compute and available training data so more complex systems like humans would not be able to be fully modeled and their complexity measured
    - I do think this gives one of the best and most practical definitions so far of complexity (actually I think my interpretation is slightly wrong/diff than what the def actually is-- need to read the paper)
- The quantitative value of statistical complexity is the information content of the simplest such model that predicts the system’s behavior. Thus, like effective complexity, statistical complexity is low for both highly ordered and random systems, and is high for systems in between—those that we would intuitively consider to be complex.
- Has been measured in real-world pheomena (e.g. firing patterns of neurons)

### Fractal Dimension

- The fractal dimension quantifies the number of copies of a self- similar object at each level of magnification of that object
    - Equivalently, fractal dimension quantifies how the total size (or area, or volume) of an object will change as the magnification level changes
- Only perfect fractals—those whose levels of magnification extend to infinity—have precise fractal dimension. For real-world finite fractal-like objects such as coastlines, we can measure only an approximate fractal dimension
- fractal dimension “quantifies the cascade of detail” in an object. That is, it quantifies how much detail you see at all scales as you dive deeper and deeper into the infinite cascade of self-similarity.
- has been applied to measure real-world phenomena but only captures one kind of complexity we want to measure

### Degree of Hierarchy

- Proposed by Herbert Simon (genius polymath) in 1962 paper “The Architecture of Complexity”
- the complex system being composed of subsystems that, in turn, have their own subsystems, and so on
- Simon proposed that the most important common attributes of complex systems are *hierarchy* and *near-decomposibility*
    - Hierarchy- subsystem that have subsystems themselves. similar otion as fractals with self-similar patterns at all scales
    - Near-decomposibility- many more strong interactions within a subsystem than between subsystems
- Simon contends that evolution can design complex systems in nature only if they can be put together like building blocks—that is, only if they are hierachical and nearly decomposible;
- Simon suggests that what the study of complex systems needs is “a theory of hierarchy.”

## Ch. 8 Self-Reproducing Computer Programs

- Von Neumann’s original self-reproducing automaton (described mathemat- ically but not actually built by von Neumann) similarly contained not only a self-copying program but also the machinery needed for its own interpretation.
    - The complete work was eventually published in 1966 as a book, *Theory of Self-Reproducing Automata*

## Ch. 9 Genetic Algorithms

- Two inputs:

    1. Population of candidate algorithms
    2. Fitness function that assigns a fitness value to each candidate algorithm measuring how well it performed the desired task

- Repeat the following steps for some number of *generations*:

    1. Generate an initial population of candidate solutions. The simplest way to create the initial population is just to generate a bunch of random programs (strings), called “individuals.”

    2. Calculate the fitness of each individual in the current population.

    3. Select some number of the individuals with highest fitness to be the

        *parents* of the next generation.

    4. Pair up the selected parents. Each pair produces offspring by

        recombining parts of the parents, with some chance of random mutations, and the offspring enter the new population. The selected parents continue creating offspring until the new population is full (i.e., has the same number of individuals as the initial population). The new population now becomes the current population.

    5. Go to step 2.

- the GA will often evolve a solution that works, but it’s hard to see *why* it works. That is often because GAs find good solutions that are quite different from the ones humans would come up with

- Evolutionary algorithms are a great tool for exploring the dark corners of design space

    - GAs for neural network architecture and hyperparameter tuning?

## Ch. 10 Cellular Automata, Life, and the Universe

- Brain computes in a fundamentally different way than digital computers. Maybe digital computers cannot replicate brain computations at a global scale
- many people have studied computation in nature via an idealized model of a complex system called a *cellular automaton*
- john von neumann showed a cellular automaton with 29 states was equivalent of a universal turing machine
- conway showed game of life is also universal turing machine
- not very good at replicating von-neumann style computations since they are inherently non-von-neumann architecture of parallel computation. therefore the computation is slow and resource inefficient if at all possible for humans to figure out the initial start states
- Wolfram's book *New Kinds of Science* posits that all natural processes are computations (process information according to set of rules)

## Ch. 11 Computing with Particles

- difficult to design cellular automata to perform tasks that require collective decision making among all the cells
- the genetic algorithm managed to evolve a rule whose behavior can be explained in terms of information-processing particles.
    - expirement worked for 1-d cellular automata but could possibly be scaled up to 3-d to explain the computations in the brain as processing information waves

## Ch. 12 Information Processing in Living Systems

- The *meaning* of the input and output information in a Turing machine comes from its interpretation by humans. The meaning of the information created in intermediate steps in the computation also comes from its interpretation (or design) by humans, who understand the steps in terms of commands in a high-level programming language. 
    - This higher level of description allows us to understand computations in a human-friendly way that is abstracted from particular details of machine code and hardware.

## Ch. 13 Analogy Making in Computers

- humans are good at perceiving abstract similarity between two entities or situations by letting concepts “slip” from situation to situation in a fluid way
- takeaways from computer making analogies program:
    - you can’t explore everything, but you don’t know which possibilities are worth exploring without first exploring them. 
    - You have to be open-minded, but the territory is too vast to explore everything; you need to use probabilities in order for exploration to be fair
    - uses ant-colony like optimization algorithm to balance exploration of breadth and depth
    - uses temperature to also control how much exploration is done
- The ultimate goal of AI is to take humans out of the *meaning* loop and have the computer itself perceive meaning. This is AI’s hardest problem. analogy making will likely be part of the solution 

## Ch. 14 Prospects of Computer Modeling

- Models are ways for our minds to make sense of observed phenomena in terms of concepts that are familiar to us, concepts that we can get our heads around 
- Prediction Models vs. Idea Models
    - Preditiction models are usually mathematical and can be used to predict the future state of a system
    - Idea models are relatively simple and meant to gain insights into a general concept without the necessity of making detailed predictions about any specific system (e.g. turing machine, cellular automaton, koch curve, prisoner's dilemma)
- Tit for tat was the optimal strategy in the prisoner's dilemma 
    - retaliated a defection by defecting the next turn
    - forgave a defection if the oppononent began cooperating by also cooperating again
    - never was the first to defect (common trait amongst all the best strategies)
    - *strategy was clear and predictable for the opponent, making cooperation much easier*
    - a genetic algorithm evolved a same/similar strategy to the tit for tat strategy proposed by a mathematician
    - “nice, retaliatory, forgiving, and clear” are the characteristics Axelrod cited as requirements for success in the repeated Prisoner’s Dilemma.
        - “How to Save the Planet: Be Nice, Retaliatory, Forgiving, and Clear.”
- “Five Rules for the Evolution of Cooperation.”
- all models are wrong in some way, but some are very useful for beginning to address highly complex systems. 
    - Independent replication can uncover the hidden unrealistic assumptions and sensitivity to parameters that are part of any idealized model.

## Ch. 15 Network Science

- A major discovery to date of network science is that high-clustering, skewed degree distributions, and hub structure seem to be characteristic of the vast majority of all the natural, social, and technological networks that network scientists have studied.
- the *small-world property*: a network has this property if it has relatively few long-distance connections but has a small average path-length relative to the total number of nodes. 
    - Small-world networks also typically exhibit a high degree of clustering
    - It has been hypothesized that at least two conflicting evolutionary selective pressures are responsible: 
        - the need for information to travel quickly within the system
        - the high cost of creating and maintaining reliable long-distance connections
        - Small-world networks solve both these problems by having short average path lengths between nodes in spite of having only a relatively small number of long-distance connections.
- scale free networks = power law degree distribution (e.g. $1/k^2$ for webpages)
    1. small # hubs 
    2. nodes with degrees over large range of possible values
    3. self similarity (invariant under rescaling)
    4. small-world structure 

## Ch. 16 Applying Network Science to Real-world Problems

- Network science includes techniques that can be applied to a huge domain of fields 
- *preferential attachment*- networks grow in such a way that nodes with higher degree receive more new links than nodes with lower degree.
    - explains the existence of many scale-free networks in the real world
    - other mechanishms also exist that are similar and quite different 
- studying dynamics of information spread, not just the structure of the network, is important open problem in network science
- Cascading failures- one nodes failure shifts lode to other nodes, that overload and subsequeuntly fail causing a domino chain of failures

### The Brain

- Brain has small-world properties which has several benefits from an evolution perspective:
    - more resilient to losing neurons or functional areas (though losing hubs causes more drastic harm)
    - more energy efficient structure since signals are not sent to all neurons/functional areas
    - greatly facilitates synchronization (groups of neurons firing repeatedly) which is a major mechanism by which the brain transmits information efficiently 
- The brain can be viewed as a network at several different levels of description; for example, with neurons as nodes and synapses as links, or with entire *func- tional areas* as nodes and larger-scale connections between them (i.e., groups of neural connections) as links.

### Genetic Regulatory Networks

- Humans and mustard seeds have roughly same number of genes (25k)
- Our complexity is thought to come from the network of genes regulating each other
- regulatory networks are scale free which makes them resilient (important given the transcription process is prone to errors)

## Ch. 17 The Mystery of Scaling

- metabolism does not scale linearly with an organism's mass becuase the corresponding surface area to distribute the by-product heat over would not scale at the same rate, making larger animals overheat
- If you plot a power law on a double logarithmic plot (both axes are log scale), it will look like a straight line, and the slope of that line will be equal to the power law’s exponent
- Power law distributions *are* fractals—they are self-similar at all scales of magnification, and a power-law’s exponent gives the dimension of the corresponding fractal, where the dimension quantifies precisely how the distribution’s self-similarity scales with level of magnification
    - fractal structure is one way to generate a power-law distribution; and if you happen to see that some quantity (such as metabolic rate) follows a power-law distribution, then you can hypothesize that there is something about the underlying system that is self-similar or “fractal-like.”
- metabolic scaling theory came out of network science and fractals and explains the scaling mystery in organisms
- Understanding power-law distributions, their origins, their significance, and their commonalities across disciplines is currently a very important open problem in many areas of complex systems research.

## Ch. 18 Evolution Complexified

- evolutionary developmental biology is answering a lot of questions related to diversity of species and its relationship with genetics and evolution
- genetic regulatory networks allow for much larger space of possibilities than simply the number of genes would indicate (explains large differences in species despite similar number of genes)
- Two types of genes:
    - functional- encode proteins for cell building/maintenance 
    - regulatory- encode proteins for turning off/on other genes by binding to their corresponding DNA sequences and disallowing or allowing RNA to bind to the gene and complete the transcription and translation process
        - regulatory genes can encode for proteins that regulate other regulatory genes, demonstrating how complex the regulation network can get and how large the combinatorial space of possible genetic expressions is which leads to large diversity in organisms
- Stuart Kauffman demonstrated natural selection is in principle not necessary to create a complex creature with Random Boolean Networks (RBNs)
    - a network structure with enough nodes (e.g. gene regulatory network) controlling other nodes will result in the emergence of complex and self-organized behavior
    - turned the idea of evolution over time being the key to organisms' complexity on its head
    - Kauffman’s book, *The Origins of Order* talks more about these ideas
- Developing accurate models of genetic regulatory networks is currently a very active research area in biology
    - RBNs have severe limatations with noise and make lots of simplifying assumptions that make it less accurate model of genetic regulatory networks
- Evolutionary biologist Dan McShea classifies evolutionists into three categories: 
    - adaptationists, who believe that natural selection is primary 
    - historicists, who give credit to historical accident for many evolutionary changes
    - structuralists, such as Kauffman, who focus on how organized structure comes about even in the absence of natural selection
- Evolutionary biology is still working on answering its most important question: How does complexity in living systems come about through evolution?

## Ch. 19 Past & Future of Complex Systems Research

- mathematician Norbert Wiener proposed the science underlying complex systems in both biology and engineering should focus not on the *mass*, *energy*, and *force* concepts of physics, but rather on the concepts of feedback, control, information, communication, and purpose (or “teleology”)
    - created field of cybernetics-- control and communication theory, in machines and animals
- H. Ross Ashby’s “Design for a Brain,” an influential proposal for how the ideas of dynamics, information, and feedback should inform neuroscience and psychology
- Norbert Wiener’s books *Cybernetics* and *The Human Use of Human Beings*, which attempted to provide a unified overview of the field and its relevance in many disciplines
- A similar effort toward finding common principles, under the name of General System Theory, was launched in the 1950s by the biologist Ludwig von Bertalanffy, who characterized the effort as “the formulation and deduc- tion of those principles which are valid for ‘systems’ in general.” 
    - A *system* is defined in a very general sense: a collection of interacting elements that together produce, by virtue of their interactions, some form of system-wide behavior.
- Artificial intelligence, artificial life, systems ecology, systems biology, neural networks, systems analysis, control theory, and the sciences of complexity have all emerged from seeds sown by the cyberneticists and general system theorists. 
    - Cybernetics and general system theory have been largely overshadowed by these offspring disciplines 
- Tough to advance field when we can't even come up with a vocab to describe it adequately (also need the mathematics to describe complex systems in general)
- The mathematician Steven Strogatz puts it this way: “I think we may be missing the conceptual equivalent of calculus, a way of seeing the consequences of myriad interactions that define a complex system. It could be that this ultracalculus, if it were handed to us, would be forever beyond human comprehension. We just don’t know.”
- pursuing these goals will require, as great science always does, an adventurous intellectual spirit and a willingness to risk failure and reproach by going beyond mainstream science into ill-defined and uncharted territory. 
    - “One doesn’t discover new lands without consenting to lose sight of the shore.” - André Gide