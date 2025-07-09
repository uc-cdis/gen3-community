# June 25, 2025 | Gen3 CSOC Working Group

Attendees: CTDS: Michael Fitzsimons, Sara Volk de Garcia, Jawad Qureshi, Clint Malson, Peter Vassilatos, Bob Grossman; Aus BioCommons: Guerdon Mukama, Nagasri Alava; IU: Alan Walsh; D4CG: Luca Graglia, Bektemir Ashirmatov; OHSU: Kyle Ellrott, Liam Beckman  

## Relevant meeting links   

* [Agenda](README.md#2025-june-25)  
* [Recording of the mtg (YouTube)]()

## Mtg Minutes

### Brief updates from other CSOC groups   

  * Guerdon & Nagasri/AusBio \- rolling out centralized IP address mgmt using [AWS IPAM](https://docs.aws.amazon.com/vpc/latest/ipam/what-it-is-ipam.html) to avoid subnet conflicts across envts/projects spread over several AWS accts. Currently configuring access for existing accounts. Migrating from Gen3 user sync to integrated Auth0 to improve consistency and simplify access mgmt. Use Auth0 to assign user to roles. Team exploring RAMs in a PoC phase to support standardized data access request workflows. Also \- welcome Nagasri. (Followup note: IPAM avoids IP conflicts in subnets when you create your VPCs)  
  * Liam & Kyle/OHSU \- Internal instances of Gen3, spinning up external server. These are using Helm, working great (nice job, PE team). Need to add Argo workflows still.   
  * Luca & Bektemir/G4CG \- no updates shared  
  * Alan/IU \- First successful end to end deployment using new terraform\! Has some small notes about improvements \- has submitted a few PRs. Growing as CSOC \- request this week for several new environments for new projects. Looking forward to moving forward with Crow. At AWS public sector summit, thru AWS team connected with a Crow/Argo person on the EKS team. Hope to have something to demo to this group soon. (Gonna share a logo with CTDS so we can put them under “powered by Gen3”)  

### Updates from CTDS on CSOC development

  * We made the [Gen3 admin repo](https://github.com/uc-cdis/gen3-admin) public. There’s a docker compose file to get you started if you want to test locally. GSoC intern helping CTDS to add extra components to this.   
  * **Cloud-auto migration to Helm**:  
    * Our status: we have migrated most of our environments, and we’re in the final phase of validating and testing before cutover  
    * Goal: To finally start using Helm in CTDS prod deployments  
    * Some security enhancements compared to admin VMs (used with cloud-auto)  
      * The problem is that they stored all the secrets in plaintext in the gen3 secrets folder (not great). So, helm lets us modernize secrets management and get better gitops integration instead of homebrewed one. And, allow managing infrastructure completely separate from deployments  
    * Our migration strategy: blue/green deployment  
      * No downtime, Namespace isolation: Spin up both a helm and a cloud auto namespace \- but they’re both pointing at the same databases. (same secrets, same configuration)  
      * Traffic Mgmt: While testing, the operator can update the local hosts file to point it at the \_\_ balancer  
      * Pod-level routingSome services require going through DNS to reach our services. For that, we have a mutating webhook where any namespaces with “helm” in their name gets the same thing added to their pod.   
    * Our approach has some prerequisites  
      * We use [Argo CD](https://argoproj.github.io/cd/) for continuous deployment with all config stored in Git.  
      * [External secrets operator](https://external-secrets.io/latest/): all our secrets are in AWS secrets manager  
      * Terraform/Terragrunt (this isn’t public) but we will preview our gitops approach to managing infrastructure. ([Atlantis](https://www.runatlantis.io/docs/using-atlantis))  
    * Step 1: migrate secrets and generate configs  
      * [We've developed a tool (python script in cloud-auto repo)](https://github.com/uc-cdis/cloud-automation/blob/master/helm-migration-script/migrate-to-helm.py) that can take your existing cloud automation deployment. Creates and migrates all your secrets into AWS secrets manager and spits out values yaml that is clean (no secrets) and preconfigured for all the services as they are currently set.   
    * Step 2: Set up IAM RSA  
      * [Gen3-terraform IRSA roles](https://github.com/uc-cdis/gen3-terraform/tree/master/tf_files/aws/irsa_role) (open source)  
      * [Aws docs](https://docs.aws.amazon.com/eks/latest/userguide/iam-roles-for-service-accounts.html)  
      * Currently doing manually \- create IAM roles for service accounts so our services have identities in AWS so they can access the things they need. We made a generic terraform module for this where you create an IAM role with some policy attached and a service account reference so you can just connect it back to EKS if you're running in amazon.   
      * For our terragrunt, we have structured it so we have an AWS folder with all our AWS accounts so, per environment, we can deploy multiple terraform modules at once.   
      * We have configured [Atlantis](https://www.runatlantis.io/docs/using-atlantis) that will let you audit who made what changes to your infrastructure  
    * Step 3: Gitops repository  
      * [Gen3-gitops repo](https://github.com/uc-cdis/gen3-gitops) is now public, so you can follow along and see how we’ve set up our env’ts  
      * There are integration tests there. New ci/cd tests are running in GH actions, so you can test your whole envt when you’re creating a PR, based on the values yamls that are provided.   
      * Can see our folder structure. Changes made there are instantly deployed.   
      * Once you have set up ArgoCD, you configure it with your application, and then it will start deploying.   
    * Step 4: Validation and testing  
      * Where we are currently at  
      * Operators who are testing can make sure there's no regression in the new helm-based envt compared to functionality of the old envt  
      * Document any differences. Update the migration tool with any of the values we missed.   
      * When teams are happy, can do the cutover from cloud-auto to helm deployment   
    * Transition from adminvm to csoc portal  
      * Since it’s not quite production ready, but we’re turning off adminvm’s \- we will temporarily use a jumpbox to provide controlled access to production sites. Has AL23 with FIPS enabled, so they have access to kubectl, psql, es, aws cli  
      * Access via aws ssm (auditable) (not ssh)  
      * No actual secrets on the box\!  
    * Future plans  
      * Continue updating csoc portal to get prod-ready  
      * Gitops improvements: eg, shorten values yaml and reference where it is in git (smaller config file, easier to audit/review)  
      * QoL (slackbots)  
      * Add Helm charts to release process with single release tag (so you don’t have to update individual services)  
      * CI testing  
      * Crossplane: in-between terraform and k8s. Each service in their helm charts can define their cloud reqs. Want to move that all to charts so you don’t have to configure some things in terraform, some in helm. Also makes it easier to spin up/tear down cloud resources  
    * Questions:  
      * Future of cloud-auto repo? Squid white-list files gonna be dealt with and also split out so community can whitelist their own things, not just what we declare. Eventually gonna be archived  
      * Secrets: what about if you have completely new secrets (not migrating)? You should be able to create new secrets in the gen3 module of terraform. (Note: there is not info in the docs about this \- we need to add it. Request for an example end-to-end deployment showing that secrets management, too.   
      * Is there a plan to support OIDC in the gen3 admin portal? Yes \- keycloak (which has oidc). Then configure identity providers (SAML or OIDC). Also will bring in some way to get Authz.   
      * What’s required to integrate existing deployments: you set up the portal (via a helm chart for API and front end). Then import existing cluster. Eventually gonna be less cluster-focused and more gen3-env’t-focused so you can monitor what’s going on in the envt vs what’s in k8s  
      * Helm secrets \- how do you manage the secrets? In the values yaml files, there are not secrets but references to where the secrets are (for us, in AWS secrets manager).   
      * How do you do the actual deployments (what triggers it Argo CD): it’s an application controlled by k8s yaml. Deploys the helm chart. all of our clusters that are running applications run a separate Argo CD  
      * Where are you running the Terraform and Terragrunt files? So you can do it in GitHub Actions as well, but we are using a tool called Run Atlantis. Atlantis basically sits there and watches for the pull requests that you're making into your Terragrunt repository. Then it runs Terraform for you, so we can restrict cloud credentials to Atlantis. Note:  Perhaps we need a more in-depth write-up of how we're using TerraGrunt, how we're using Atlantis, etc.   
      * In the Gen 3 admin, do you have a role other than admin working? Not yet. Working on more granular roles (create new envs, kick off things).   

### Topics for next mtg  

Discussion to be continued

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
