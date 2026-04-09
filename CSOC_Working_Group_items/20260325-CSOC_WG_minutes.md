# October 29, 2025 | Gen3 CSOC Working Group

**Attendees:**  
* CTDS: Michael Fitzsimons, Sara Volk de Garcia, Jawad Qureshi, Elise, Ed, Ajo, Sai, Bob;  
* Aus BioCommons: Nagasri Alava, Guerdon Mukama;
* Univ Auckland, NZ: Carvin Chen;  
* D4CG: Bektemir Ashirmatov, Luca;   
* OCC: Stephen Dranger

## Relevant meeting links   

* [Recording of the mtg (YouTube)](https://youtu.be/S-OwfpRb1lM))

## Agenda

* How to reduce EC2 costs in EKS using cilium
* How to reduce portal costs and build times
* Karpenter configurations


## Mtg Minutes

### Brief updates from other CSOC groups   

* Alan&Jimmy/IU - (update from Michael) Michael met the ARDaC group in person at the ARDaC Annual Retreat
* Bektemir & Luca/D4CG - Working on openshift
* Claire & Matt & Carven/Univ Auck: Planning to use CSOC admin hopefully soon
* Nagasri & Guerdon/AusBio:  Starting new gen3 project soon
* Stephan/OCC - putting bloodpac on hold and looking at a new


### Karpenter - compute provisioning

* Goal is to reduce AWS compute costs (~70%) for k8s
* Use karpenter and spot instances - how to take advantage of cost-benefit while keeping platform reliable
* Enforce spot usage with karpenter constraints - workloads only run on spot nodes and prevents accidental use of
* Restrictions to instance sizing to avoid very small inefficient nodes and very large expensive nodes
* Consolidation (most important) - removes empty node and underutilized nodes, replaces nodes with cheaper alts. Aggressive optimization with controlled disruption (controls how many nodes can be replaced at once (eg, 80% max).
* Handling spot interruptions (uptime)
  * Replica for all workloads
  * Pod disruption budgets
  * Separate workloads - critical goes on on-demand, less critical to spot
* If you are currently using cluster autoscaler, to transition to use this, follow deployment of karpenter instead. With carpenter, everything controlled with CRDs, so yaml files that apply to k8s. You should be able to just enable/deploy from helm charts and it should be pretty well set up, and scale down the autoscaler pods, and then carpenter will take over.
* Spot instances are compute that is not being used by other AWS customers. So they’re a lot cheaper

### Cilium

* The problem: our deployments use fewer CPU/Memory requests. But, pod density became a limiting factor. Each C2 instance only has aa certain amt of eni’s that you can attach. So - flex instances allow you to double the # of IP addresses per node.Even so, we still were hitting pod density limit.
* New solution: virtual ips (cilium uses vip address for pod networking, not host IPs). Allows a hi pod limit of 2000/node. So tighter node packing,running more pods per node efficiently
* Set up cilium
  * Enable cilium in cluster level resources chart(it’s on a feature branch now)
  * Roll pods to use vips. Maybe short downtime in transition.
  * Optionally remove old daemonsets
* More features:
  * hubble for network traffic/visibility
  * Replace calico with cilium policies
  * Service to service TLS
* Sometimes we have seen an issue where a subnet runs out of IPs - cilium solves that issue!

### Shrinking Portal
* Portal is high memory at startup (build), even tho it’s lightweight eventually
* New approach - cache build objects in persistent volume. Instead of building each time, compute checksum to verify cached config. If it finds it, just pull that. If it doesn’t find a matching set of files, it will create a job to build new artifacts to store in persistent volume
* It’s on a feature branch for now. If you want to try, you would
  * Create an iam role with access to an s3 bucket with a portal service account that can use it.
  * Update values yaml to enable the rebuild portal workflow, set bucket and role name
* Question: Is this applicable to FEF?
  * FEF is already really lightweight, so you don’t need this

### Rethinking stateful services
* K8s vs managed cloud services (but these arent cheap!)
* For lower-level envs, is it worth paying for mgd serv, or can you endure downtime or some dataloss
* Running postgresql in k8s
* Bitnami is out of support, so looking at cloud native pg
* Aurora is helpful, bc helps us scale down when not in use
* With cloud native pg, helps give you a lot of benefits like AWS RDS without needing to go to the cloud

### AWE Cost/usage report
* Practice good cloud hygiene
* If you want to figure out what is accruing costs, use these filters and groups on the side
* Can choose what services you want to include in filter, for ex


### Potential Topics for next time
* hands-on training session to bootstrap a CSOC portal and deploy an env.
* Could also show jawad’s development workflow
* General technical deep-dive session


## Next Steps

**Action items**


## About the Gen3 Community CSOC working group

The CSOC working group will focus on supporting the needs of organizations that run multiple Gen3 systems.

A commons services operations center (CSOC) is used by organizations that run more than one Gen3 system and allows a team of engineering and security staff to set up, configure, secure, operate, and monitor two or more data commons or data meshes. Part of the working group focus will be on the development of dashboards and tools that will enable an administrator to configure, launch, and monitor a data commons or mesh. We will also discuss and work on other improvements and topics of interest to multi-Gen3 organizations.

Projects completed by the working group will be merged into the Gen3 source code and made available to the community. As the Gen3 maintainer, CTDS will manage the working group, contribute code, and provide guidance to others on contributing to the Gen3 source code. Other participants will help provide requirements and also contribute code to Gen3.

### Useful Links

* Agendas and minutes can be found in the [Gen3 Community GitHub Repo CSOC Working Group folder](/CSOC_Working_Group_items).   
* Slack channel: [\#gen3\_working\_group\_csoc\_ext](https://gen3friends.slack.com/archives/C082FLTBYMA) - email Gen3 support to request to be added to the channel ([support@gen3.org](mailto:support@gen3.org))
