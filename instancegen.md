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
- he file name of the generated instance will be `instance<name>.rddl`, where `<name>` is the string specified in the name field.
- param is the dictionary of values for the controlled parameters of the domains.

As each domain has different set of parameters we document here the dictionary keys required for each domain
  
## HVAC

A problem with a single zone and a single heater:

```python  
params = {
          'num_heaters': 1,
          'num_zones': 1,
          'density': 1.0,
          'temp-zone-range-init': (0., 15.),
          'temp-heater-range-init': (0., 10.),
          'TEMP-ZONE-MIN': 22.0,
          'TEMP-ZONE-MAX': 25.0,
          'p-switch-number': 0,
          'p-switch-prob': 0.02,
          'horizon': 100,
          'discount': 1.0
}
```

## MarsRover

A problem with a single rover and a single mineral to harvest:

```python
params = {
          'num_minerals': 1,
          'num_rovers': 1,
          'location_bounds': (-10., 10.),
          'area_bounds': (3., 6.),
          'value_bounds': (0., 20.), 
          'horizon': 100,
          'discount': 1.0
}
```


## Mountain Car

A problem with a single valley: 

```python
params = {
          'terrain_xleft': -1.2,
          'terrain_widths': [0.7, 1.1],
          'terrain_heights': [0.9, 0.9], 
          'num_points': 100,
          'pos': -0.6,
          'vel': 0.01,
          'goal-min': 0.5,
          'horizon': 200,
          'discount': 1.0
}
```
  
## Power Generation

A problem with a single generator:

```python
params = {
          'num_gas': 1,
          'num_nuclear': 0,
          'num_solar': 0,
          'demand_scale': 1.0,
          'temp_variance': 5.0,
          'temp_range': (-30.0, 40.0),
          'horizon': 100, 'discount': 1.0
}
```

## RaceCar

A simple problem without obstacles:

```python
params = {
          'num_blocks': 0,
          'min_block_size': 0.0,
          'max_block_size': 0.0,
          'scale': 1.0,
          'goal_radius': 0.06,
          'horizon': 200,
          'discount': 1.0
}
```
  
## RecSim

A problem with providers selling the same commodity:

```python
params = {
        'provider_dispersion': 10.0,
        'provider_fan_out': 1,
        'num_provider_clusters': 1,
        'num_users': 100,
        'docs_per_cluster': 2,
        'user_stddev': 20.0,
        'horizon': 100,
        'discount': 1.0,
}
```
  
## Reservior Control

A problem with a single reservoir to be controlled:

```python
params ={
          'num_reservoirs': 1,
          'max_edges': 1,
          'top_range': (100., 200.),
          'target_range': (0.4, 0.7),
          'rain_var': 5.,
          'horizon': 100,
          'discount': 1.
}
```

## UAV

A problem with a single controllable UAV:

```python
params = {
          'num_aircraft': 1,
          'num_control': 1,
          'variance': 1.0,
          'xrange': (-50., 50.),
          'yrange': (-50., 50.),
          'zrange': (0., 100.),
          'horizon': 100,
          'discount': 1.0
}
```
