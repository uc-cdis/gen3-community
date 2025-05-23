# Dec 9, 2024 | [Gen3 CSOC Working Group Kickoff](https://www.google.com/calendar/event?eid=NnQ0Nml2bzdwZnY4Z2NhZWJlbjZyY2J0cG8gc212Z2FyY2lhQHVjaGljYWdvLmVkdQ)

Attendees: Amy Burns (IU), Uwe Winter (Aus BioCommons),  Alan Walsh (IU),  Peter Vassilatos (CTDS), Sara Volk de Garcia (CTDS), Clair Rye (NeSI),  Jawad Qureshi (CTDS),  Plamen Martinov (OCC) Michael Fitzsimons (CTDS), Ruslan Forostianov (SC4Bio), Colin Griffin (KrumWare), Clint Malson (CTDS), Kyle Ellrott (OHSU), Brian Furner (D4CG), Luca Graglia (D4CG), Guerdon Mukama (Aus BioCommons), Hunter Adams (KrumWare)

## Relevant meeting links   

* Agenda: [https://github.com/uc-cdis/gen3-community/blob/master/CSOC_Working_Group_items/README.md](https://github.com/uc-cdis/gen3-community/blob/master/CSOC_Working_Group_items/README.md)  
* Slides: [https://github.com/uc-cdis/gen3-community/blob/master/CSOC_Working_Group_items/20241209-CSOC_WG_slides.pdf](https://github.com/uc-cdis/gen3-community/blob/master/CSOC_Working_Group_items/20241209-CSOC_WG_slides.pdf)
* Recording of the mtg: [on YouTube](https://www.youtube.com/watch?v=Rd4qjhm3oKI)

## Mtg Minutes

* Introductions by all participants (give name, organization, and some details about your Gen3 installation if you have one)  
  * **Indiana Univ:** Alan Walsh and Amy Burns \- ARDaC [https://portal.ardac.org/login](https://portal.ardac.org/login), developing Indiana Precision Oncology (IPO), [Center for Cannabis, Cannabinoids, and Addiction (C3A)](https://c3a.indiana.edu/), also helping Univ FL to bring up a Gen3 commons.   
  *  **UChicago, Data for the Common Good** \- Brian Furner, Luca Graglia, Pediatric Cancer Data Commons, planning for deployment of extra Gen3 instances for other groups, so starting to think about best practices for CSOC, use the same framework as AnVIL and others  
  * **NeSI (New Zealand eScience Infrastructure)** \- Claire Rye, they have 1 DC and maybe another prototype, they often work closely with Univ Auckland. Interested in best practices for expanding to multiple systems.   
  * **KrumWare** \- Colin Griffin \- not a research group, but instead a SE and PE dev group that got into Gen3 to help a project at Wake Forest Univ  
  * **Aus BioCommons** \- Guerdon Mukama and Uwe Winter. 2 Gen3: ACDC. operated for a collective of CVD researchers. Multiomic. OMIX3 \- multiomics platform. Maybe a 3rd coming. Recently made deployment code public, run on AWS. Working to be best positioned to run multiple commons  
  * **Oregon H\&S Univ** \- Kyle Ellrott, Alliance for Cancer Early Detection. Public Facing (AWS) and internal facing (openstack). Managing multiple S3 envts  
  * **Open Commons Consortium** \- Plamen Martinov \- Run 6 data commons with 2.5 petabytes of data. BloodPAC, Prometheus Data Platform, others. In AWS, working on bringing to GCP and Azure  
  * **SC4Bio** \- Ruslan Forostianov. SE who build software, from Europe. There’s interest there to use Gen3, so they’re looking to gather info about it.   
  * **CTDS folks:** Michael Fitzsimons Dir of Research Programs, Jawad Qureshi, Lead Platform Engineer; Sara Volk de Garcia \- User Services; Clint Malson, Director of Security/CISO;  Peter Vassilatos, Director of Engineering   

* Mission of group  
  * How can we make it simpler for users to spin up 1 or more Gen3 instances  
  * CSOC also sets up req’s infrastructure for people who want to use Gen3 but don’t have the background for quickly deploying all the infrastructure  
  * Also \- setting up multiple data commons or meshes  
  
* Purpose: centralized management platform to host the backend of Gen3 to empower orgs to use all of gen3’s potential but securely and efficiently .   
  * Tie into different open source tools  
  * Do this collaboratively, with the community who face actual real-life problems  
  * We have a POC that could resemble this. Core platform under dev with:  
    * Fully featured K8s dashboard, so vis without having to use k8s tools  
    * Our ultimate goal with Gen 3 as things have evolved for us over the years is to help operationalize and enable researchers and the institutions to do more with their cloud environments. And follow best practices and standards to secure and develop those cloud environments where an application like Gen 3 may be deployed and the rest of the lifecycle and everything else that needs to go along with that.  
    * Helm  
    * Working on “deployment wizard”   
    * Building in authn/z to integrate with diff providers (eg keycloak)  
    * Monitoring and observability: used to be DataDog, now building on open source components like Grafana  
    * Setting up cloud integration \- provisioning and mgmt of all the infra in the cloud. Open to hearing other’s experiences to inform our dev  
    * Ability to share cloud spending across AWS accounts  
    * Other features: role based access control (RBAC), securing the backend (right now, IP restriction, but open eyed to new ideas)   
    * Try to provide CSOC as part of SaaS and PaaS – with the goal of empowering project teams from individual CSOCs (set up a capability so anyone can run their own CSOC, cloud-agnostically)  
    * Jawad Demo: Feedback:   
      * Plamen: re: cloud-automation  
      * Plamen: what’s on top of all the (many) grafana logs that provides intuitive info for further analysis \- any analytical tools doing the interpretation and prioritization? Answer: we are leveraging grafanas’s dashboard abilities to present the info in a sensible, digestible way. And to follow up as a question for this group: is this direction helpful for the group? Or will your indiv security orgs require you to do things independently  

* Discuss how to work together on a CSOC dashboard and other goals  
* Open discussion

**Next steps:**  
Michael will send out invite for the regular monthly meeting time.   
Uwe will present on their solution Gen3 deployment and infrastructure management

**Action items**

- [ ] Everyone: Watch for email to schedule regular working group meetings  
- [ ] Michael \- send out poll for monthly meeting slot

## About the Gen3 Community CSOC working group

The CSOC working group will focus on supporting the needs of organizations that run multiple Gen3 systems.

A commons services operations center (CSOC) is used by organizations that run more than one Gen3 system and allows a team of engineering and security staff to set up, configure, secure, operate, and monitor two or more data commons or data meshes. Part of the working group focus will be on the development of dashboards and tools that will enable an administrator to configure, launch, and monitor a data commons or mesh. We will also discuss and work on other improvements and topics of interest to multi-Gen3 organizations.

Projects completed by the working group will be merged into the Gen3 source code and made available to the community. As the Gen3 maintainer, CTDS will manage the working group, contribute code, and provide guidance to others on contributing to the Gen3 source code. Other participants will help provide requirements and also contribute code to Gen3.

### Useful Links

* Agendas and minutes can be found in the [Gen3 Community GitHub Repo](https://github.com/uc-cdis/gen3-community/blob/master/Working%20Groups.md).   
* Slack channel: [\#gen3\_working\_group\_csoc\_ext](https://gen3friends.slack.com/archives/C082FLTBYMA) - email Gen3 support to request to be added to the channel ([support@gen3.org](mailto:support@gen3.org))
