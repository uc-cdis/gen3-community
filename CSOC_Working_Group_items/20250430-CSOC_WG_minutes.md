# Apr 30, 2025 | Gen3 CSOC Working Group

Attendees: CTDS: Michael Fitzsimons, Sara Volk de Garcia, Jawad Qureshi, Peter Vassilatos, Bob Grossman; Aus BioCommons: Guerdon Mukama; IU: Alan Walsh; D4CG: Luca Graglia, Bektemir Ashirmatov; KrumWare: Colin Griffin  

## Relevant meeting links   

* [Agenda](README.md#2025-april-2930)  
* [Recording of the mtg (YouTube)](https://youtu.be/BqlWFnzCfJ4?si=a3bh5KEqHIZM7Dtf&t=16)

## Mtg Minutes

### Brief updates from other CSOC groups   
  * Guerdon/AusBio \- progressing well with CDK work, code shared with Jawad and it was used in his dashboard  
  * Luca/D4CG \- new team member, Bektemir  
  * Alan/IU \- has a grad student looking at [Kro](https://kro.run/) for a future deployment model. Also testing deployment from scratch using our docs  
  * Colin/Krumware \- leveraging Rancher and IaC and non K8S resources, and multi-account management, good progress for standardized stack for data commons deployment  
  * Bob/CTDS \- promoted the Accelerating Research Using Data Meshes and Data Fabrics (ARDM-25) Workshop [https://ctds.uchicago.edu/ardm25-workshop](https://ctds.uchicago.edu/ardm25-workshop)   
  * Colin \- Request for sharing info about where people are presenting, to increase discussion about Gen3 at the events  

### Updates from CTDS on CSOC development
  * CTDS is moving away from adminvm for all our deployments  
  * First alpha release of CSOC portal coming very soon  
  * No further integrations for CDK since last mtg, but can present current status  
  * Integration of squid proxies \- can swap them, get in them, change the rules (squid is the egress proxy, uses whitelisted domains)  
  * Improved deployment \- tighter integration with AWS \- cert mgr shows certs you added. Can define your host name. And defaults to using the same load balancer  
  * Generates a values yaml for helm  
  * Workspace configuration wizard   
  * User sync config \- where your auth rules live (can define manually or pull from S3 bucket)  
  * Having the ability to view all deployments across all clusters easily  
  * Build with helm and argo-cd  
  * Right now, dashboard is very cluster-specific in its views. Vision is to look across many clusters and let you see the unhealthy areas and quickly interrogate why  
  * PGWeb \- looking to see whether we can integrate with it so we can look into databases  
  * How does it work with a version control system like git (when you create the values yaml)? copy/paste and put into git, or copy/paste the folder and it creates a new environment. The idea is that whatever is generated from the config wizard is deployment ready.   
  * We may be able to make our gitops repo public for people to see what’s in there for how we configured. Also, we are planning to copy some examples to documentation and other public-accessible places  
  * Colin asked about crossplane \-   
  * From Colin: really like Percona Everest for CRD-based and self-hosted databases \-   
  * Cloudnative PG is what Jawad has been using  
  * Have not gotten to build in the ability to deploy custom services through the wizard  
  * Guerdon: status on monitoring and obs? \- there is some integration with grafana and loki. Can get access logs, there are some grafana dashboards that we can use to monitor, too.   
  * Can you integrate the monitoring/obs tools with a status page? Yes, possibly. Guerdon shared the link to their status page (page service by atlassian) [https://biocloud3.statuspage.io/](https://biocloud3.statuspage.io/)   
  * As people develop other integrations with Gen3, we would love to feature them on our blog \- [https://docs.gen3.org/blog/](https://docs.gen3.org/blog/)   

### Topics for next mtg  
  * Would be good to rotate around for presenting at these meetings.   
  * Krumware and OCC perhaps on deck? Up to plamen  
  * Interest in seeing more of the transition away from needing an admin vm.   
  * Perhaps the Jun mtg will be when Jawad can talk about migrating cloud-auto based deployment  

## Next Steps

**Action items**

-

## About the Gen3 Community CSOC working group

The CSOC working group will focus on supporting the needs of organizations that run multiple Gen3 systems.

A commons services operations center (CSOC) is used by organizations that run more than one Gen3 system and allows a team of engineering and security staff to set up, configure, secure, operate, and monitor two or more data commons or data meshes. Part of the working group focus will be on the development of dashboards and tools that will enable an administrator to configure, launch, and monitor a data commons or mesh. We will also discuss and work on other improvements and topics of interest to multi-Gen3 organizations.

Projects completed by the working group will be merged into the Gen3 source code and made available to the community. As the Gen3 maintainer, CTDS will manage the working group, contribute code, and provide guidance to others on contributing to the Gen3 source code. Other participants will help provide requirements and also contribute code to Gen3.

### Useful Links

* Agendas and minutes can be found in the [Gen3 Community GitHub Repo CSOC Working Group folder](/CSOC_Working_Group_items).   
* Slack channel: [\#gen3\_working\_group\_csoc\_ext](https://gen3friends.slack.com/archives/C082FLTBYMA) - email Gen3 support to request to be added to the channel ([support@gen3.org](mailto:support@gen3.org))
