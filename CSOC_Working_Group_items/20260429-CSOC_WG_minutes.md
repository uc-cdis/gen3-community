# March 25, 2026 | Gen3 CSOC Working Group

**Attendees:**  
* CTDS: Michael Fitzsimons, Jawad Qureshi, Sai, Bob;  
* Aus BioCommons: Nagasri Alava, Guerdon Mukama;
* Univ Auckland, NZ: Carvin Chen, Matt Pestle;
* D4CG: Bektemir Ashirmatov, Luca;   
* OCC: Stephen Dranger

## Relevant meeting links   

* [Recording of the mtg (YouTube)](https://youtu.be/1_ygikuNerI)

## Agenda

* Hands on CSOC deployment demo led by Jawad

## Mtg Minutes

### Brief updates from other CSOC groups   

* Alan/IU - nothing urgent
* Bektemir & Luca/D4CG - nothing urgent
* Matt & Carven/Univ Auck: scanning Gen3 for vulnerabilities, found some critical CVEs, compliance report , Carvin will send for us to help review
* Nagasri & Guerdon/AusBio:  launched a new Gen3 biological psychiatry environment
* Stephan/OCC - Stephen - focusing on other topics right now.  Australian sent them the REMS code to review


### CSOC Demo

* Started workshop by Jawad.
* First navigate from here: https://github.com/uc-cdis/gen3-admin/tree/master
* Clone this and then execute: ./scripts/setup-minikube.sh --keycloak
* Jawad trouble shooted with Michael for a bit.  Apparently, his ingress controller did not come online.  Added this manually, but still would not load http://csoc.local/. Will try to troubleshoot later
* Carvin had a issue due to using a Windows laptop
* Jawad moved ahead to set up a Gen3 system
* Pulling images from docker takes a long time
* Needs to work on syncing with AWS secrets manager
* Deployed successfully via CSOC admin portal
* Not using ArgoCD right now - something Jawad may work on for the future.
* Security  for isolated account - Jawad will look into that.
* Current status
  * Security review has occurred, needs Zero Trust Architecture
  * Potentially next week will ask for more people to use it.


## Next Steps
* Possibility of next meeting to demo on the cloud rather than laptop



## About the Gen3 Community CSOC working group

The CSOC working group will focus on supporting the needs of organizations that run multiple Gen3 systems.

A commons services operations center (CSOC) is used by organizations that run more than one Gen3 system and allows a team of engineering and security staff to set up, configure, secure, operate, and monitor two or more data commons or data meshes. Part of the working group focus will be on the development of dashboards and tools that will enable an administrator to configure, launch, and monitor a data commons or mesh. We will also discuss and work on other improvements and topics of interest to multi-Gen3 organizations.

Projects completed by the working group will be merged into the Gen3 source code and made available to the community. As the Gen3 maintainer, CTDS will manage the working group, contribute code, and provide guidance to others on contributing to the Gen3 source code. Other participants will help provide requirements and also contribute code to Gen3.

### Useful Links

* Agendas and minutes can be found in the [Gen3 Community GitHub Repo CSOC Working Group folder](/CSOC_Working_Group_items).   
* Slack channel: [\#gen3\_working\_group\_csoc\_ext](https://gen3friends.slack.com/archives/C082FLTBYMA) - email Gen3 support to request to be added to the channel ([support@gen3.org](mailto:support@gen3.org))
