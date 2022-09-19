# Search in a Complex Environment

- relaxing the constraint of discrete state space
    - can use objective function and try to find the global max/min
    - when cannot take the gradient of the function, can use other approximation techniques 
        - simulated annlealing, evolutionary aglorithm, ant colony algorithm, particle search optimization

## Simulated Annealing

- Gradient free
- Annealing- heat metal to high temp and then cool down slowly
- decrease a temp over time
    - high temp = agent moves freely
    - low temp = agent moves towards higher objective (hill climbing)
- given enough time, it will converge to the global min with a high probability
- widely used in circuit design, airline scheduling, etc.