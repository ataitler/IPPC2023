# Competition Instance Generators

Instance generators for all 8 competition domains are released for the benefit of the competitors.
The competition instances (pre-released and unseen) will be generated using theses generators as well.

The generators are included in the distribution of pyRDDLGym under `pyRDDLGym/Examples/InstanceGenerators` and can be accessed directly (via import).
They can also be accessed through the `ExampleManager` interface for pyRDDLGym version 1.0.4 and above.

Once an Example manager object has been instanciated an instance can be generated via the interface:

```python
EnvInfo = ExampleManager.GetEnvInfo(env)
EnvInfo.generate_instance(name, param, path)
```

The `generate_instance` method has the following signature:

```python
string ExampleManager.generate_instance(string name, dict param, string path[optional])
```

- If no path is specified then the instance will be generated in pyRDDLGym the folder of the example.
- The return value is the full path of the new generated example.
- The file name of the generated instance will be instance<name>.rddl, where <name> is the string specified in the name field.
- param is the dictionary of values for the controlled parameters of the domains.

As each domain has different set of parameters we document here the dictionary keys required for each domain
  
## HVAC
  
## MarsRover
  
## Mountain Car
  
## Power Generation

## RaceCar
  
## RecSim
  
## Reservior Control
  
## UAV

