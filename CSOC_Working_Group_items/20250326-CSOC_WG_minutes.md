# Mar 26, 2025 | Gen3 CSOC Working Group

Attendees: CTDS: Sara Volk de Garcia, Jawad Qureshi, Peter Vassilatos; IU: Alan Walsh; D4CG: Luca Graglia; OCC: Plamen Martinov  

## Relevant meeting links   

* [Agenda](README.md#2025-march-2627)  
* [Recording of the mtg (YouTube)](https://youtu.be/8A1S5MS-5cQ)

## Mtg Minutes

* ## Update from CTDS on CSOC dashboard repo

  * Vision: High-level architecture diagram  
  * narrow down scope of “CSOC”  
  * Plan out what features to prioritize before releasing first (alpha) version.  
    * Concern assuaged about being able to “bring your own infrastructure” with OpenShift (Luca/D4CG)  
    * We know features will not be part of the alpha release  
    * What features would be most immediately helpful for the group  
      * BYOI is important to OCC  
      * Argo CD is in the center (for some very specific Gen3 features that aren’t supported in other ways) \-   
    * What we are planning  
      * Auth:Keycloak authentication (local users, remote ID provider) (future: RBAC fxnality, perhaps through Keycloak “groups” which has rbac-like fxnality)  
      * Wizard to configure your values.yaml based on questionnaire (details of questionnaire still in dev to make more human-friendly)  
      * Can choose which cluster to look into if you have multiple agents used  
      * A view for what’s happening in your commons (relying on Grafana stack, extrapolated from nginx logs)  
      * Overview of what’s happening with EC2 instances (now: only works with 1 acct, but working on multiple accounts)  
    * IaC part will not be part of the first release bc relies on community a lot  
    * We will support BYOInfrastructure  
    * Starting locally and bootstrapping a cluster (we’re interested in comparing our approach to Cluster API to boot management cluster) \- VERY interested in hearing other’s experience, bc we’re trying to decide whether it’s a direction we want to go  
    * Suggestion from Plamen (really more of a migration thing as we migrate from cloud-auto to argo-managed \- maybe input form?): add some additional (discovery of what you got already) controls to wizard: Which of your clusters do you want to manage, which features do you want to manage, which …etc to allow admin portal to be more likely to produce what you’re looking for (caveat: this is for people who already are running gen3 and implementing the dashboard post-development/deployment). This is consistent with what we are trying to do \- make changes in gitops, rely on argo to make the changes for us. We want to be able to be selective about what commons we tie to this (let us distinguish between commons we run vs we are just associated with)  
    * From alan: the “opinionated” approach to deployment is REALLY valuable, so hopefully the IaC stuff will be brought in as soon as possible, even if not in alpha  
    * How do you see operational tasks changing:  
      * Eg, EKS version upgrade:  
      * Today: re-run the same terraform with the version changed. We use a gitops approach for terraform (terragrunt, etc)  
      * How that changes with this deployment: you would rerun the same template with different variables checked. Docker containers around IaC we need to define some way to define input and govern output for deployment.   
      * Can only do one version bump at a time, so need to be aware of that in the development  
      * Since we’re doing open source, our users can get the original code and turn it into what they want/need  
      * Luca Suggestion: in the wizard \- don’t spend too much time on refining the selection bc there’s a history of not so much documentation, but this can be solved with more documentation  
      * Luca - Nice for later version – ability to add your OWN apis/service to the dashboard (add path to revproxy) \- even add your own jobs that you can set up an monitor  
      * Link out to docs about the services  
      * Different bundles of services \- add tags (eg “this is good for data mesh” “this is a framework service for everyone” etc)  

* ## Next Steps

**Action items**

- Michael will work with Jawad on listing out features that need community participation.  This may be in the form of GitHub issues or something else.  Will try to share before the next meeting.

## About the Gen3 Community CSOC working group

The CSOC working group will focus on supporting the needs of organizations that run multiple Gen3 systems.

A commons services operations center (CSOC) is used by organizations that run more than one Gen3 system and allows a team of engineering and security staff to set up, configure, secure, operate, and monitor two or more data commons or data meshes. Part of the working group focus will be on the development of dashboards and tools that will enable an administrator to configure, launch, and monitor a data commons or mesh. We will also discuss and work on other improvements and topics of interest to multi-Gen3 organizations.

Projects completed by the working group will be merged into the Gen3 source code and made available to the community. As the Gen3 maintainer, CTDS will manage the working group, contribute code, and provide guidance to others on contributing to the Gen3 source code. Other participants will help provide requirements and also contribute code to Gen3.

### Useful Links

* Agendas and minutes can be found in the [Gen3 Community GitHub Repo CSOC Working Group folder](/CSOC_Working_Group_items).   
* Slack channel: [\#gen3\_working\_group\_csoc\_ext](https://gen3friends.slack.com/archives/C082FLTBYMA) - email Gen3 support to request to be added to the channel ([support@gen3.org](mailto:support@gen3.org))
