# Logbook fields in current system

## General notes
- Mixed naming scheme (camel case and snake case). Should be unified.
- bold is bare minimum  
## Log Entries
| ## Field                   | ## Notes                                                                                     |
| -------------------------- | -------------------------------------------------------------------------------------------- |
| ## **id**                  |                                                                                              |
| ## **run**                 | currently only 1 run. allow multiple runs.                                                   |
| ## **userid**              | rename to authorId ?                                                                         |
| ## **title**               |                                                                                              |
| ## **comment**             | rename to body ?                                                                             |
| class                      | HUMAN or PROCESS. Replace by tags ?                                                          |
| ~~type~~                   | Never fully used. Some overlap with subsystems. Replace by tags ?                            |
| ## **time_created**        | Rename to timeCreated ?                                                                      |
| ~~deleted~~                | REMOVE                                                                                       |
| parent                     | Used to create threads. Replace by something better ?                                        |
| root_parent                | Used to create threads. Replace by something better ?                                        |
| ~~dashboard~~              | REMOVE                                                                                       |
| ~~time_validity~~          | REMOVE                                                                                       |
| processedEmailNotification | Used to flag as processed for purposes of email notification.  Replace by something better ? |
| ~~context~~                | Replace by tags ?                                                                            |

## Files
| ## Field            | ## Notes                |
| ------------------- | ----------------------- |
| ## **commentid**    | Rename to logEntryId ?  |
| ## **fileid**       | Rename to fileId ?      |
| ## **title**        | Can be optional         |
| ## **filename**     |                         |
| ## **size**         |                         |
| ## **content_type** | Rename to contentType   |
| ## **time_created** | Rename to timeCreated ? |
| ~~deleted~~         | REMOVE                  |

## Runs 
| ## Field                               | ## Notes                                              |
| -------------------------------------- | ----------------------------------------------------- |
| ## **run**                             |                                                       |
| ## **time_created**                    | Rename to o2TimeStart ?                               |
| ~~DAQ_time_start~~                     | REMOVE                                                |
| ~~DAQ_time_end~~                       | REMOVE                                                |
| ## **TRGTimeStart**                    | Rename to dataTimeStart ?                             |
| ## **TRGTimeEnd**                      | Rename to dataTimeEnd ?                               |
| ## **time_completed**                  | Rename to o2TimeEnd ?                                 |
| time_update                            | Unclear, not really useful so far                     |
| runDuration                            | Derived from start/stop times. Still needed ?         |
| pauseDuration                          | Derived from individual pause periods. Still needed ? |
| ## **partition**                       | Rename to activityId ?                                |
| ~~detector~~                           | REMOVE                                                |
| ## **run_type**                        | Rename to runType. Replace by tags ?                  |
| ~~calibration~~                        | Replace by tags ?                                     |
| ~~ecs_success~~                        | REMOVE                                                |
| ~~daq_success~~                        | REMOVE                                                |
| ~~eor_reason~~                         | REMOVE                                                |
| beamEnergy                             | Rename to lhcBeamEnergy ?                             |
| beamType                               | Rename to lhcBeamType ?                               |
| LHCBeamMode                            | LHC lowercase  (lhc)                                  |
| LHCFillNumber                          | LHC lowercase (lhc)                                   |
| LHCTotalInteractingBunches             | LHC lowercase  (lhc)                                  |
| LHCTotalNonInteractingBunchesBeam1     | LHC lowercase  (lhc)                                  |
| LHCTotalNonInteractingBunchesBeam2     | LHC lowercase  (lhc)                                  |
| LHCBetaStar                            | LHC lowercase  (lhc)                                  |
| LHCFillingSchemeName                   | LHC lowercase  (lhc)                                  |
| LHCInstIntensityNonInteractingBeam1SOR | Unclear                                               |
| LHCInstIntensityNonInteractingBeam1EOR | Unclear                                               |
| LHCInstIntensityNonInteractingBeam1Avg | Unclear                                               |
| LHCInstIntensityInteractingBeam1SOR    | Unclear                                               |
| LHCInstIntensityInteractingBeam1EOR    | Unclear                                               |
| LHCInstIntensityInteractingBeam1Avg    | Unclear                                               |
| LHCInstIntensityNonInteractingBeam2SOR | Unclear                                               |
| LHCInstIntensityNonInteractingBeam2EOR | Unclear                                               |
| LHCInstIntensityNonInteractingBeam2Avg | Unclear                                               |
| LHCInstIntensityInteractingBeam2SOR    | Unclear                                               |
| LHCInstIntensityInteractingBeam2EOR    | Unclear                                               |
| LHCInstIntensityInteractingBeam2Avg    | Unclear                                               |
| LHCInfoStatus                          | Unclear                                               |
| forceLHCReco                           | Unclear                                               |
| ## **numberOfDetectors**               |                                                       |
| detectorMask                           | Unclear. Do we need to do bitwise operations ?        |
| ~~splitterDetectorMask~~               | REMOVE                                                |
| totalSubEvents                         | rename to totalSubtimeframes                          |
| ## **totalDataReadout**                |                                                       |
| ## **totalEvents**                     | rename to totalTimeframes                             |
| totalEventsPhysics                     | Unclear                                               |
| totalEventsCalibration                 | Unclear                                               |
| totalEventsIncomplete                  | Unclear                                               |
| ## **totalDataEventBuilder**           | rename to totalDataTimeframeBuilder                   |
| ## **totalDataRecorded**               |                                                       |
| averageSubEventsPerSecond              | Unclear                                               |
| averageEventsPerSecond                 | Unclear                                               |
| averageDataRateReadout                 | Unclear                                               |
| averageDataRateEventBuilder            | Unclear                                               |
| averageDataRateRecorded                | Unclear                                               |
| LDClocalRecording                      | Unclear                                               |
| GDClocalRecording                      | Unclear                                               |
| GDCmStreamRecording                    | Unclear                                               |
| eventBuilding                          | Unclear                                               |
| LHCperiod                              | Rename to lhcPeriod                                   |
| ~~HLTmode~~                            | REMOVE                                                |
| dataMigrated                           | Unclear                                               |
| ## **runQuality**                      |                                                       |
| L3_magnetCurrent                       | Unclear                                               |
| Dipole_magnetCurrent                   | Unclear                                               |
| ~~L2a~~                                | REMOVE                                                |
| ~~ctpDuration~~                        | REMOVE                                                |
| ~~ecs_iteration_current~~              | REMOVE                                                |
| totalNumberOfFilesWriting              | Unclear                                               |
| totalNumberOfFilesWaitingMigration     | Unclear                                               |
| totalNumberOfFilesMigrationRequested   | Unclear                                               |
| totalNumberOfFilesMigrating            | Unclear                                               |
| totalNumberOfFilesMigrated             | Unclear                                               |
| numberOfPar                            |                                                       |
| numberOfFailedPar                      |                                                       |



