# Requirements for detector commissioning

# Functional requirements
## Log Entries

- create log entries from GUI, process ✓
- attach files to log entries (either at creation time or afterwards) ✓
- connect log entries to 0 to n runs (either at creation time or afterwards) ?
- add tags to log entries (either at creation time or afterwards) (TO BE DISCUSSED FURTHER) Add endpoints for tagsystem
- administer tags (TO BE DISCUSSED FURTHER) UI element.
- display log entries in compact table ✓
- display log entries in full mode ✓
- filter log entries by tag, free text, author, creation time (free text still being researched, author and tag have to be added.)
- order log entries ✓
- reply to log entries (threads) (under development)
- paging sytem ✓

## Runs

- add run info from C++ process, Go process ? ✓
- display run summary in compact table form ✓
- display run detailed info ✓
- add tags to runs (afterwards) (Under development)
- administer tags (TO BE DISCUSSED FURTHER) 
- filter runs by tag, run number, start/stop time, ... (tags has to be added)
- order runs ✓
- paging system ✓
- export to CSV 

## Non-functional requirements

- SSO (Ready but has to switch to CERN SSO) 
- Ansible recipes ✓
- integration with infoLogger (To be discussed)

## Database model
