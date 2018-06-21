# Data model overview

# Abstract 

The ALICE O² computing system will consist of roughly 100 thousand processes running on 2000 nodes in two different computing farms executing complex workflows such as data readout, data reduction via cluster finding and fast tracking, detector calibration, global reconstruction and event extraction. Additionally, some of these workflows will be offloaded to the WLCG sites where they will be executed as Grid jobs.
To achieve an efficient, reliable and accountable operational mode, it is essential to have a clear and coherent bookkeeping model that formally defines the relevant logical entities and describes the relationship between them.

# Changelog
| 1 | 2017-10-31 | Initial version |

# Introduction

The main goals of the O2 metadata model are to provide a **formal definition** of the logical entities relevant to O2 and describe the **relationship** between those entities. It covers the workflows and operations of the O2 computing system – both in CR1/CR0 and on the WLCG – and the operations of the ALICE experiment.

It incorporates the data stored and the experience gathered with the ALICE Electronic Logbook [1] [2] (for what concerns online workflows and the ALICE operations) and with Alien [3] [4] (for what concerns offline workflows including reconstruction, data preparation, simulation and analysis).

# Entities 

This chapter provides a formal definition of the main entities that make the O2 metadata model, thus allowing for a common vocabulary to be shared across the O2 project. It is not intended to be an exhaustive list. 

## Workflow entities 

These are entities related with the execution of processes either in the O2 clusters or on the WLCG. The concepts can be considered as somewhat generic and common to any distributed system. Useful mainly for O2 developers and operators.  

**Activity** 
Execution of a set of well-defined tasks in a set of nodes during a finite time period. Multiple Activities can be executed in parallel both in the O2 farm and on the Grid. For the current online environment, it corresponds to a *Run* and is executed in the Counting Rooms at P2. Examples of online Activities types are “Detector Calibration Run”; “Global Run”, “Data migration”. For the current offline environment, it corresponds to a *Processing Chain* as managed by Alien’s Lightweight Production Manager (LPM) [5] and is executed in the WLCG sites. Examples of offline Activities types are “Reconstruction Pass”, “Monte Carlo Production”. 

The rationale behind the concept of Activity is:  

- Scheduling and synchronization of related Tasks 
- Aggregation point for bookkeeping of configurations, selected workflows, global statistics 

**Task** 
Well-defined workflow implemented by one or more O2 processes and executed in one or multiple nodes during a finite time period. Multiple Tasks can be executed either in parallel or sequentially in the context of one Activity and normally have well defined configuration, input and output. Examples of tasks are “Readout of detector X”, “Processing Y of detector X”, “TimeFrame Building”, “Calibration Y of detector X”, “Quality Control X”, “Storage”, “Global Reconstruction”, “Event extraction”, “AOD extraction”.  

The rationale behind the concept of Task is: 

- Identification of O2 workflows 
- Selection of workflows that are executed in the context of an Activity 
- Aggregation point for bookkeeping of configurations, application-specific statistics 

**Role**
Logical container (do not confuse with Linux Containers/Docker) of one or more O2 processes being executed in a single computer node. Multiple roles can coexist in the same computer node. A Role defines *where* an O2 Process is being executed. Examples of Roles are “FLP TPC X”, “FLP TOF Y”, and “EPN Z”. 

The rationale behind the concept of Role is: 

- Naming scheme for resource management (particularly important for specialized computer nodes such as FLPs which are tightly coupled to detector sectors) 

**O2 Process** 
Process being executed in a computer node in the context of a Task. Taking advantage of dynamic (re)configuration, an O2 Process might change configuration and therefore transition between Activities without being restarted (this is an optimization detail, however it is better to make it explicit).  

The rationale behind the concept of Role is:  

- Identification of process executions 
- Aggregation point for bookkeeping of process configuration, performance statistics, logs 
## Dataset entities 

These are entities related with the datasets generated and/or managed by O2. Useful for O2 developers and operators but also for the physics community involved in Analysis. They are executed in as an Activity.   

**Run** 
Synchronous data readout and processing Activity in the O2 farm with a specific and well-defined configuration. It normally ranges from a few minutes to tens of hours. It provides a unique identifier for the data set generated at the end of the synchronous dataflow (might not include Reconstruction for certain Runs such as calibration and/or tests). 

The rationale behind the concept of Run is: 

- Dataset identification and management 
- Aggregation point for bookkeeping of conditions, quality control, statistics 

 
**Reconstruction Pass** 
Asynchronous data processing Activity in the O2 farm or the Grid with a specific and well-defined configuration. It provides a unique identifier for the data set generated at the end of the asynchronous data processing. As today, Multiple Reconstruction Passes can be made for the same Run.  

The rationale behind the concept of Reconstruction Pass is: 

- Dataset identification and management 
- Aggregation point for bookkeeping of conditions, quality control, statistics 

**Simulation**
TBD 

## Operational entities 

These are entities similar to the Workflow entities which are more related with the ALICE operations (Run Coordination, Technical Coordination) but are still relevant for O2.   

**LHC Fill** 
Period of activity in the LHC accelerator. It normally ranges from a few minutes to tens of hours. It is generated and managed by the LHC system. 

The rationale behind the concept of LHC Fill is:  

- Aggregation point for efficiency statistics, LHC conditions. 

**Log Entry** 
Text message that describes a significant intervention or event that happened. Can be generated either by humans (e.g. a shifter enters his/her end-of-shift report) or by computer processes (e.g. a detector logs some abnormal situation automatically) and are normally consumed by humans.  

The rationale behind the concept of LHC Fill is:  

- Permanent logging and reporting of significant operational events 
# Relationship between Entities

This chapter highlights the relationships between the different entities previously described.

## Workflow entities  

In a nutshell, the relationship of Workflow entities is the following: Activities are made of Tasks which are executed by O2 Processes in a set of Roles. Figure 1 tries to capture that hierarchical structure.  

![Figure 1 - Relationship between Activity, Task, Role and O2 Process](https://d2mxuefqeaa7sj.cloudfront.net/s_C94F0E4AFF70163EA70E4C209B4EAFD3666ECBEFFED57EC2C936F05020D4F994_1528375567002_file.png)


Some notes from Figure 1:  

- The same Role can be part of multiple Tasks. For example, Role 1 participates in Tasks 1 and 3. 
- O2 Processes are always executed in a Role. 
## Dataset entities 

Runs identify the data generated at the end of the synchronous data flow. Reconstruction Passes will have as input the data generated in either a Run or a previous Reconstruction Pass. 

| **Input**         |                                                                                                                                      | **Output**        |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------ | ----------------- |
| ALICE             | ![](https://d2mxuefqeaa7sj.cloudfront.net/s_C94F0E4AFF70163EA70E4C209B4EAFD3666ECBEFFED57EC2C936F05020D4F994_1528375567004_file.png) | Run 12345         |
| Run 12345         | ![](https://d2mxuefqeaa7sj.cloudfront.net/s_C94F0E4AFF70163EA70E4C209B4EAFD3666ECBEFFED57EC2C936F05020D4F994_1528375567012_file.png) | Run 12345, Pass A |
| Run 12345         | ![](https://d2mxuefqeaa7sj.cloudfront.net/s_C94F0E4AFF70163EA70E4C209B4EAFD3666ECBEFFED57EC2C936F05020D4F994_1528375567014_file.png) | Run 12345, Pass B |
| Run 12345, Pass B | ![](https://d2mxuefqeaa7sj.cloudfront.net/s_C94F0E4AFF70163EA70E4C209B4EAFD3666ECBEFFED57EC2C936F05020D4F994_1528375567016_file.png) | Run 12345, Pass C |

 Both Runs and Reconstruction Passes are executed by Activities. 

## Operational entities 

Runs can be executed either during an LHC Fill (as for most global physics data taking cases) or in between LHC Fills (for cosmics data taking, calibration and/or tests). An LHC Fill can have many Runs but a Run only belongs to an LHC Fill. Reconstruction Passes are indirectly connected to LHC Fills via the Run.  

Log Entries are generic and can be connected to any of the other entities.  

# References
| [1] Barroso, Vasco et al, "The ALICE Electronic Logbook," in *IEEE-NPSS Real Time Conference*, Lisbon, 2010.                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [2] "ALICE Electronic Logbook," ALICE Collaboration, [Online]. Available: https://cern.ch/alice-logbook. [Accessed 01 November 2017].                              |
| [3] Bagnasco, Stefano et al, "Alien: ALICE environment on the GRID," in *Computing in High Energy Physics (CHEP)*, Victoria, Canada., 2007.                        |
| [4] "Alien - ALICE Environment Grid Framework," ALICE Collaboration, [Online]. Available: http://alien.web.cern.ch. [Accessed 01 November 2017].                   |
| [5] Grigoras, Costin et al, "A tool for optimization of the production and user analysis on the Grid," in *Computing in High Energy Physics (CHEP)*, Taipei, 2010. |


