---
copyright:
  years: 2024, 2025
lastupdated: "2025-12-09"
keywords:
subcollection: deployable-reference-architectures
authors:
  - name: Babitha Padiri
production: true
deployment-url:
docs:
image_source: https://github.com/terraform-ibm-modules/terraform-ibm-powervs-workspace/reference-architectures/standard/deploy-arch-ibm-pvs-ws-standard.svg
use-case: ITServiceManagement
industry: Technology
content-type: reference-architecture
version: v4.1.0
compliance:
---

{{site.data.keyword.attribute-definition-list}}

# Power Virtual Server workspace
{: #deploy-arch-ibm-pvs-ws-standard}
{: toc-content-type="reference-architecture"}
{: toc-industry="Technology"}
{: toc-use-case="ITServiceManagement"}
{: toc-compliance=""}
{: toc-version="v4.1.0"}


This solution deploys an IBM® Power Virtual Server (PowerVS) workspace using [terraform-ibm-powervs-workspace](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-workspace) in the `solutions/standard` directory.


## Architecture diagram
{: #standard-architecture-diagram}

Architecture diagram for 'Power Virtual Server workspace' - Standard solution(deploy-arch-ibm-pvs-ws-standard.svg "Architecture diagram"){: caption="Figure 1. PowerVS workspace with optional subnets, images, and transit gateway" caption-side="bottom"}

## Design requirements
{: #standard-design-requirements}

Design requirements for 'Power Virtual Server workspace' - variation 'Standard'.(heat-map-deploy-arch-ibm-pvs-ws-standard.svg "Design requirements"){: caption="Figure 2. Scope of the solution requirements" caption-side="bottom"}

IBM Cloud® Power Virtual Servers (PowerVS) is a public cloud offering that an enterprise can use to establish its own private IBM Power computing environment on shared public cloud infrastructure. PowerVS is logically isolated from all other public cloud tenants and infrastructure components, This solution provides a simple, modular framework to deploy a PowerVS workspace with ssh key, optional networking and image import features from the IBM Cloud.

## Key solution features
- Minimal configuration for quick deployment
- Modular options for private subnets, public network, and transit gateway
- Secure SSH key management
- Optional import of custom images from COS


## Components
{: #standard-components}

### PowerVS workspace architecture decisions
{: #pvs-components-workspace}

| Requirement | Component | Choice | Alternative choice |
|-------------|-----------|--------------------|--------------------|
|* Create an IBM® Power Virtual Server workspace|PowerVS workspace|Create a single PowerVS workspace in the chosen region and in an existing resource group or a new resource group||
|* Create an SSH key for administrative access|SSH key||Require users to provide their own SSH public key or reference a key in Secure Cloud Key Management|
|* Optionally import up to three custom OS images from Cloud Object Storage|Custom OS images|Import up to three images from COS into the PowerVS workspace using provided COS credentials and object locations|Skip image import and use standard public PowerVS images; or import images manually after deployment|
|* Optionally create private subnets for workload isolation|Private subnets|Create 1, 2 or 3 private subnets as requested |Use a single private subnet for all workloads or create additional subnets manually post-deployment|
|* Optionally create a public subnet for external access|Public subnet|Create one public subnet ||
|* Optionally attach the PowerVS workspace to a transit gateway to connect VPC services|Transit gateway|Attach workspace to a local transit gateway to enable connectivity with VPC and other networks|Do not attach to transit gateway; rely on site-to-site VPN, direct internet, or other connectivity mechanisms|

{: caption="Table 1. PowerVS workspace architecture decisions" caption-side="bottom"}


## Next steps
{: #standard-next-steps}

- Review and confirm input variables (region, resource group, COS locations, SSH public key).
- Validate network connectivity (private subnets and transit gateway attachments).
- Verify imported images are present and usable in PowerVS.
