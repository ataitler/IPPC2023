<p style="font-size:30px;text-align:center"><b>RDDL and the pyRDDLGym Infrastructure</b></p>

The problems in this year's competition will be described in the RDDL language.
RDDL is intended to compactly support the representation of a wide range of relational MDPs and POMDPs and support the efficient simulation of these domains. The domains will be simulated via autogenerating environment simulator and interacted via the standard [Gym](https://www.gymlibrary.dev/) interface. Simply put, the pyRDDLSim takes textual problem description in RDDL, and generates a gym environment without writing a single line of python code.


# Getting started with RDDL
[RDDL language guide](http://users.cecs.anu.edu.au/~ssanner/IPPC_2011/RDDL.pdf)

Please cite as

```
@unpublished{Sanner:RDDL,
      author = "Scott Sanner",
      title = "Relational Dynamic Influence Diagram Language (RDDL): Language Description",
      note = "http://users.cecs.anu.edu.au/~ssanner/IPPC_2011/RDDL.pdf",
      year = 2010}
```

[RDDL tutorial](https://sites.google.com/site/rddltutorial/)

# pyRDDLSim
## Getting started
The pyRDDLGym infrastructure is available for cloning: `https://github.com/ataitler/pyRDDLGym.git`

Read the [Readme page](https://github.com/ataitler/pyRDDLGym/README) for information on the framework contents, requirements, examples, and more.

## Basic usage

### Initializing Environments
Initializing environments is very easy in pyRDDLGym and can be done via: 
```python
from Env import RDDLEnv as RDDLEnv
myEnv = RDDLEnv.RDDLEnv(domain="domain.rddl", instance='instance.rddl')
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
This example will run the instance `instance.rddl` of the problem specified in the file `domain.rddl`.
The loop will run for the amount of time steps specified in the environment's `horizon` field. If the env.render() function will be used we will also see a window pop up rendering the environment
```python
from Env import RDDLEnv as RDDLEnv
from Policies.Agents import RandomAgent

myEnv = RDDLEnv.RDDLEnv(domain='domain.rddl', instance='instance.rddl')
agent = RandomAgent(action_space=myEnv.action_space, num_actions=myEnv.NumConcurrentActions)

total_reward = 0
state = myEnv.reset()
for _ in range(myEnv.horizon):
      next_state, reward, done, info = myEnv.step(agent.sample_action())
      total_reward += reward
myEnv.close()
```

### Spaces

### Domains
