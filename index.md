<p style="font-size:30px;text-align:center;line-height:100%"><b>Welcome to the International Planning Competition 2023: Probabilistic and Reinforcement Learning Track</b></p>


The International Probabilistic Planning Competition is organized in the context of the International Conference on Planning and Scheduling (ICAPS). It empirically evaluates state-of-the-art planning systems on a number of benchmark problems. The goals of the IPC are to promote planning research, highlight challenges in the planning community and provide new and interesting problems as benchmarks for future research.

Since 2004, probabilistic tracks have been part of the IPC under different names (as the International Probabilistic Planning competition or as part of the uncertainty tracks). After 2004, 2006, 2008, 2011, 2014, and 2018, the 7th IPPC will be held in 2023 and conclude together with ICAPS, in July 2023, in Prague (Czech Republic). This time it is organized by Ayal Taitler and Scott Sanner.


## Calls
Please forward the following calls to all interested parties:
- [Call for Participation and Domains](/call_email.md)

<div style="width:100%;text-align:center;">
  <a href="images/IPPC2023_Graphical_Call_V2.jpg">
    <img src="images/IPPC2023_Graphical_Call_V2.jpg" height="246" width="190" />
  </a>
</div>

We invite interested competitors to join the competition discussion:

   [ippc2023-rddl@googlegroups.com](https://groups.google.com/g/ippc2023-rddl)

## Preliminary Schedule


| Event                                         | Date             |
|:----------------------------------------------|:-----------------|
| Infrastructure release with sample domains    | October, 2022    |
| Call for domains and praticipants             | October, 2022    |
| Final domains announcement                    | March 2, 2023    |
| Competitors registration deadline             | March 15, 2023   |
| Planner abstract dubmission                   | May 1, 2023      |
| Contest run                                   | June 5-8, 2023   |
| Results announced                             | July 12, 2023    |



## Setup

This year's competition will be using the generic pyRDDLGym - an autogeneration tool for gym environments from RDDL textual description.

<img src="images/RDDLGym.jpg" alt="RDDLGym diagram">

More information about the infrastructure, how to use it and how to add user defined domains can be found the following short guide

- [Infrastructure guide](/infrastructure.md)

pyRDDLGym also comes with a set of auxiliary utils and baseline methods:

- [Tools and Baselines](/planning.md)


## Domains

There are several original domains at the time of the competition call, but more domains will be added, and we strongly encourage the community to create and contribute used defined domains in you field of expertise, or any problem you think the community should try to solve. The highest quality community contributed domains will be selected to be part of the competition's domains. We are aware that participants that submit a domain that is used have some advantage with respect to performance on that domain. We view this as a good incentive for teams to submit high quality proposals.



<div class="image123" style="center">
  <div style="float:left;margin-right:5px;">
        <a href="wildfire.html">
        <img src="images/wildfire_image.gif" height="190" width="190"  />
        <p style="text-align:center;">Fire Fighting (from tutorial)</p>
        </a>
    </div>
    <div style="float:left;margin-right:5px;">
        <a href="rover.html">
        <img src="images/Rover_image2.gif" height="190" width="190"  />
        <p style="text-align:center;">Mars Rovers Science Mission</p>
        </a>
    </div>
    <div style="float:left;margin-right:5px;">
        <a href="recsim.html">
        <img class="middle-img" src="images/recsys_loop.gif" height="190" width="190" />
        <p style="text-align:center;">Recommendation Systems</p>
        </a>
    </div>
    <div style="float:left;margin-right:5px;">
        <a href="powergen.html">
        <img src="images/power_gen.gif" height="190" width="190" />
        <p style="text-align:center;">Power Unit Commitment</p>
        </a>
    </div>
    <div style="float:left;margin-right:5px;">
        <a href="uav.html">
        <img src="images/drones.gif" height="190" width="190" />
        <p style="text-align:center;">UAV</p>
        </a>
    </div>
    <div style="float:left;margin-right:5px;">
        <a href="elevator.html">
        <img src="images/elevator2.gif" height="190" width="190" />
        <p style="text-align:center;">Elevator Control</p>
        </a>
    </div>
</div>


<br clear="left">

In addition to the original domain, we have recreated some of the classical control domains in RDDL. Illustrating how easy it is to generate domains in pyRDDLSim:

<div class="image123" style="center">
    <div style="float:left;margin-right:5px;">
        <a href="cartpole.html">
        <img src="images/cart_pole.gif" height="190" width="190"  />
        <p style="text-align:center;">Cart Pole</p>
        </a>
    </div>
    <div style="float:left;margin-right:5px;">
        <a href="mountaincar.html">
        <img class="middle-img" src="images/mountain_car.gif" height="190" width="190" />
        <p style="text-align:center;">Mountain Car</p>
        </a>
    </div>
  <div style="float:left;margin-right:5px;">
        <a href="racecar.html">
        <img class="middle-img" src="images/racecar.gif" height="190" width="190" />
        <p style="text-align:center;">Race Car</p>
        </a>
    </div>
</div>

<br clear="left">

Note, that there are additional domains out there from past competitions (IPPC 2011, IPPC 2014), which can be also be used with pyRDDLSim:
- [IPPC 2011 domains](https://github.com/ssanner/rddlsim/tree/master/files/final_comp/rddl): This repository contains 8 domains: Elevators, Cross Traffic (Frogger), Game of Life, Navigation, Reconnaissance, Skill Teaching, SysAdmin, Traffic. 
- [IPPC 2014 domains](https://github.com/ssanner/rddlsim/tree/master/files/final_comp_2014/rddl): This repository contains some of IPPC 2011 domains, with additional 4 new domains: Tamarisk (Invasive Species), Wildfire (Firefighting), Academic Advising, Triangle Tireword.

Past competitions were entirely discrete; the focus of this year’s competition is on continuous and mixed discrete-continuous problems. However, everybody are welcome to take advantage of their existance. All previous competition domains are avilavble through the [rddlrepository](https://github.com/ataitler/rddlrepository) package/git.

<!--Past compeition were entirely discrete and as the focus of this year is continous and mix discrete-continous problems, their domains were not included in the pyRDDLGym repository. However everybody are welcome to take advantage of their existence. Just make sure they do not make use of something outside of pyRDDLGym RDDL subset. In that case the original [Java simulator](https://github.com/ssanner/rddlsim) can be used. -->

## Procedure

All competitors must submit an up to 2 pages abstract, describing their method. The compatitors must also submit the source code of their method to be examined (and may be run) by the organizers of the competition. An important requirement for IPC 2023 competitors is to give the organizers the right to post their paper and the source code of their learners/planners on the official IPC 2023 web site, and the source code of submitted planners must be released under a license allowing free non-commercial use.

The competition will take place Mon-Thu June 5 - June 8 2023. The competition will be comprised of two phases.
- __Training phase__: During the two months before the competition, the competitors will train and get ready to compete. The RDDL sources for the domains and at least one instance per domains will be available during the whole period. In addition, instance generators will also be released after the registration deadline.
- __Evaluation phase__: during the week starting at June 5th, at the beginning of each day 2 instances will be release for 2 domains per day. The competitors will have 24 hours to fine-tune their method and submit a container before the end of the 24 hours window.

### Domains
The competition will include:
- 8 domains (two will be release each day)
- 5 instances per domain

| Domain                | pyRDDLGym name         |
|:----------------------|:-----------------------|
| Race Car              |  RaceCar               |
| Reservoir Control     |  Reservoir continuous  |
| Recommender Systems   |  RecSim                |
| HVAC                  |  HVAC                  |
| UAV                   |  UAV continuous        |
| Power Generation      |  PowerGen continuous   |
| Mountain Car          |  MountainCar           |
| Mars Rover            |  MarsRover             |



### Evaluation and Score
The methods will be evaluated on all the competition domains and instances. Expect evaluation submission with 24 hours, on their own hardware with self-reported specs. All methods will be evaluated on an 8 CPU computer with 32 GB of memory. Each instance will be evaluated for 50 trails and the average will be taken. Typical horizon will be around 100 steps.

All results will be normalized according to
- 0: max(noop, random).
- 1: baseline such as Jaxplanner or best competing method to ensure values [0,1].

 
<!--- ### Procedure
The competition will be comprised of two phases.
- Training phase: a week before the competition day, 3 evaluation instances of each domain will be released. For competitors to train/evaluate their methods on.
- Evaluation phase: at the end of the week, each competitor will have a designated time and IP for a cloud resource. The competitors will connect, set up their solutions (the time for that will be taken into consideration), and execute their solutions 10 times for each instance. The average reward over these 10 runs will be the score for the instance. During evaluation, an additional 2 never seen before instances will be evaluated (in addition to the 3 already-released instances). I.e., 5 instances for each domain, 10 runs per instance.


### Score
For each instance, the total reward will be normalized to the range [0,1], and the winner is the competitor who achieves the highest total score.
(The minimum score for the competition will be 0 and the maximum will be 40)
The fine details are subject to discussion in the google-group and will be finalized by the end of January.
--->
<!-- but the general lines will follow the evaluation of the past [IPPC 2011](http://users.cecs.anu.edu.au/~ssanner/IPPC_2011/index.html) competition. 

Domains (note numbers might change this year)
- 8 domains
- 10 instances per domain
- 30 trials per instance

Procedure
- We will use a cloud computing resources, where every team will gain access to an identical computer. The exact configuration will be published enough time before the competition, and an early access will be possible in order to test the code and know what to expect.
- At competition time
    - You will receive instructions on how to login to your own personal Linux node.
    - The location of all RDDL domains / instances.
    - Your agent will have 24 hours to complete trials for all instances.
        - Instances will have a suffix "_1" up to "_10" where 1 will be the smallest (usually easiest) and 10 the largest (usually hardest).
        - You need not compete on all instances or for all trials, in that case the best average score from the random and NOOP policies is assigned (see below).
- Post-competition evaluation
    - We will shutdown the server at the 24 hour time limit.
    - The server maintains a log file for all instances and trials you complete.
    - If you execute more than 30 trials per instance, we will only use data for the last 30 trials.
    - Overall planner evaluation criterion for ranking.
        - For each instance trial, the server records a raw score.
            - For the final competition (boolean MDP and POMDP tracks), a fixed horizon of 40 will be used for all instances.
    - We will compute a [0,1] normalized average score per instance from raw score.
        - Per instance, averaged over all 30 trials, we will determine.
            - The minimum average score (minS_{instance}) is the max over the average scores from a purely random policy and an always-noop policy.
            - The maximum average score (maxS_{instance}) is the max over all competitors, a purely random policy, and a pure noop policy.
            - If a planner does not compete a trial for an instance, minS_{instance} is assigned as the raw score for that missing trial.
            - We will make available all raw and normalized data as well as minS_{instance} and maxS_{instance} used to compute the normalized score for each instance.
        - Normalized-score_{planner,instance} = max(0, [(sum_{trials 1..30} raw-score_{planner,instance,trial})/30 - minS_{instance}] / [(maxS_{instance} - minS_{instance})] ).
        - We use a max here in the unlikely event that a planner does worse than either the noop or random policies to ensure the minimum score is 0... we don't want to penalize a planner that tries and fails vs. a planner that simply skips an instance and gets 0 automatically.
    - Final agent evaluation criterion
        - avg-norm-score_{planner} = (sum_{instance 1..80} normalized-score_{planner,instance}) / 80.
        - Note 1: 80 instances are from 8 domains X 10 instances per domain (instance names uniquely determine the domain).
        - Note 2: given the normalized score per instance, it is to your advantage to complete easier instances before harder ones.
    - Min / max score:
        - The minimum avg-norm-score for any competing planner is 0.
        - The maximum avg-norm-score for any competing planner is 1.
        - Agents will be ranked by their avg-norm-score.

In addition we intend to make the following changes to the 2011 evaluation (subject to community discussions)
1. Per-instance time limits instead of an overall 24 hour time limit.
2. Competitor can do as many simulations as it wants before it initiates the final evaluation of 30 trials.
3. We're considering using strong manual baseline policies for max normalization (hence scores will not necessarily be in [0,1]) <!-- to deal with the issues raised in Jendrik's paper. -->

## Registration
<!--- At this point just join the google group (see link at the bottom) and announce your interest to compete in a post that includes your tentative team name, organization, and team members. --->
Registration for the competition is now open. Please register at the following link:
[Registration form](https://forms.gle/W9ng4v3vciNcc9S27)

The registration will be closed on March 15, 2023. If you missed the deadline and wish to compete please contact one of the organizers (Ayal Taitler or Scott Sanner).




## Organizers
- [Ayal Taitler](https://sites.google.com/view/ataitler/home) (University of Toronto, CA)
- [Scott Sanner](https://www.mie.utoronto.ca/faculty_staff/sanner/) (University of Toronto, CA)

## Contributors
- [Michael Gimelfarb](https://mike-gimelfarb.github.io/) (University of Toronto, CA)
- [Jihwan Jeong](https://jihwan-jeong.netlify.app/) (University of Toronto, CA)
- [Sriram Gopalakrishnan](https://marirsg2.github.io/Sriram_Unravel/) (JP Morgan AI Research, USA)
- [Martin Mladenov](https://ataitler.github.io/IPPC2023/) (Google, BR)
- [Jack Liu](https://ataitler.github.io/IPPC2023/) (University of Toronto, CA)

Contact us: [ippc2023-rddl@googlegroups.com](https://groups.google.com/g/ippc2023-rddl)
