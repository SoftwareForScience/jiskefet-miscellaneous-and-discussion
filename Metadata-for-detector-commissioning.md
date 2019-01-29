# Metadata for detector commissioning

| Version | Date | Comment |
|-|-|-|
| 1 | 2018-06-18 | Initial version. Contains bare minimum for first usable release of an O2 bookkeeping system. |
| 2 | 2018-06-22 | Add clarification on amount of entries per run. Add info about EPNs being able to leave/join run dynamically. |
| 3 | 2019-06-29 | Update on detector commissioning minimum requirements |


# Introduction

This document describes the metadata needed for detector commissioning.

Concerning the **Update time** of the fields:
- At SOR: synchronously at Start of Run 
- At EOR: synchronously at End of Run 
- During Run: periodically during the run, normally to update/overwrite counters
- After EOR: asynchronously after the run finishes, normally by humans

Concerning the **Update key** of the fields, it indicates which key will be provided to know which database record to update. 

Concerning the **Update mode** of the fields: 
- Insert: direct insert via the API
- Replace: direct insert via the API, new value replaces existing one
- Derived from FLPs: aggregated from fields in the FLPs table(s), normally a SUM of partial counters of each FLP
- Derived from EPNs: aggregated from fields in the EPNs table(s), normally a SUM of partial counters of each EPN

# Run general info (NEEDED FOR v1)
- This section lists the information which is stored at the run level, i.e., one global value per run.  
- Some of the data might be derived from other lower-level data (example: “Data volume readout” is the sum of the “Data volume readout” of all the individual Readout processes running in each FLP). 
- Data insertion might be split in different calls. 

Missing: 

- tags

| **Field**                     | **Description**  | **Example** | **Update time** | **Update Key** | **Update mode** |
| ----------------------------- | ---------------- | ------------|-----------------|----------------|-----------------|
| Run number                    | Integer ID of a specific data taking session. Should be positive and strictly increasing.| 23  | At SOR | | Insert |
| O2 Start time                 | Time when command to start a new Run was given. | | At SOR | Run number | Insert |
| TRG Start time                | Time when Trigger subsystem was started. | | At SOR | Run number | Insert |
| TRG End Time                  | Time when Trigger subsystem was stopped. | | At EOR | Run number | Insert |
| O2 End time                   | Time when Run was completely stopped. | | At EOR | Run number | Insert |
| Activity ID                   | Control ID string. Can be a long hash, 32 or 64 character long. | | At SOR | Run number | Insert |
| Run Type	                    | Type of run. Might be replaced by tags.	| PHYSICS, COSMICS, TECHNICAL | At SOR | Run number | Insert |
| Run Quality                   | Overall quality of the data from O2 point of view. | Good, Bad, Unknown | At EOR | Run number | Insert |
| # of detectors                | Number of detectors in the Run. | | At SOR | Run number | Insert |
| # of FLPs                     | Number of FLP nodes in the Run. | 250 | At SOR | Run number | Insert |
| # of EPNs                     | Number of EPN nodes in the Run. | 1500 | At SOR | Run number | Insert |
| # of timeframes               | Total number of timeframes processed by the system. Can reach 10s or 100s of millions. | 1000 | During Run | Run number | Derived from FLPs |
| # of subtimeframes            | Total number of subtimeframes processed by the O2 system. Can reach 10s or 100s of millions. Is the sum of the # of subtimeframes of all FLPs in the Run. | 50000  | Derived from FLPs |
| Data volume readout           | Total data volume read out from the detectors by the O2 system in bytes. Can reach PetaBytes. | | During Run | Run number | Derived from FLPs |
| Data volume timeframe builder | Total data volume assembled in full timeframes by the different timeframe builders running in the EPNs. Can reach PetaBytes. | | During Run | Run number | Derived from EPNs |

# FLP general info (NEEDED for v1)
This section lists the information which is stored at the FLP level, i.e., one value for each FLP role, where each FLP role is related to one run. (note: multiple FLP roles might coexist in the same host).   

| **Field**          | **Description**  | **Example** | **Update time** | **Update Key** | **Update mode** |
| ------------------ | ---------------- | ----------- |-----------------|----------------|-----------------|
| Name               | FLP name.  | FLP-TPC-1 | At SOR | Run number | Insert | 
| Hostname           | FLP hostname.  | someserver.cern.ch | At SOR | Run number, FLP name | Insert |
| # of subtimeframes | Number of subtimeframes processed in this FLP. Updated regularly. | 50 | During run | Run number, FLP name | Replace |
| Data volume IN     | data volume read out from the detector by this FLP in bytes. Can reach PetaBytes. Updated regularly. | | During run | Run number, FLP name | Replace |
| Data volume OUT    | data volume sent to EPNs by this FLP in bytes. Can reach PetaBytes. Updated regularly. | | During run | Run number, FLP name | Replace |

# EPN general info
This section lists the information which is stored at the EPN level, i.e., one value for each EPN role (note: multiple EPN roles might coexist in the same host). EPNs can be added or removed during a run. For example, an EPN could be in the run at the beginning, leave mid-run and later rejoin. 

| **Field**             | **Description** | **Example**        | **Update time** | **Update Key** | **Update mode** | 
| --------------------- | --------------- | ------------------ |-----------------|----------------|-----------------|
| Name                  | EPN name | EPN-1 | At SOR | Run number | Insert | 
| Hostname              | EPN hostname | someserver.cern.ch | At SOR | Run number, EPN name | Insert | 
| # of timeframes       | Number of timeframes processed in this FLP. | 50 | During run | Run number, EPN name | Replace | 
| Data volume processed | data volume processed by this EPN in bytes. Can reach PetaBytes. | | During run | Run number, EPN name | Replace | 

# Detector general info
This section lists the information which is stored for each detector, i.e., one value for each detector per run. 

| **Field** | **Description**                      | **Example**              | **Update time** | **Update Key** | **Update mode** | 
| --------- | ------------------------------------ | ------------------------ |-----------------|----------------|-----------------| 
| Name      | detector name                        | ITS                      | At SOR          | Run number     | Insert          |
| quality   | quality of the run for this detector | ‘Good’, ‘Bad’, ‘Unknown’ | After run       | Run number, detector | Insert    |

# Log Entries general info (NEEDED for v1)
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

# Files general info (NEEDED for v1)
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


