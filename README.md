# Kustomize overlay to deploy metallb v0.12 on Openshift with FRR mode enabled

*Disclaimer: upstream metallb is not supported on openshift, and in order to get support users should use
the red hat officially distributed one*

In order to deploy on metallb, all that needs to be done is running:

```bash
kubectl apply -k .
```

from a checkout of this project, or

```bash
kubectl apply -k https://github.com/fedepaol/metallbonocp.git
```


This kustomize overlay will deploy the [MetalLB Operator](https://github.com/metallb/metallb-operator/) with FRR enabled BGP.

After deploying the operator, the metallb deployment must be enabled by creating a MetalLB instance: 

```bash
apply -f https://raw.githubusercontent.com/fedepaol/metallbonocp/master/metallb.yaml
```

When using the Operator, users must configure MetalLB via CRDs. The configmap will not be available and any attempt to change it will be
overridden by the Operator.

## Documentation

In order to configure MetalLB, users can follow the [upstream documentation](https://metallb.universe.tf/configuration/), following the notes
about using the Operator. Additionally, the notes about [running in bgp mode](https://metallb.universe.tf/concepts/bgp/) must be checked.

The official [Openshift 4.10 documentation](https://docs.openshift.com/container-platform/4.10/networking/metallb/about-metallb.html) provides another
non supported good reference for how to configure MetalLB via the Operator.

