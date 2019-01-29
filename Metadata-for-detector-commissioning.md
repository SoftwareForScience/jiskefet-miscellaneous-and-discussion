# Metadata for detector commissioning

| Version | Date | Comment |
|-|-|-|
| 1 | 2018-06-18 | Initial version. Contains bare minimum for first usable release of an O2 bookkeeping system. |
| 2 | 2018-06-22 | Add clarification on amount of entries per run. Add info about EPNs being able to leave/join run dynamically. |


# Introduction

This document describes the metadata needed for detector commissioning.
It does not try to say how this metadata will be implemented in a database schema.

# Run general info
- This section lists the information which is stored at the run level, i.e., one global value per run.  
- Some of the data might be derived from other lower-level data (example: “Data volume readout” is the sum of the “Data volume readout” of all the individual Readout processes running in each FLP). 
- Data insertion might be split in different calls. 

Missing: 

- tags

| **Field**                     | **Description**  | **Example**               |
| ----------------------------- | ---------------- | ------------------------- |
| Run number                    | Integer ID of a specific data taking session. Should be positive and strictly increasing.| 23  |
| O2 Start time                 | Time when command to start a new Run was given. | |
| TRG Start time                | Time when Trigger subsystem was started. | |
| TRG End Time                  | Time when Trigger subsystem was stopped. | |
| O2 End time                   | Time when Run was completely stopped. | |
| Activity ID                   | Control ID string. Can be a long hash, 32 or 64 character long. | |
| Run Type                      | Type of run. Might be replaced by tags. | PHYSICS, COSMICS, TECHNICAL |
| Run Quality                   | Overall quality of the data from O2 point of view. | Good, Bad, Unknown |
| # of detectors                | Number of detectors in the Run. | |
| # of FLPs                     | Number of FLP nodes in the Run. | 250 |
| # of EPNs                     | Number of EPN nodes in the Run. | 1500 |
| # of timeframes               | Total number of timeframes processed by the system. Can reach 10s or 100s of millions. | 1000 |
| # of subtimeframes            | Total number of subtimeframes processed by the O2 system. Can reach 10s or 100s of millions. Is the sum of the # of subtimeframes of all FLPs in the Run. | 50000  |
| Data volume readout           | Total data volume read out from the detectors by the O2 system in bytes. Can reach PetaBytes. | |
| Data volume timeframe builder | Total data volume assembled in full timeframes by the different timeframe builders running in the EPNs. Can reach PetaBytes. | |

# FLP general info

This section lists the information which is stored at the FLP level, i.e., one value for each FLP role, where each FLP role is related to one run. (note: multiple FLP roles might coexist in the same host).   

| **Field**          | **Description**  | **Example**        |
| ------------------ | ---------------- | ------------------ |
| Name               | FLP name. Inserted once. | FLP-TPC-1 |
| Hostname           | FLP hostname. Inserted once. |someserver.cern.ch |
| # of subtimeframes | Number of subtimeframes processed in this FLP. Updated regularly. | 50 |
| Data volume IN     | data volume read out from the detector by this FLP in bytes. Can reach PetaBytes. Updated regularly. | |
| Data volume OUT    | data volume sent to EPNs by this FLP in bytes. Can reach PetaBytes. Updated regularly. | |

# EPN general info

This section lists the information which is stored at the EPN level, i.e., one value for each EPN role (note: multiple EPN roles might coexist in the same host). EPNs can be added or removed during a run. For example, an EPN could be in the run at the beginning, leave mid-run and later rejoin. 

| **Field**             | **Description**                                                  | **Example**        |
| --------------------- | ---------------------------------------------------------------- | ------------------ |
| Name                  | EPN name                                                         | EPN-1              |
| Hostname              | EPN hostname                                                     | someserver.cern.ch |
| # of timeframes       | Number of timeframes processed in this FLP.                      | 50                 |
| Data volume processed | data volume processed by this EPN in bytes. Can reach PetaBytes. |                    |

# Detector general info

This section lists the information which is stored for each detector, i.e., one value for each detector per run. 

| **Field** | **Description**                      | **Example**              |
| --------- | ------------------------------------ | ------------------------ |
| Name      | detector name                        | ITS                      |
| quality   | quality of the run for this detector | ‘Good’, ‘Bad’, ‘Unknown’ |

# Log Entries general info

This section lists the information which is stored with each log entry. 
Missing: 

- attach log entries to runs
- tags

| **Field**     | **Description** | **Example** |
| ------------- | --------------- | ----------- |
| id            | Log Entry ID    | 123         |
| author ID     | Author ID       |             |
| title         |                 |             |
| body          |                 |             |
| creation time |                 |             |

# Files general info

This section lists the information which is stored for each file. 

| **Field**     | **Description** | **Example**        |
| ------------- | --------------- | ------------------ |
| log entry ID  |                 | 123                |
| file ID       |                 | 1                  |
| title         | Optional        | “calibration plot” |
| filename      |                 |                    |
| size          |                 |                    |
| content type  |                 |                    |
| creation time |                 |                    |


