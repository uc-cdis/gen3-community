# Jan 29, 2025 | Gen3 CSOC Working Group

Attendees: CTDS: Michael Fitzsimons, Sara Volk de Garcia, Jawad Qureshi, Bob Grossman, Peter Vassilatos, Fay Booker;  
Aus BioCommons: Uwe Winter, Guerdon Mukama; IU: Alan Walsh, Amy Burns; D4CG: Brian Furner, Luca Graglia; OHSU: Kyle Ellrott; NeSI: Claire Rye; KrumWare: Colin Griffin

## Relevant meeting links   

* [Agenda](README.md#2025-january-2930)   
* [Slides](20250129-CSOC_WG_slides.pdf)
* [Recording of the mtg (YouTube)](https://youtu.be/yF-T97MggUQ)

## Mtg Minutes

* ## Presentation by Australian BioCommons (Guerdon) on deployment

  * Infrastructure as Code (IaC) \- allows IF to be defined, versioned and deployed as code to ensure consistency. Terraform is an example of this  
  * IaC solves problems relating to deploying in multiple envts, and manages dependencies (network, databases). Allows traceable IF changes through GitOps  
  * Multi-account strategy. Enables least-priv IAM policies, isolates workloads, prevent resource contention btwn envts  
  * Gitops ensures auditable, trackable deployment  
  * IaC with AWS CDK \- leverage AWS EKS blueprints, handles complex resources (custom code)  
  * Deployment order:  
    * Network pipeline \-\> VPC, private, public, isolated subnets, NAT gateways, WAF  
    * Database pipeline → RDS, Opensearch(elasticsearch)  
    * Creds pipeline → DB cred in secrets mgr  
    * EKS pipeline → EKS cluster, IAM roles (also brings in Gen3 charts)  
    * Resources pipeline → SQS queues, SNS, S3 buckets  
    * squid/proxy pipeline → self healing properties  
  * Deployment flow: deploye change to GH, then through AWS CodePipelines, then proceeds through envts to prod   
  * Quick start deployment: EKS cluster. Need VPC with private and public subnets (esp for Prod), Database Service, Creds in AWS secrets mgr  
    * Understand Gen3 Helm Charts  
    * Fork the pipeline repos (links at end of prez)  
    * Set up cred in AWS secrets mgr, configure  
    * Deploy\!  
  * Compare to cloud-automation  
    * No need for mgmt vm  
    * Integrate CI/CD to reduce errors  
    * Simpler

 (Slide 14 in slide deck is a great summary of comparison of Gen3 Deployment with AWS CDK Pipelines to Cloud Automation)

* Takeaways: Reproducible. Able to control versions. Easier to maintain.   
  * Self-healing for squid – they expect to make that opensource, so he can share it  
  * CDK will do cloud formation in the background, can also run outside pipelines (even GH actions). CodePipeline is nice because you can connect the envts together and easily promote changes through envts  
  * They have just one repo with envts separated by directory.   
  * CDK can run in a container, then provision the whole pipeline. but, you would probably lose the visibility because you aren’t using a pipeline.   
  * Colin is on GC, Azure, on prem, and … . They follow a 2 stage bootstrapping process for flexibility. But, modules are different depending on what envt they go into. Looking to donate terraform models for different modules. Reworking terraform for AWS to allow bootstrapping.   
  * “expected/estimated AWS costs for the environment”: I will get back to you with exact figures, but varies from account to account. The tools account cost is minimal. Others are in the range of $800 \- $2000  
  * We should communicate with each other in the community about what we’re doing to try to prevent duplicating efforts  
  * Note from Colin: recommends External Secrets Operator and Cluster API

* ## Update from CTDS on CSOC deployment

  * What are we trying to build:  
  * CSOC dashboard  
  * Any infrastructure prov would be part of this portal  
  * Create endpoint lets you create IAM role in your acct which allows the CSOC to assume this role, so now you have access to do stuff in the AWS (or whatever cloud). This will ultimately allow you to create a new cluster based on bootstrapping, then can deploy gen3 with a wizard.   
  * Need a way to do “inventory mgmt” (eg S3 buckets, etc). Looking to build that into portal  
  * Consider looking into AWS marketplace  
  * Colin and OCC have stuff on Marketplace  
  * Institutionas/orgs are seeing the need to adopt cloud-native K8s. we are encouraging them to look at it as both managing commons AND more generally how to manage your compute. To that end \- try to make sure the tools needed to manage a commons doesn’t conflict with what they need to do other stuff

* ## Next Steps

* Perhaps ask Colin and Jawad to try to develop a picture of what this looks like, and ask AusBio for their input also.

**Action items**

- [ ]

## About the Gen3 Community CSOC working group

The CSOC working group will focus on supporting the needs of organizations that run multiple Gen3 systems.

A commons services operations center (CSOC) is used by organizations that run more than one Gen3 system and allows a team of engineering and security staff to set up, configure, secure, operate, and monitor two or more data commons or data meshes. Part of the working group focus will be on the development of dashboards and tools that will enable an administrator to configure, launch, and monitor a data commons or mesh. We will also discuss and work on other improvements and topics of interest to multi-Gen3 organizations.

Projects completed by the working group will be merged into the Gen3 source code and made available to the community. As the Gen3 maintainer, CTDS will manage the working group, contribute code, and provide guidance to others on contributing to the Gen3 source code. Other participants will help provide requirements and also contribute code to Gen3.

### Useful Links

* Agendas and minutes can be found in the [Gen3 Community GitHub Repo CSOC Working Group folder](/CSOC_Working_Group_items).   
* Slack channel: [\#gen3\_working\_group\_csoc\_ext](https://gen3friends.slack.com/archives/C082FLTBYMA) - email Gen3 support to request to be added to the channel ([support@gen3.org](mailto:support@gen3.org))
