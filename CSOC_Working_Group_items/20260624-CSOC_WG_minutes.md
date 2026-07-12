# June 24, 2026 | Gen3 CSOC Working Group

**Attendees:**  
* CTDS: Michael Fitzsimons, Jawad Qureshi, Sara;  
* Aus BioCommons: Nagasri Alava, Guerdon Mukama;
* Univ Auckland, NZ: Carvin Chen;
* D4CG: Bektemir Ashirmatov;   
* OCC: Stephen Dranger

## Relevant meeting links   

* [Recording of the mtg (YouTube)](https://youtu.be/WYLIp0e_L0Y)

## Agenda

* CSOC Dashboard Setup on Cloud Walkthrough — Hands-on session. 

## Mtg Minutes

### Brief updates from other CSOC groups   

* Guerdon: REMS and Gen3 integration work
* Alan: normal operational work. Has been working on PRs for Gen3
* Bektemir: Issues with Cilium, working with Ajo on that
* Kyle: Going more experimental lately to support analysts in a project sharing files. Plugged into git LFS pattern using DRS as primary interface so you can track versions in GitHub. Put us pretty far ahead of DRS available in gen3, though. Created a new drs server called siphon (https://github.com/calypr/syfon) and trying to keep it with ga4gh Drs 1.6. To solve that needed to include RBAC in indexd because we needed project-level management of file listings. This also does the URL signing, listing of all files, and managing addition of new records. Important to make sure it paces with GA4GH. https://calypr.org 
* Carvin: exploring the CSOC platform, deployed into VM. Now trying to figure out the gen3 instance deployed by CSOC. There are some problems, it didn’t create the tables based on our dictionary. It still used some original tables from the DB. testing the FEF
* Stephen: No new updates, really. 



### CSOC Demo

* Started workshop by Jawad.
* Run the entirety of gen3 with csoc in google cloud. Intro to gen3 lite. Can be multiple instances, but we’re gonna just do single. Cost of running it yourself is ~$250/month. For the underlying k8s infra, we will use k3s, a lightweight k8s offered by rancher. 
* We will set up csos portal itself with keycloak. So that is gonna run in a separate namespace with the cluster. 
* Prerequisite is to have a google account
* script needed for workshop
https://raw.githubusercontent.com/uc-cdis/gen3-admin/refs/heads/master/scripts/setup-k3s.sh 
* Review video for rest of walkthrough



## About the Gen3 Community CSOC working group

The CSOC working group will focus on supporting the needs of organizations that run multiple Gen3 systems.

A commons services operations center (CSOC) is used by organizations that run more than one Gen3 system and allows a team of engineering and security staff to set up, configure, secure, operate, and monitor two or more data commons or data meshes. Part of the working group focus will be on the development of dashboards and tools that will enable an administrator to configure, launch, and monitor a data commons or mesh. We will also discuss and work on other improvements and topics of interest to multi-Gen3 organizations.

Projects completed by the working group will be merged into the Gen3 source code and made available to the community. As the Gen3 maintainer, CTDS will manage the working group, contribute code, and provide guidance to others on contributing to the Gen3 source code. Other participants will help provide requirements and also contribute code to Gen3.

### Useful Links

* Agendas and minutes can be found in the [Gen3 Community GitHub Repo CSOC Working Group folder](/CSOC_Working_Group_items).   
* Slack channel: [\#gen3\_working\_group\_csoc\_ext](https://gen3friends.slack.com/archives/C082FLTBYMA) - email Gen3 support to request to be added to the channel ([support@gen3.org](mailto:support@gen3.org))
