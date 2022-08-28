# Ch. 2 Intelligent Agents

- agent- anything that perceives its environments through sensors and acts upon that environment through actuators
- percept- content an agent's sensors are perceiving
- percept sequence- complete history of everything the agent has ever perceived
- agent function- maps any given percept sequence to an action
- *As a general rule, it is better to design performance measures according to what one actually wants to be achieved in the environment, rather than according to how one thinks the agent should behave.*
- rational agent- *For each possible percept sequence, a rational agent should select an action that is ex- pected to maximize its performance measure, given the evidence provided by the percept sequence and whatever built-in knowledge the agent has.*
- Doing actions *in order to modify future percepts*—sometimes called information gathering—is an important part of rationality
- autonomy- agent does not rely on the prior knowledge of its designer and instead uses its own percepts and learning processes
- Just as evolution provides animals with enough built-in reflexes to survive long enough to learn for themselves, it would be reasonable to provide an artificial intelligent agent with some initial knowledge as well as an ability to learn. After sufficient experience of its environment, the behavior of a rational agent can become effectively *independent* of its prior knowledge.
- specify the task environment with performance metric, environemnt, actuators, and sensors
- fully oversvable environent- agent's sensors give it access to the complete state of the environment at each point in time
    - effectively fully observable if sensors detect all relevant aspects to the choice of action (depends on the performance measure)
- partially observable environment- due to noisy or inaccurate sensors and because parts of the state are missing from the sensor data
    - most environments
- multi-agent systems are defined by where other objects behavior can be described as maximizing a performance measure that is dependent on agent A's behavior
    - ex: chess is competitive multiagent, driving is partially cooperative multiagent (trying to avoid collisions)
    - has different rational behaviors than single-agent environments (e.g. communication and randomized behaviors)
- deterministic- next state of environment completely determined by current state and action executed by the agent(s)
    - most cases are nondeterministic
        - stochastic is slightly different and deals with probabilities instead of unquanitied possibilities
- The hardest case is *partially observable*, *multiagent*, *nondeterministic*, *sequential*, *dynamic*, *continuous*, and *unknown*
- agent = architecture + program
    - programs will take current percept as input from sensors and return an action to the actuators
    - (agent function may depend on entire percept history)

### Types of Agents

- Simple Reflex Agent- select actions on the basis of the current percept
- Model-based Reflex Agents- maintain an internal state that depends on the percept history and reflects some of the unobserved aspects of the current state
    - uses a sensor model (knowledge of how the state of the world is reflected in the agent's percepts) and a transition model (how the world works/changes over time)
    - does not eliminate uncertainty in some unobserved aspects of the world
    - model-free agents can learn what action is best for a percept without ever learning how the action changes the environment
- Goal-based Agents- a model-based reflex agent with the addition of goal information to aid in decision making
    - search and planning are subfields devoted to finding action sequences to achieve an agent's goals
    - this involves imagining counterfactuals (what will happen if i perform this action) in order to achieve a goal in the future (unlike the simple reflex agent that directly maps a percept to an action)
- Utility-based Agents- uses a utility function (an internalization of the performance measure) to decide between multiple action sequences that achieve a goal
    - more flexible than simpler agents (but not necessarily any more rational)