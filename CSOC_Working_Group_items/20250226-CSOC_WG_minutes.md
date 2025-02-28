# Feb 26, 2025 | Gen3 CSOC Working Group

Attendees: CTDS: Michael Fitzsimons, Sara Volk de Garcia, Jawad Qureshi, Bob Grossman, Peter Vassilatos, Clint Malson, Elise Castle, Ed Malinowski;  
Aus BioCommons: Guerdon Mukama; IU: Alan Walsh, Amy Burns; D4CG: Brian Furner, Luca Graglia; OHSU: Kyle Ellrott; NeSI: Claire Rye;  

## Relevant meeting links   

* [Agenda](README.md#2025-february-2627)   
* [Slides](20250226-CSOC_WG_slides.pdf)
* [Recording of the mtg (YouTube)](https://youtu.be/dh7FWSqx-1w)

## Mtg Minutes

* ## Update from CTDS on CSOC deployment

  * Problem statement
    * **Need:** Organizations require the ability to deploy multiple enterprise-grade Gen3 environments on their preferred cloud providers.
    * **Challenge:** Managing Gen3 infrastructure demands specialized cloud-native expertise, creating a barrier for teams without deep cloud knowledge.  CTDS also doesn’t have deep expertise in all clouds.
    * **Impact:**
      * Slower deployment timelines
      * Increased operational complexity & costs
      * Limited scalability across cloud providers
      * Barrier to wide-scale use of Gen3
    * **Solution Opportunity:** A streamlined, scalable approach to Gen3 deployment, reducing technical friction and enabling seamless cloud management that leverages community contributions.
  * CSOC Vision: A Unified Gen3 Management Portal
    * One Portal for End-to-End Gen3 Lifecycle Management
    * Multi-Cloud Infrastructure Provisioning
    * Community-Driven
    * Comprehensive Monitoring & Management
  * Collaboration Opportunities
    * How can we design the CSOC portal to make sure that different orgs can work on it at the same time?
  * IaC as a Plugin
    * containerized plugin system to manage infrastructure deployments
    * May have a different support model – would need to coordinate with contributors
    * Future support for Azure, Google Cloud, Digital Ocean, and other cloud providers
  * System Architecture: see slide 7
    * we need some help getting Azure IaC
    * We need to be able to see what's going on, open telemetry
    * Once we deploy gen3, use a gitops approach
    * Expand helm charts so they can work with the other cloud equivalents of secrets manager
    * Right now, limited support for keycloak, but looking to expand that (esp for collab with React or Go skills)
    * want to be more explicit about how people can contribute
    * Have we considered a more K8S centric approach? (per alan) - once the CSOC is up, can use k8s for everything else. Have we looked at Crow? Also clusterAPI, ACK. The challenge is that we don’t have any templates for that that are production ready yet. We do have prod-ready for terraform and that. But – interesting to explore. How is the infrastructure state managed is an impt question. Also - possible to do both approaches.



* ## Next Steps

*

**Action items**

- Michael will work with Jawad on listing out features that need community participation.  This may be in the form of GitHub issues or something else.  Will try to share before the next meeting.

## About the Gen3 Community CSOC working group

The CSOC working group will focus on supporting the needs of organizations that run multiple Gen3 systems.

A commons services operations center (CSOC) is used by organizations that run more than one Gen3 system and allows a team of engineering and security staff to set up, configure, secure, operate, and monitor two or more data commons or data meshes. Part of the working group focus will be on the development of dashboards and tools that will enable an administrator to configure, launch, and monitor a data commons or mesh. We will also discuss and work on other improvements and topics of interest to multi-Gen3 organizations.

Projects completed by the working group will be merged into the Gen3 source code and made available to the community. As the Gen3 maintainer, CTDS will manage the working group, contribute code, and provide guidance to others on contributing to the Gen3 source code. Other participants will help provide requirements and also contribute code to Gen3.

### Useful Links

* Agendas and minutes can be found in the [Gen3 Community GitHub Repo CSOC Working Group folder](/CSOC_Working_Group_items).   
* Slack channel: [\#gen3\_working\_group\_csoc\_ext](https://gen3friends.slack.com/archives/C082FLTBYMA) - email Gen3 support to request to be added to the channel ([support@gen3.org](mailto:support@gen3.org))
