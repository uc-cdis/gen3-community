# August 27, 2025 | Gen3 CSOC Working Group

Attendees: CTDS: Michael, Sara, Jawad, Clint, Peter, Elise, Ed, Bob, Abhijith; Aus BioCommons: Guerdon Mukama, Nagasri Alava; Univ Auckland; IU: Alan Walsh; D4CG: Luca Graglia, Bektemir Ashirmatov; OHSU: Kyle Ellrott, Liam Beckman; University of Aukland: Matt Pestle, Claire Rye, Rui Chen

## Relevant meeting links   

* [Recording of the mtg (YouTube)](https://youtu.be/LktSl1S0Izo)


## Agenda

* Jawad Qureshi and Abhijith MS, CTDS, University of Chicago, will give an update on the CSOC portal
  * KeyCloak - Authentication and Authorization. How to set up read-only roles, and admin roles.
  * Database integrations
    * Web view of the postgres databases! Now using the csoc portal you can see and query the databases.
    * Interface to query Elasticsearch
  * New environment overview dashboard
    * Get the health of your environment at a glance.
  * First helm release with keycloak, csoc, and grafana - so people can start bootstrapping CSOC.

## Mtg Minutes

### Brief updates from other CSOC groups   

* Alan/IU - Met with Luca to get CCDI fed query working. Also IPO DC (re: this grant https://reporter.nih.gov/search/U0dL9krSLEyMBjQCcAcEug/project-details/10879283) is up and we’re loading data.
* Bektemir/G4CG - Setting up Argo CD and helm charts
* Claire & Matt: Working thru helm charts, and we have a PR to contribute to Helm.
* Guerdon/AusBio - Enable user reg thru Auth0 - https://data.test.biocommons.org.au , upgrading K8S clusters.
* Kyle/OHSU - Brian Walsh has submitted a starter PR to add dynamic bucket control for Fence (https://github.com/uc-cdis/fence/pull/1292). Use case where users are providing buckets of their own. (Self managed model where users can provide the repository where the files are.) Similar to the Indexd PR for RBAC model.




### Update from CTDS on CSOC development

* https://github.com/uc-cdis/gen3-admin/
* Overview:
  * Helm charts and KeyCloak authentication working with the CSOC portal (but only CSOC portal - note that KeyCloak is not generally working with Gen3 as a whole)
* KeyCloak (KC)- Authentication and Authorization. How to set up read-only roles, and admin roles.
  * KC is flexible for setting up users, roles, and even groups. (note that groups needs to be configured carefully to ensure it gets into the token properly)
    * In older versions of KC, used to be production groups, newer version is Realm Roles (that’s what gets mapped). Need to be sure you’re using Realm Roles moving forward
* New environment overview dashboard
  * Get the health of your environment at a glance.
  * There’s an environment overview that helps you to visualize or see every aspect of the cluster from a single point of view, and lets you view all the jobs you have on a cluster and trigger them
  * Another component shows all the pods that you have running on that cluster, with their status and important metrics, like CPU usage and memory requested
  * Another component shows the CPU usage for every node and pod within the cluster, so you're able to see which pod is taking up too many or too few resources
  * another component which shows every event that happens across the cluster
  * There's an active alerts component that shows you the most important events
  * Keycloak is deployed in our dev cluster. (ours is also behind our VPN to have an extra barrier)
  * Google integration as well with KeyCloak, so KeyCloak is acting as an Identity provider
  * In our Gen 3 admin repository, added a script to deploy the KC Helm charts with some default values.
  * Then, you can create a realm, which is just a sort of environment that you're managing. And you can have different identity providers for that realm.
  * 3 types of role
    * Read - only GET requests
    * Write - also POST requests
    * Superadmin -
    * Access token has the info about your group membership
    * KC doesn’t do granular authz as well as arborist (we have to manually code authz stuff into CSOC portal). KC does act as ID broker really well, also does SSO stuff well.
* Database integrations
  * Web view of the postgres databases - Now, using the csoc portal, you can see and query the databases.
    * Dashboard gives list of DB you have available. Then you can start a session against the DB. You can see all the cols available in the DB, what connxns are open, can craft queries against DB
  * Interface to query Elasticsearch
    * We looked into PG web for ES, but it was bulky or very config-needy. Instead, added most of the default endpoints that you would query your Elasticsearch cluster with
    * Editor in here is the same as in VS Code, so that’s convenient to have a familiar interface
* First helm release with keycloak, csoc, and grafana - so people can start bootstrapping CSOC.
  * We have grafana stack that can have this integrated
  * KC helm chart
  * CSOC portal helm chart (WIP)
  * Still needs comprehensive security review
  * Next step - integrate with Terraform.
  * Request to Alan - if your Kro stuff is moving along well, maybe we can start to check how it can be used to bootstrap the CSOC itself
  * Gen 3 deployment wizard being polished by Elise
  * Updates on the agents that we deploy:
    * if you're deploying to an EKS cluster, you can set up a cloud identity for that agent that you deployed to
    * so if you deploy it to, for example, one of our production clusters, we would definitely be relying on a role
    * but if you're deploying on-prem, you can still have some level of AWS identity in this agent to be able to do AWS stuff down the line.
    * Because we are going to add stuff where you can manipulate buckets, or spin up different things in the different AWS accounts.
  * there's going to be some cost overview added into this dashboard
  * Adding Shell capability into pods and other things that you can shell into (complex engineering!)
    * Being able to have terminal access to any part of your cluster
    * Previously it used to show the overview, the YAML associated with the pod
    * We added a shell which allows you to have terminal access, basically.
    * The whole process starts with the front-end initiating a HTTP request.
    * Which goes to the Golang server. The Golang server upgrades this HTTP request to a WebSocket request.
    * And sends it to the agent in the cluster. The cluster then creates a Kubernetes client and uses that client to exec into the pod. Which underneath uses the SPDY protocol.
    * Then we're using a library in the front end, called Extern, to be able to do this functionality.
* Questions:
  * Q: Is there a convenient kind of integration between the Gen 3 admin and the Argo CD? Answer: Yes, all of these environments are deployed with Argo CD and there is an integration with Argo CD.
    * And actually, Argo API’s bring back so much info that we’re not using yet. I'm hoping at some point that we can create some sort of a visual map/dashboard that shows you all of these resources and their states. If anyone here wants to join and try to brush off their React skills. If you're interested, just reach out
  * Q: Are we ready for people to be early-adopters? A: Yes, we’re about to merge it to master.
* Topics for next mtg
  * Request from Alan - Maybe a discussion about observability (what CTDS has done and made available, vs AusBiocommons, for eg, doing something different)
  * Claire and Guerdon may also be able to share how they do observability
  * Jawad: We can also talk about the components that we use in AWS that are relatively cheap to run, that enhances not just the observability, but security, such as WAF


## Next Steps

**Action items**

* Set up tech call with Kyle/OHSU and some of our Fence team (and Pieter and Jawad) to coordinate development of bring your own bucket feature

## About the Gen3 Community CSOC working group

The CSOC working group will focus on supporting the needs of organizations that run multiple Gen3 systems.

A commons services operations center (CSOC) is used by organizations that run more than one Gen3 system and allows a team of engineering and security staff to set up, configure, secure, operate, and monitor two or more data commons or data meshes. Part of the working group focus will be on the development of dashboards and tools that will enable an administrator to configure, launch, and monitor a data commons or mesh. We will also discuss and work on other improvements and topics of interest to multi-Gen3 organizations.

Projects completed by the working group will be merged into the Gen3 source code and made available to the community. As the Gen3 maintainer, CTDS will manage the working group, contribute code, and provide guidance to others on contributing to the Gen3 source code. Other participants will help provide requirements and also contribute code to Gen3.

### Useful Links

* Agendas and minutes can be found in the [Gen3 Community GitHub Repo CSOC Working Group folder](/CSOC_Working_Group_items).   
* Slack channel: [\#gen3\_working\_group\_csoc\_ext](https://gen3friends.slack.com/archives/C082FLTBYMA) - email Gen3 support to request to be added to the channel ([support@gen3.org](mailto:support@gen3.org))
