__This software is ALPHA and lacks documentation.__

# Lens

Lens is a tool for online analytical data processing in medical studies.

This repository contains a top-level documentation of the whole Lens system 
which currently consists of these components:

* [Lens App][1] - the web frontend of the Lens system
* [Lens Warehouse][2] - the data warehouse service which holds the actual data
  to be queried
* [Lens Workbook][3] - the workbook storage service which manages the workbooks
  containing queries of various users
* [Lens Auth][4] - the central OAuth 2.0 authorization service for all Lens 
  backend services
  
In addition to the Lens components, the warehouse and workbook service needs a
Datomic database each.
  
## Deployment
  
Different deployment scenarios are thinkable. Each Lens service follows the
principles of a [12-factor app][5]. Public deployments on [Heroku][6] are evenly
possible as private deployments on a PaaS system like [Deis][7]. Currently a
deployment on Deis is tested.

There are also different ways to deploy the two Datomic databases needed by the
warehouse and the workbook service. The minimal deployment is one 
[Datomic Free Edition][8] installation hosting both databases. In order to
improve fault tolerance, two separate Datomic installations are also possible.
Bigger production deployments may benefit from a [Datomic Pro Edition][9] 
installation. There is a no-cost Starter variant of the Pro Edition available.
Lens is tested with a Datomic Pro Edition installation using Riak and Zookeeper
as storage backend.

### Easy Docker Deployment

This repository contains a [Docker Compose][10] file which allows a single
command deployment assuming a working Docker installation. All you need to do
is cloning this repo and typing

    docker-compose up
    
after the Lens system is started, you can point your browser at 
`http://localhost:8080`. 

The Docker Compose file starts several containers which are all automated Docker
Hub builds of the respective GitHub projects available [here][11]. Please check
the `docker-compose.yml` before bringing it up if you want to be sure that you
don't run unwanted containers in your environment.

Currently the Docker deployment comes with two empty databases which contain
only the initial schema. You can log in the web frontend and create workbooks
but there is no data to be queried. 

There will be deployments with sample data very soon.

[1]: <https://github.com/alexanderkiel/lens-app>
[2]: <https://github.com/alexanderkiel/lens-warehouse>
[3]: <https://github.com/alexanderkiel/lens-workbook>
[4]: <https://github.com/alexanderkiel/lens-auth>
[5]: <http://12factor.net>
[6]: <https://www.heroku.com>
[7]: <http://deis.io>
[8]: <https://my.datomic.com/downloads/free>
[9]: <http://www.datomic.com/get-datomic.html>
[10]: <https://docs.docker.com/compose/>
[11]: <https://hub.docker.com/u/akiel/>
