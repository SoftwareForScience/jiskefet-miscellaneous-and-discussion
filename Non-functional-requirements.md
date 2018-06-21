# Non functional requirements


## Availability

Given the criticality of the accounting data, the repositories should run in high availability.
The views don’t stricktly need high availability for as long as failures remain rare and downtime low and as long as it doesn’t impact operations.

## Backup

Backups of the repositories are mandatory. 
CERN facilities such as tape system can be used to store the backups. 
For disaster recovery, a remote copy might make sense. 

## Configuration management

Recipes for O2 adopted configuration management tools (most likely Puppet or Ansible) are mandatory in order to allow deployment and configuration changes without intervention of main developers. 

## Documentation

User documentation is needed for complex actions.
Administrator documentation for system administrators and oncall support crew during operations.
Developers documentation for newcomers, long term maintainability and in case of need for handover. 

## Evolution 

Changes are frequent due to new requirements, changes in workflows and operational optimizations. New developments should be expected during the full lifetime of the software.
The software also needs to be supported until the end of Run 4 (currently 2029).   
SLAs should be agreed between AUAS and ALICE O2.

## Guidelines

Software code should follow O2 guidelines and software processes.
C++ coding guidelines available [here](https://github.com/AliceO2Group/CodingGuidelines). 
Web development guidelines available [here](https://github.com/AliceO2Group/Gui/blob/master/docs/DEV.md). 
More information on build system, cmake etc available [here](https://github.com/AliceO2Group/AliceO2).

## Interoperability

Software needs to integrate with the following systems: 

- Configuration Management
- Monitoring
- Logging
- Build system
- O2 
- Grid operations (Alien, LPM) 
## Licensing 

Software needs to be compatible with O2 project licensing guidelines (GPLv3, copyright owners are all participating institutes). 
License available [here](https://github.com/AliceO2Group/AliceO2/blob/dev/COPYING). 

## Performance

The repository should handle the load from processes running in the O2 farm and jobs running on the grid. Numbers TBD. 
The web server should handle the load from human visitors (should not be very high, numbers TBD) and the load from programmatic access via the REST API. Numbers TBD.
Web GUI response time should follow accepted guidelines, latency TBD.

## Platform compatibility

The software should be compatible with the O2 supported platforms.
Server components will run in the O2 facility at P2, OS will most likely be CentOs 7 or similar Linux distribution. 
Programmatic APIs should run on all target platforms (Linux, Apple).
GUI should run on major browsers (Firefox, Chrome, Safari). Microsoft Edge to be checked.

## Security

Integration with CERN Single Sign On services.
Roles based on CERN e-groups.  

## Serviceability

Support crews should be able to independently diagnosis and either restore the service to nominal conditions or migrate to a new instance. 
Access model to production instances by developers team TBD.

