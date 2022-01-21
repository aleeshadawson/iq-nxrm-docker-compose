# Running Sonatype's Nexus Repository Manager and Nexus IQ Server

As a Customer Success Engineer, matching a client's environment will aid in advising how to best approach the problems that they want to solve. In particular, for companies where software upgrades have especially tedious manual approval processes, it is likely that our local versions of Nexus Repository Manager (NXRM) and Nexus IQ Server will not match our clients. In order to match our clients version and architecture locally, we can use containers to mimic thier environment. This project solves that problem. 

## Prerequisites
- Docker version 20.x.x
- Nexus License

Note: that this was written and tested with 20.10.10 on macOS Big Sur version 11.3.1 with an Intel Chip. Other issues may come up and be addressed as others test with their machines. 

## Quick Start
1. Save your license under `./mounted/licenses/` and add it to your `.gitignore`
2. Run `docker-compose up` to start the containers and watch the logs
3. Run:
    1. `docker-compose stop` to stop the containers, or 
    2. `docker-compose down` to stop and delete the containers. 


**Important Note:** All files matching `./mounted/licenses/*.lic` will be ignored from `git`. If you name your license file something else, it will be committed and pushed if you do not add it to your `.gitignore` file. Use care when working with credentials and DO NOT commit or push them to a remote repository.

## The Docker Compose File 

### Services
We currently have the following services defined:
- NXRM
- IQ Server
- PostGres
NXRM is set up to use the external PostGres database currently. IQ Server is set up to use it's embedded database.

### Environment Variables
In our `.env` file we define the following:
`NXRM_VERSION` - version for NXRM
`IQ_SERVER_VERSION` - version for IQ
`POSTGRES_VERSION` - version for PostGres
`POSTGRES_USER` - name of user/database in postgres
`POSTGRES_PASSWORD` - password for user in postgres

<!-- TODO: Make this into a table with the default values and discuss further. -->

### Mounted Volumes
<!-- TODO: I need to explain the mounted volumes better. -->
Note that we mount some files onto the services to be used instead of the ones provided with the container. All of the mounted files found in the `./mounted` directory. The containers have write priveleges to thses files. This is especially important in the case of `./mouted/sonatype-logs` and `./mounted/sonatype-work` because those files are created and written by the service. We do not provide defaults, but rather mount them so we can have data locally accessible. 

### Configuration
This is in progess. We will discuss how to configure environment variables for different situations.
<!-- TODO: Discuss how to configure env variables to use different versions -->
<!-- TODO: Discuss how to configure NXRM to use embedded or external db -->
<!-- TODO: Discuss how to configure IQ server to use embedded or external db -->


<!-- TODO: Add an open source LICENSE to the project. -->