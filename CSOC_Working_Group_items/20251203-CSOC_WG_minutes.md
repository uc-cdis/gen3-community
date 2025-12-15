# December 3, 2025 | Gen3 CSOC Working Group

**Attendees:**  
* CTDS: Michael Fitzsimons, Sara Volk de Garcia, Jawad Qureshi, Elise, Bob;  
* Aus BioCommons: Nagasri Alava, Guerdon Mukama, Uwe Winter;   
* Univ Auckland, NZ: Claire Rye;  
* IU: Alan Walsh, Jimmy;   
* D4CG: Bektemir Ashirmatov, Luca;   
* OCC: Danne Elbers
* Australian NCI: Brian Davis
* OHSU: Kyle Ellrott  

## Relevant meeting links   

* [Recording of the mtg (YouTube)](https://youtu.be/FREBARkkuis)

## Agenda

* Brief Team Updates
* Update on Kro - Jimmy and Alan - Indiana University
* Bootstrapping the Gen3 CSOC - Jawad - CTDS
* Open Discussion


## Mtg Minutes

### Brief updates from other CSOC groups   

* Alan&Jimmy/IU - lots of deployments with new gen3 terraform. Super well documented - thank you!
* Bektemir & Luca/D4CG - Not many updates, just upgrading terraform and managing some conflicts as upgrades happen.
* Claire & Matt & Carven/Univ Auck:
* Danne/OCC: We can openly share code now and looking forward to moving forward with that. Outlining plan to move some of the commons to CSOCs
* Nagasri & Guerdon/AusBio:  From ACDC, final bits to go-live next week (soft launch)
* Kyle/OHSU: Nothing unique on devops side. We’ve been looking at index and how to improve managing multiple buckets (RBAC).
* UAuck: integrating REMS with gen3. Looking for other folks using REMS



### Update on Kro - Jimmy and Alan - Indiana University

* K8s SIG projects (AWS & Google) Amazon is now offering kro as an eks integration/addon, along with Argo CD (https://docs.aws.amazon.com/eks/latest/userguide/kro.html)
* Simplify deployment and mgmt of apps and resources by grouping them
* Common Expression Language
* Depends on existing controllers for infra mgmt
* NOT available til 2026
* IU is trying to be ready to go when they do launch Kro
* How kro works:
  * Creates resource graph definition (all infra bits, everything needed for deployment, and gen3 itself)
  * Once you define this, it’s very easy to create an instance of it
  * Take everything in helm and terraform, synthesize them into a set of graphs. Integrated with gen3 admin, it can be used to deploy
* https://kro.run/
* https://github.com/indiana-university/gen3-kro
* (Jimmy demos current iteration of their Gen3 Kro)
* Q: what happens if you delete one of the resources in the cluster, would it delete the AWS resource too? A: Depending on how you manage the graph, you can delete it without deleting stuff in AWS.
* You can spin up infra as easily as pods.
* Can eventually bake into Helm (bc it’s all K8s) - that’s what Jimmy does
* They are targeting this as POC https://github.com/uc-cdis/gen3-terraform/tree/master/tf_files/aws/generic_commons

### Bootstrapping the Gen3 CSOC - Jawad - CTDS
* How do you start from nothing, get something going locally, then get everything going
* Bootstrapping UI
* Minified UI
* Variable set (eg docker compose) - 2 env variables
* Cuts out some of the routes, and gets you autologged in with mock auth
* Keycloak operator (similar to Kro)
* Have bootstrap UI and the ability to spin up most of this
* Need to own a domain - ideally Route53
* Can select among different AWS profiles you have configured
* Deploys it locally then persists the state of everything in an S3 bucket
* Cost estimator
* Next steps: deploy csoc itself on the cluster, then also trying to create the DNS record automatically



### Topics for next mtg  

* Cost cutting/cost control




## About the Gen3 Community CSOC working group

The CSOC working group will focus on supporting the needs of organizations that run multiple Gen3 systems.

A commons services operations center (CSOC) is used by organizations that run more than one Gen3 system and allows a team of engineering and security staff to set up, configure, secure, operate, and monitor two or more data commons or data meshes. Part of the working group focus will be on the development of dashboards and tools that will enable an administrator to configure, launch, and monitor a data commons or mesh. We will also discuss and work on other improvements and topics of interest to multi-Gen3 organizations.

Projects completed by the working group will be merged into the Gen3 source code and made available to the community. As the Gen3 maintainer, CTDS will manage the working group, contribute code, and provide guidance to others on contributing to the Gen3 source code. Other participants will help provide requirements and also contribute code to Gen3.

### Useful Links

* Agendas and minutes can be found in the [Gen3 Community GitHub Repo CSOC Working Group folder](/CSOC_Working_Group_items).   
* Slack channel: [\#gen3\_working\_group\_csoc\_ext](https://gen3friends.slack.com/archives/C082FLTBYMA) - email Gen3 support to request to be added to the channel ([support@gen3.org](mailto:support@gen3.org))
