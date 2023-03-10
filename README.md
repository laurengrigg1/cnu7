# Week 7 workshop: Population models

This week you'll be **pair programming**. Choose one of you to be the driver first; then, every 15 minutes or so, **swap roles**. The driver writes code and shares their screen, the navigator is an active observer/helper.

Work in the script `population.py`.

## Modelling fish populations

An important application of computational mathematics is to produce simulations to guide policy making. These simulations are based on mathematical models, and use numerical methods to compute solutions for different parameter values. In a simulation, every parameter can be changed independently to observe its influence on the results; you could see it as running "numerical experiments" to better understand and predict the behaviour of a complex system.

An example of this, which we are all very familiar with by now, is the `CovidSim` model developed at Imperial College ([available in full on Github](https://github.com/mrc-ide/covid-sim) -- the time-stepping happens [right there](https://github.com/mrc-ide/covid-sim/blob/master/src/CovidSim.cpp#L3179)). Another example is the [Met Office's computational model](https://www.metoffice.gov.uk/research/approach/modelling-systems/unified-model/index) for weather prediction, which computes solutions to the differential equations which govern the dynamics of the atmosphere, using a time-stepping method. Beyond public health and weather forecasting, simulations are also used to guide policy in economics, energy, environment and sustainability, traffic and transportation...

Today, you have been tasked to advise the Scottish government on **fishing policy**. Your will produce simulations of the evolution of a fish population over time, depending on the resources available in their habitat, how fast they reproduce, and the rate at which they are caught by fishermen. Your goal is to help the government set quotas to avoid overfishing and endangering fish populations. The model we will use is the **logistic population growth** model.

Let P(t) represent a population of fish (the number of individuals) at time t (in weeks). The following differential equation models the evolution of P(t) over time:

dP/dt = kP(1 - P/K) - m

where k is the rate at which these fish reproduce (the number of new baby fish per week), K is the *carrying capacity* of this population (the maximum number of fish that the environment can sustain in the long run -- this depends on the amount of food available, for instance), and m is the number of catches each week by fishermen.

## Task 1: building the simulation

Approximate the derivative dP/dt in the ODE with the forward difference operator, and rearrange the resulting difference equation into a recursive formula. Using this formula, program a simulation of the evolution of P(t) over time. (See the last part of the Week 7 tutorial for an example with a different ODE.)

Use the following parameters:
- Total simulation time: 5 years
- Time step: 1 day
- k = 0.1
- K = 1000
- m = 10

If the population drops to zero at a given time step, you should interrupt the simulation.

Compute solutions for different initial populations P(0) = 300, 600, 900, 1200, 1500, and plot them all on the same graph, with the time (in weeks) on the x-axis.

Do the results correspond to what you expected? Why/why not?

## Task 2: setting quotas

Set P(0) = 500. This time, compute solutions for different fishing rates; try values of m between 10 and 30. Plot the results on the same graph.

For these fixed values of the initial population, k, and K, can you find the maximum number of catches which can be made each week without risking the fish to go extinct?

Produce more simulations to explore whether these quotas should change depending on the initial population, the reproduction rate k, and the carrying capacity K.

## Task 3: seasonal changes

The model can be refined by considering that the carrying capacity K might change over time. For example, the amount of food available to the fish may be smaller in the winter than in the summer.

Adapt your model so that the carrying capacity K(t) is a periodic function, with a period of 1 year, representing seasonal changes. You can use a sinusoid with a given amplitude and offset to represent this.

Explore whether quotas should be adapted depending on the amplitude of seasonal variations in the carrying capacity.

## Task 4: backward Euler

Discretise the ODE using the backward Euler method -- i.e. using the backward difference operator to approximate the derivative, instead of the forward difference operator. How would you proceed to compute the solution using this method?
