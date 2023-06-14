# zarf-podinfos

> **Warning**
>
> NOT FOR PROD USE!!!

## prereq

- k3d cluster
  - zarf init
  - dubbd deployed (big bang) per [these instructions](https://github.com/defenseunicorns/uds-package-dubbd/blob/main/README.md#example-dubbd-deployment---using-pre-built-oci-packages-here)
- kubecontext set to the above cluster

## optional steps

- create your own tls secret (using mkcert or something)

```bash
# replace the "PATH-TO*" with your cert & key file names
kubectl -n podinfo-too create secret tls podinfo-tls-secret --cert PATH-TO-CERT-FILE --key PATH-TO-KEY-FILE --dry-run=client -o yaml
```

- update the k8s-manifests file(s) accordingly (cue the `vi`)

## package and deploy

```bash
# create zarf package
zarf package create --architecture amd64 . --confirm

# deploy zarf package
date; time zarf package deploy --confirm zarf-package-podinfos-*.tar.zst
```

## test

- get the LB IPs of the istio ingressgw's
- update your hosts file accordingly & curl away!

## releases are done with release-please

this repo uses [release-please](https://github.com/google-github-actions/release-please-action#release-please-action) GHA for cutting releases automatically
