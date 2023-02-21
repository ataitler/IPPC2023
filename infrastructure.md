<p style="font-size:30px;text-align:center"><b>RDDL and the pyRDDLGym Infrastructure</b></p>

The problems in this year's competition will be described in the RDDL language.
RDDL is intended to compactly support the representation of a wide range of relational MDPs and POMDPs and support the efficient simulation of these domains. The domains will be simulated via autogenerating environment simulator and interacted via the standard [Gym](https://www.gymlibrary.dev/) interface. Simply put, the pyRDDLSim takes textual problem description in RDDL, and generates a gym environment without writing a single line of python code.


# Getting started with RDDL

The following tutorial covers RDDL basics and how to run it in pyRDDLGym:
- [pyRDDLGym RDDL tutorial](pyrddlgym_rddl_tutorial.html)


For those who wish to learn RDDL at a later time, it is possible to just skip ahead for the next section, without knowing RDDL (and use the existing environemnts), pyRDDLGym is a fully gym compatible simulator, and can be treated as such, with the knowledge that the environments are not written in python but in RDDL.

The RDDL language guide which documents all the language components is also available here:
- [RDDL language guide](http://users.cecs.anu.edu.au/~ssanner/IPPC_2011/RDDL.pdf)

Please cite as

```
@unpublished{Sanner:RDDL,
      author = "Scott Sanner",
      title = "Relational Dynamic Influence Diagram Language (RDDL): Language Description",
      note = "http://users.cecs.anu.edu.au/~ssanner/IPPC_2011/RDDL.pdf",
      year = 2010}
```


### Legacy RDDL
RDDL is out there since 2010, with a JAVA simulator and an excellent tutorial, explaining step by step with the help of a simple and illustrative example the power of RDDL and how to describe an MDP as an RDDL domain and instance. 

- [RDDL tutorial](https://sites.google.com/site/rddltutorial/)
- [JAVA RDDLSim](https://github.com/ssanner/rddlsim)

**Note**: the 2023 competition is fully in python and the old simulator will not be used.


# pyRDDLGym

pyRDDLSim is a generic autogeneration simulator from RDDL files to OpenAI Gym environments.

## Paper 
Please see our [paper](https://arxiv.org/abs/2211.05939) describing pyRDDLGym.

## Status 
pyRDDLSim implements a large subset of the full RDDL capabilities, with additional new capabilities not originaly present in RDDL.

What listed bellow is a list of what we currently do not support:
* state-action-constraints -- deprecated in favor of state-invariants and action-preconditions (RDDL2.0).
* action-preconditions are not enforced by the environment, and should be incorporated into the cpfs definitions.
* action-preconditions of structure of `action <= BOUND` and `action >= BOUND`
where BOUND is deterministic-function (can be of constants or non-fluents),
are supported for the porpuse of gym spaces definitions.
* General action-preconditions can still be specified in the rddl file for the benefit of reasoning in planners.
* enums

We have extended the RDDL language and also support the following:
* Automatic reasoning of levels. Levels are no longer required (and ignored by the infrastructure).
* Terminal states can now be explicitly defined. The termination block has been added to the language.

All other features of RDDL are supported according to the language definition.

## Getting started
There are two options at the moment to obtain the pyRDDLGym infrstructure
1. Pip installation `pip install pyRDDLGym` \
In order to avoid any package conflicts we recommand using a virtual environment:
```bash
conda create -n rddl python=3.7
conda activate rddl
pip install pyrddlgym
```
2. Cloning directly from Github `https://github.com/ataitler/pyRDDLGym.git`


Please refer to the [README page](https://github.com/ataitler/pyRDDLGym) for information on the framework contents, requirements, examples, and more.

## Basic usage

### Initializing Environments
Initializing environments is very easy in pyRDDLGym and can be done via: 
```python
from pyRDDLGym import RDDLEnv
myEnv = RDDLEnv.RDDLEnv(domain="domain.rddl", instance='instance.rddl')
```
where `domain.rddl` and `instance.rddl` are rddl files of your choosing.

### Built in environments
puRDDLGym is shiped with 12 environments designed completly in RDDL. The RDDL files are part of the distribution and can be accessed.
In order to use the built in environments and keep the api of the RDDLEnv standard we supply an ExampleManager class:
```python
from pyRDDLGym import ExampleManager
ExampleManager.ListExamples()
```
The `ListExample()` static function lists all the example environments in pyRDDLGym
Then in order to retrive the informaiton of a specific environment:
```python
EnvInfo = ExampleManager.GetEnvInfo(ENV)
```
Where ENV is a string name of the desired example. \
Setting up an environment at the point is just
```python
myEnv = RDDLEnv.RDDLEnv(domain=EnvInfo.get_domain(), instance=EnvInfo.get_instance(0))
```
Where the argument of the method `get_instance(<num>)` is the ID number of the instance (0 in this case).
Listing all the available instances of the problem is accessed via
```python
EnvInfo.list_instances()
```
Last, setting up the dedicated visualizer for the example is done via
```python
myEnv.set_visualizer(EnvInfo.get_visualizer())
```


### Interacting with the Environment
pyRDDLGym is build on Gym as so implements the classic “agent-environment loop”. 
The infrastructure comes with two simple agents:

1. **NoOpAgent** - which allows the environment to evolve according to the default behavior as specified in the RDDL file.
2. **RandomAgent** - which sends a rendom action according to the env.action_space and the maximum number of allowed concurrent actions as specified in the RDDL file.


Using a pre existing agent, or using of of your own is as simple as:
```python
from Policies.Agents import RandomAgent
agent = RandomAgent(action_space=myEnv.action_space, num_actions=myEnv.NumConcurrentActions)
```

Let’s see what a complete the agent-environment loop looks like in pyRDDLGym.
This example will run the Example `MarsRover`
The loop will run for the amount of time steps specified in the environment's `horizon` field. If the env.render() function will be used we will also see a window pop up rendering the environment
```python
from pyRDDLGym import RDDLEnv
from pyRDDLGym import ExampleManager
from pyRDDLGym.Policies.Agents import RandomAgent

# get the environment info
EnvInfo = ExampleManager.GetEnvInfo('MarsRover')

# set up the environment class, choose instance 0 because every example has at least one example instance
myEnv = RDDLEnv.RDDLEnv(domain=EnvInfo.get_domain(), instance=EnvInfo.get_instance(0))
# set up the environment visualizer
myEnv.set_visualizer(EnvInfo.get_visualizer())

# set up an aget
agent = RandomAgent(action_space=myEnv.action_space, num_actions=myEnv.NumConcurrentActions)

total_reward = 0
state = myEnv.reset()
for _ in range(myEnv.horizon):
      myEnv.render()
      next_state, reward, done, info = myEnv.step(agent.sample_action())
      total_reward += reward
      state = next_state
      if done:
            break
myEnv.close()
```

### Lifted vs Grounded Representations

RDDL is a lifted language, which means it compactly describes variables and processes in a general non-specific way. It is best explained with an example.
The following block describes the behavior of an abstract entity car, with first order dynamics:

```python
types {
      car : object;
};

pvariables{
      DT            : { non-fluent, real, default=0.1 };
      position(car) : { state-fluent, real, default=0.0 };
      velocity(car) : { action-fluent, real, default=0.0 };
};

cpfs {
      position'(car) = position(car) + DT * velocity(car)
};
```
This is a behavior description, this type of code can be found in the domain block of the RDDL code. In the code above no specific car is described. that will be done in the instance and non-fluents blocks. first we should define the objects in the problem:
```python
objects {
      car : {car1, car2};
};
```
Now that we have specific car objects, we can define their intial state:
```python
init_state {
      position(car1) = -1.0;
      position(car2) = 1.0;
};
```
So in the lifted description we have behavior, types and objects for instantiation. When pyRDDLGym instantiate an environment it will *ground* everything, which means we will no longer have types and objects, we will have only effects and evolutions over the explicit variables of the problem, i.e., the variables of the problem will be (with their initial values):
``` python
states = { position_car1 : -1.0, position_car2 : 1.0 }
actions = { velocity_car1 : 0.0, velocity_car2 : 0.0 } 
```
and the explicit effect will be:
```python
position_car1 = position_car1 + DT * velocity_car1;
position_car2 = position_car2 + DT * velocity_car2;
```
The power of the lifted representation is the ability to easily specify different objects (and many of them), and in reasoning.
When interactingn with pyRDDLGym environment, the states recieved and actions submitted are always specific (e.g., setting the velocity of car1) and thus grounded.

- *Note* the name conversions between the lifted and the grounded representation.

### Spaces

The state and action spaces of pyRDDLGym are standard `gym.spaces`, and inquireable througth the standard API: `env.state_space` and `env.action_space`.
State/action spaces are of type `gym.spaces.Dict`, where each key-value pair where the key name is the state/action and the value is the state/action current value or action to apply.

Thus, RDDL types are converted to `gym.spaces` with the appropriate bounds as specified in the RDDL `action-preconditions` and `state-invariants` fields.
The conversion is as following:
- real -> Box with bounds as specified in `action-preconditions`, or with `np.inf` and symetric bounds.
- int -> Discrete with bounds as specified in `action-preconditions`, or with `np.inf` and symetric bounds.
- bool -> Discrete(2)

There is no need in pyRDDLGym to specify the values of all the existing action in the RDDL domain description, only thus the agent wishes to assign non-default values, the infrastructure will construct the full action vector as necessery with the default action values according to the RDDL description.

Note: enum types are not supported by pyRDDLGym at this stage.

### Constants
RDDL allows for the constants of the problem instead of being hardcoded, to be specified and in the non-fluent block of the instance. Meaning every instance can have different constants, e.g., different bounds on action, different static object location, etc.

While these constants are not available through the state of the problem, it is possible to access them through gym (or directly through the RDDL description) with a dedicated API: `env.non_fluents`. The non_fluents property returns a python dictionary where the keys are the grounded non-fluents and the values are the appropriate values. 

### Termination
An Addition made to the RDDL language during the development of this infrastructure is the termination block.
The termination block is intended to specify terminal states in the MDP, when reached the simulation will end. A terminal state is a valid state of the MDP (to emphesize the difference ob state-invariants). An example of terminal state can be any state within the goal set for which the simulation should not continue, or a state where there are no possible actions and the simulation should end, e.g., hitting a wall when it is not allowed. When a terminal state is reached the state is returned from the environment and the `done` flag is returned as True. The reward is handled independently by the reward function, thus if there is a specific reward for the terminal state, it should specified in the reward formula. The termination block has the following syntax:
```python
termination {
	Terminal_condition1;
	Terminal_condition2;
	...
};
```
where `Terminal_condition#` are boolean formulas. The termination decision is a disjunction of all the conditions in the block (termination if at least one is True).

### Visualization

pyRDDLGym visualization is just like regular Gym. Users can visualize the current state of the simulation by calling `env.render()`. The standard visualizer that comes out of the box with every pyRDDLGym domain (even used defined domain will have it without explicitly doing anything) is the TextViz. TextViz just renders an image with textual description of the states and their current values.

Replacing the built is TextViz is simple as calling the environment method `env.set_visualizer(viz)` with `viz` as the desired visualization object.
```python
from pyRDDLGym import RDDLEnv
from pyRDDLGym import ExampleManager

EnvInfo = ExampleManager.GetEnvInfo('MarsRover')
myEnv = RDDLEnv.RDDLEnv(domain=EnvInfo.get_domain(), instance=EnvInfo.get_instance(0))

# set up the environment visualizer
myEnv.set_visualizer(EnvInfo.get_visualizer())
```
In order to build custom visualiztions (for new user defined domains), one just need to inherit the class `Visualizer.StateViz.StateViz()` and return in the `visualizer.render()` method a PIL image for the gym to render to the screen. The environment initilization will look something like that:
```
```python
from pyRDDLGym import RDDLEnv
from pyRDDLGym.Visualizer.StateViz import StateViz

class MyDomainViz(StateViz)
# here goes the visualization implementation


myEnv = RDDLEnv.RDDLEnv(domain='myDomain.rddl', instance='myInstance.rddl')

# set up the environment visualizer
myEnv.set_visualizer(MyDomainViz)
```

By default, calling `EnvInfo.get_visualizer()` on a domain without a dedicated visualizer sub-class 
will return a `Visualizer.TextViz.TextVisualizer()` instance, which simply prints a textual representation
of the state. An alternative `ChartVisualizer` is also available to better track the evolution of the fluents over time.
Like the textual visualizer, this viz handles both continuous and discrete fluent variables:
- scatter plots are used for discrete/categorical variables
- line plots are used for continuous variables
- heatmaps are used for boolean variables

It can be instantiated as simply as follows:

```python
from pyRDDLGym import RDDLEnv
from pyRDDLGym.Visualizer.ChartViz import ChartVisualizer

myEnv = RDDLEnv.RDDLEnv(domain='myDomain.rddl', instance='myInstance.rddl')

# set up the graphical visualizer
myEnv.set_visualizer(ChartVisualizer)
```

and when running on the wildfire domain, produces the following:

![](images/wildfire_graph.gif "Wildfire Graphical Visualization")

### Custom user defined domains

Writing new user defined domains is as easy as writing a few lines of text in a mathematical fashion!
All is required is to specify the lifted constants, variables (all are refered as fluents in RDDL), behavior/dynamic of the problem and generating an instance with the actual objects and initial state in RDDL - and pyRDDLGym will do the rest.\
For more information about how to create new domains in RDDL please see the *RDDL tutorial* at the top of this page.

<hr>
[Back to main page](index.md)
