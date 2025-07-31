# July 30, 2025 | Gen3 CSOC Working Group

Attendees: CTDS: Michael Fitzsimons, Sara Volk de Garcia, Jawad Qureshi, Peter Vassilatos; Aus BioCommons: Conrad Leonard, Nagasri Alava; IU: Alan Walsh, Jimi Adeyemi; D4CG: Luca Graglia, Bektemir Ashirmatov; OHSU: Kyle Ellrott; University of Aukland: Matt Pestle

## Relevant meeting links   

* [Agenda](README.md#2025-july-30)  
* [Recording of the mtg (YouTube)](https://youtu.be/FrzsUzQeNoQ)
* [Slides](20250730-CSOC_WG_slides.pdf)

## Mtg Minutes

### Brief updates from other CSOC groups   

* Nagasri (Australian BioCommons) - Moving to Frontend framework services, running into some issues.
* Matt Pestle (University of Aukland) - will be pulled into help support Gen3 for the New Zealand group
* Indiana University - have done some initial work with Kro
* Kyle Ellrot (OHSU) - GetLFS plug for Indexd
* Jawad (CTDS) - AuthZ work for keyloak, making terraform deployable from anywhere in one shot, can present at the next meeting




### Requestor presentation by Sara Volk de Garcia (CTDS)

* Sara gave presentation on setting up and using the [requestor service](https://github.com/uc-cdis/requestor) in Gen3.  A few highlights are included below, but see slides or video for details
* Requestor allows granting and revoking access to resources and policies.  It is scalable, auditable, may be integrated into third party tools (e.g. zendesk), and allows you to manage complex policy combinations
* Flexible - if you can come up with a policy, you can use requestor to grant access
* Conrad - what does this look like in the UI?
  * Sara gave example of how they use Zendesk to manage it



### REMS presentation by Conrad Leonard (Australian BioCommons)

* Conrad gave a presentation on how they use REMS to manage access to their Gen3 system.  This is a system that they use for non-Gen3 systems and so wanted to use it for Gen3 as well.  This is why they did not use Requestor.
* Discussed in detail the implementation and the different handoffs between different services
* They will go back to review requestor and see how much additional integration they can do there.  



### POC presentation by Jimi Adeyemi on Kro

* Kro may be a kubernetes native solution to replace both helm and terraform
* Indiana University group is exploring whether this may be a good solution for them
* Jimi presented on how this is set up for them
* Call for collaboration for anyone interested
  * Jawad volunteered to collaborate




### Topics for next mtg  

Jawad from CTDS will present on CSOC portal improvements and updates to Gen3 Terraform

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
