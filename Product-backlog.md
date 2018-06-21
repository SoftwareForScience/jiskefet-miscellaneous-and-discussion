# Product backlog
**DISCLAIMER: WORK IN PROGRESS**  

## Log Entry 

A *Log Entry* is a text message that describe an intervention or an event that happened. It can be generated either by humans (e.g. a shifter enters his/her end-of-shift report) or by machines (e.g. a detector logs some abnormal situation automatically).  

- As a user, I want to have a smart editor to create my log entries (WYSIWYG or Markup) and be able to use smart text so that messages look nice (e.g. links, code, …) 
- As a user, I want to attach files to log entries so that I can add additional non-textual information 
- As a user, I want to reply to existing log messages so that a conversation stays in a well-defined thread 
- As a user, I want to list log entries in a summary view so that I can get an overview of what happened in a given period. 
- As a user, I want to list log entries in a detailed view so that I can read them one after the other. 
- As a user, I want to search log entries by different criteria (e.g. title, content, author, creation date, …) and have the results listed. 
- As a shifter, I want to have templates that prefill most of my end-of-shift reports from the available metadata so that I don’t need to fill in myself what the system already knows. 
- As run coordinator, I want shifters to use templates so that it is easier and faster to read them. 
- As a subsystem responsible, I want to be notified by email (or other channels) of log entries which are related with my subsystem so that I can better follow-up activities without having to constantly visit the product. 
- As a developer, I want to programmatically fetch log entries that match a given criteria so that I can build custom logic or applications based on existing data. 
- As an administrator, I want to have a dashboard that gives me log-entry related analytics so that I follow the evolution of the repository.  

 

## Run 

A *Run* is a unique ID that identifies a synchronous data processing session in the O2 computing system with a specific and well-defined configuration. It normally ranges from a few minutes to tens of hours. It is generated and managed by the O2 system. 

- As a user, I want to browse through all the available metadata associated with a given run to understand on which conditions the run was made.  
- As a user, I want to list all runs that match a given criteria to create my own run set. 
- As run coordinator, I want to attach tags to runs so that I can then use them while searching. 
- As run coordinator, I want to edit certain specialized fields associated to a run (e.g. EOR Reason) so that I correct wrong information inserted by the O2 software. 
- As run coordinator, I want to specify acquisition targets for certain time periods and check how far we are in achieving them so that I can keep track of progress. 
- As subsystem expert, I want to attach quality flags to runs so that physicists can use them while searching for good data sets for their analysis.  
- As a subsystem expert, I want to store custom fields that are only relevant to my subsystem so that I can correlate them with the rest of the metadata repository (e.g. ‘fetch all runs with configuration X where this happened to my detector’). 
- As a developer, I want to programmatically fetch runs that match a given criteria so that I can build custom logic or applications based on existing data. 

 

## LHC Fill 

An *LHC Fill* is a unique ID that identifies a period of activity in the LHC accelerator. It normally ranges from a few minutes to tens of hours. It is generated and managed by the LHC system and published via DIP protocol.   

- As a user, I want to see in a dashboard the metadata associated with an LHC Fill so that I can have a global image of what happened during that LHC Fill. 
- As a user, I want to receive via email a global summary of each LHC Fill so that I can still follow ALICE operations without visiting the product.  

 

## User Experience  
- As a user, I want to be able to login with my CERN credentials to avoid having to remember a new set of credentials. 
- As a user, I want to be able to customize dashboards so that I only see the fields relevant to me. 
- As a user, I want to be able to save search criteria for later use so that I don’t lose time defining them at each visit. 

