# October 29, 2025 | Gen3 CSOC Working Group

**Attendees:**  
* CTDS: Michael Fitzsimons, Sara Volk de Garcia, Jawad Qureshi, Elise, Ed;  
* Aus BioCommons: Nagasri Alava, Guerdon Mukama;   
* Univ Auckland, NZ (formerly NeSI): Matt Pestle, Claire Rye, Carvin Chen;  
* IU: Alan Walsh, Jimmy;   
* D4CG: Bektemir Ashirmatov, Luca;   
* OHSU: Kyle Ellrott;   
* OCC: Stephen Dranger, Danne Elbers  

## Relevant meeting links   

* [Recording of the mtg (YouTube)](https://youtu.be/jPd-QTjeWAQ)
* [Slides](20251029-CSOC_WG_slides.pdf)

## Agenda

* Brief Team Updates
* Update on OCC/Krumware CSOC - Stephen Dranger, OCC
* Quick update on Infrastructure as Code Dashboard - CTDS
* Open Discussion


## Mtg Minutes

### Brief updates from other CSOC groups   

* Alan/IU - Jimmy has the best update (on the Kro stuff – google “gen3 Kro”), but not on the call. Using the Gen3 terraform code a lot, lots of feedback. Starting to build out the graphs
* Bektemir & Luca/D4CG - moving env to Helm, almost there.
* Claire & Matt & Carven/Univ Auck: Big push on obs (Carvin shared last time) - working to integrate REMS.
* Nagasri & Guerdon/AusBio:  Nothing major for us for HCDC project. On track for dec go-live. Working on gen3 FEF for the omics 3 project.
* CTDS - we’re working with the University to get gen3 working on openshift. Openshift has strict security reqs, working to deploy on-prem. D4CG is also working on openshift at UChicago. (This infrastructure allows for PHI)

### Update on OCC/Krumware CSOC - Stephen Dranger, OCC

* See [Slides](20251029-CSOC_WG_slides.pdf) for most details
* Working with Krumware to work out a CSOC and IaC, as well as looking for a way to meet our workflow. Lots of DC across many AWS accounts.
* Rancher lets you control multiple K8s clusters, either on same or diff AWS accounts. Each acct has a WAF in front that can be controlled. Each DC has their own DB and secrets, and the key is that argo
* Using terraform to create the main rancher acct and all the envs. Krumware has their own terraform plugin (will be open source eventually). Use that plugin in your own terraform definitions (ARN, domain, IPs, etc). It will make all of the infra.
* Supports dev, testing, and prod envs for each commons, as well as multicommon support, so you can use the diff AWS accounts. The plugin allows security best practices (eg, cred rotation, postgres, certs, etc)
* Uses Gen3 helm charts
* Gives a nice look, thru Argo, at all the services and you can see the health overall or else drill down into one service
* OCC has a bunch of diff DC across AWS accounts so now can look across them without a bunch of k8s configs or going into diff aws accounts
* Helps apply best security practices across all the DC uniformly
* Argo CD is built into the terraform process, so it’s part of the infrastructure itself. Has logging and monitoring built in in each commons (under development)
Covers similar ground as Gen3 terraform. Difference is that one repo you have can go to multiple AWS accs. IaC defines a bunch of DC ecosystems. Also, argo cd is built into deployment.
* Question: do you already have terraform for GC or Azure? A: no plans for that currently. It would be a non-trivial upgrade. Helm charts work in GCP or Azure, but the rest of the infrastructure is the challenge
* Question: when do we expect to open this? A: at least the next 6 months.

### Update on CSOC Dashboard - CTDS (Jawad and Elise)
* Main screen for deployment wizard. You can bootstrap CSOC itself
* If running locally, just need docker. If in K8s pod, can configure the creds you wanna use.
* UI to input different parameters - trying to identify the minimum variables needed to deploy
* Stateless system – talking to either docker containers or pods that you have running for your system and you can do all the terraform operations from here.
* Terraform init pulls all the modules and providers and everything.
* checks your AWS infra agains your terraform state file, so tells you what you need to change before you run it.
* Once CSOC is bootstrapped into the cloud you can go to csoc.yourdomain.com using a WAF with an IP allow list.
* Can run without a database
* There is a branch for this in gen3-admin, called TFUI.
* Next: bring up just the terraform ui to bootstrap CSOC
* Q: how soon will it be production ready? (running TF and things from CSOC portal) A: we have deployed internally (not the TF, the k8s dashboards and argo) (deployed with keycloak), next steps are to kick off a security review.  


### Topics for next mtg  

* Volunteers for presenting at next month’s meeting (might move or cancel Nov mtg from the Wed before thanksgiving)
* Jimmy can give an update on Gen3 Kro
* Another suggestion - since Dec mtg will also be a problem, let’s move it til early/mid Dec
* Question: would a SaaS version of this ESOC make sense to people, where you don't even need to host it yourself, but you can spin up your own Gen 3… from something that we are hosting, potentially.  We could talk about that at a meeting.


## Next Steps

**Action items**

- [ ] ####  Michael to send out a doodle poll to reschedule November and December meetings

## About the Gen3 Community CSOC working group

The CSOC working group will focus on supporting the needs of organizations that run multiple Gen3 systems.

A commons services operations center (CSOC) is used by organizations that run more than one Gen3 system and allows a team of engineering and security staff to set up, configure, secure, operate, and monitor two or more data commons or data meshes. Part of the working group focus will be on the development of dashboards and tools that will enable an administrator to configure, launch, and monitor a data commons or mesh. We will also discuss and work on other improvements and topics of interest to multi-Gen3 organizations.

Projects completed by the working group will be merged into the Gen3 source code and made available to the community. As the Gen3 maintainer, CTDS will manage the working group, contribute code, and provide guidance to others on contributing to the Gen3 source code. Other participants will help provide requirements and also contribute code to Gen3.

### Useful Links

* Agendas and minutes can be found in the [Gen3 Community GitHub Repo CSOC Working Group folder](/CSOC_Working_Group_items).   
* Slack channel: [\#gen3\_working\_group\_csoc\_ext](https://gen3friends.slack.com/archives/C082FLTBYMA) - email Gen3 support to request to be added to the channel ([support@gen3.org](mailto:support@gen3.org))
