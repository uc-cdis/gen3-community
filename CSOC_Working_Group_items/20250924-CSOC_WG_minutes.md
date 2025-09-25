# Sep 24, 2025 | Gen3 CSOC Working Group

**Attendees:**  
CTDS: Michael Fitzsimons, Sara Volk de Garcia, Jawad Qureshi, Peter Vassilatos, Bob Grossman;  
Aus BioCommons: Nagasri Alava;   
Univ Auckland, NZ (formerly NeSI): Matt Pestle, Claire Rye, Carvin Chen;  
IU: Alan Walsh;   
D4CG: Bektemir Ashirmatov;   
OHSU: Kyle Ellrott;   
OCC: Stephen Dranger, Danne Elbers, Mikisha Patel.  

## Relevant meeting links   

* [Agenda](README.md#2025-Sep-24)  
* [Recording of the mtg (YouTube)](https://youtu.be/SD-OdsUkaDQ)

## Mtg Minutes

### Brief updates from other CSOC groups   

  * Alan/IU \- Met with Jawad to talk about Kro and how to integrate into Gen3 Admin (will continue discussion in a more public place \- maybe the CSOC slack channel  
  * Bektemir/D4CG \- no updates  
  * Claire & Matt & Carvin/Univ Auck: no updates now  
  * Stephen & Danne/OCC: (see below).   
  * Nagasri/AusBio: Trying to enable the discovery page and FEF  

### Brief update on OCC CSOC \- Stephen Dranger, OCC.  

  * Working with Krumware. They’ve developed a Terraform structure (to create infrastructure). OCC is using it with AWS. Using it with Rancher to keep track and maintain multiple k8s installations, and leverage Gen3 Helm Charts to make sure the clusters have their own Gen3.   
  * Demo \- dev cluster, MC2DP cluster Krumware created. We can see all the workloads involved in gen3 in the cluster.   
  * Right now, some Krumware code is OSS and some is not (because it’s still under development and being tested). The plan is that all of it will be open source  

### Gen3 Observability Overview \- Jawad Qureshi, CTDS.  

  * Not too much new, but review what we’re doing re: obs on our end  
  * We use grafana for obs. Sits in centralized CSOC cluster.   
  * We are building on grafana to build in logs and metric views  
  * We also have open-sourced dashboards, showing \# of downloads and requests on the commons, also logins. You can see all the requests being made and their status codes and who’s making them, and how long it took to get a response.   
  * In the dashboard, different views:  
    * you can see how many pods are in your namespace  
    * Another view \- see if you have any services that are not healthy  
    * Another view \- CPU and memory  
    * Another view: usage graph showing which pods are using how many resources  
  * All build on top of grafana, so gen3 admin queries grafana stack  
  * Currently working on bootstrapping everything \- some easy command to get a version of gen3 admin running locally so you can bootstrap   
  * Requests for info to collect in dashboard:  
    * Logins and downloads  
    * what kind of search terms users are putting in (may be possible with Grafana Faro, or possibly other approaches)  

### Gen3 Observability \- Carvin Chen, University of Auckland

  * 2 prod Gen3: agdr and rakeiora ([data.agdr.org.nz](http://data.agdr.org.nz)  and [browse.rakeiora.ac.nz](http://browse.rakeiora.ac.nz))   
  * AGDR obs uses Grafana OSS stack (a note about OS vs enterprise grafana \- in OS, can’t control data source permission to user but only to roles in OSS; enterprise allows you to assign data source permissions to specific users)  
  * Uses prometheus instead of alloy to send the metrics to mimir  
  * We use infra obs at k8s level most often. Also use alerting and monitoring  
  * Each project has 2 clusters (a qa/dev and prod)  
  * They use Grafana to manage data sources, dashboards, and alerts bc can isolate those resources by different organizations  
  * Then, create and manage our data source   
  * After you have the data sources, you can create and import the dashboard. We have 4 different folders (one for each dashboard), each can get permissions for accessing  
  * For each dashboard, you can also set permissions for roles  
  * (Demo of different dashboard views and logs)  
  * Integrated alerts from gen3 admin with slack to make alerts more visible  
  * Also alerts from gen3 helm charts (eg for jobs)  

### Topics for next mtg  

Discussion to be continued

## Next Steps

**Action items**

- [ ] ####  Carvin will post in Gen3 Friends CSOC slack channel about enabling metrics collection and on authentication problems with gen3 admin

## About the Gen3 Community CSOC working group

The CSOC working group will focus on supporting the needs of organizations that run multiple Gen3 systems.

A commons services operations center (CSOC) is used by organizations that run more than one Gen3 system and allows a team of engineering and security staff to set up, configure, secure, operate, and monitor two or more data commons or data meshes. Part of the working group focus will be on the development of dashboards and tools that will enable an administrator to configure, launch, and monitor a data commons or mesh. We will also discuss and work on other improvements and topics of interest to multi-Gen3 organizations.

Projects completed by the working group will be merged into the Gen3 source code and made available to the community. As the Gen3 maintainer, CTDS will manage the working group, contribute code, and provide guidance to others on contributing to the Gen3 source code. Other participants will help provide requirements and also contribute code to Gen3.

### Useful Links

* Agendas and minutes can be found in the [Gen3 Community GitHub Repo CSOC Working Group folder](/CSOC_Working_Group_items).   
* Slack channel: [\#gen3\_working\_group\_csoc\_ext](https://gen3friends.slack.com/archives/C082FLTBYMA) - email Gen3 support to request to be added to the channel ([support@gen3.org](mailto:support@gen3.org))
