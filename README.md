# aksc-petclinic

`status = in-progress`

This repo deploys the Spring Petclinic application onto an Azure Kubernetes Cluster, all using bicep in a single `code-golf` step.

## Aim

To deploy a sample of the Petclinic application into the Azure Kubernetes Service all using Bicep. This is not a real-world pattern, but great for producing samples quickly.

## Notable components

### ACR

Rather than use publicly hosted docker images, we will import them into an Azure Container Registry where they can be scanned by Microsoft Defender before being used in Kubernetes.

### AKS

The AKS Construction Set is being leveraged to deploy a secure cluster in a simple way.

## The bicep

TODO: Diagram

Bicep File | Description
---------- | -----------
main.bicep | Orchestrates creation of all resources
aks-construction/main.bicep | Creates AKS and associated infrastructure components
importImages.bicep | Imports container images into ACR from DockerHub


## Lets deploy it!

The Azure CLI is the only prerequisite. If you deploy from the Azure CloudShell then this makes the process even simpler.

```bash
az group create -n aks-petclinic -l eastus
az deployment group create -g aks-petclinic -f main.bicep
```

## Other Steps???

Well it looks like we can't go full bicep-code-golf, the issues outstanding are;

Issue | Error? | Resolution | Impact 
----- | ------ | ---------- | ------
Wavefront | Error: secret "wavefront" not found | Need to obtain a Wavefront API key and then create a Kubernetes secret. | App seems to work...

## Repo Notes

This repo uses git submodules. The following commands were run to clone the respective repositories at a point in time.
This was done rather than forking as
- This project will not be contributing back to the Petclinic sample
- Submodules captures the repo at a point in time, which is good for our sample. We can fetch latest and test as this sample is periodically reviewed.

```bash
git submodule add https://github.com/Azure/AKS-Construction.git aks-construction
git submodule add https://github.com/spring-petclinic/spring-petclinic-cloud.git spring-petclinic-cloud
```
