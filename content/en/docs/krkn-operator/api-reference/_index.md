---
title: API Reference
description: Fields of every krkn-operator custom resource
weight: 6
---

The operator is driven by custom resources. These pages are generated from the
CRDs in krkn-operator, so a field here always matches the cluster.

To fix a description, edit the Go doc comment in `api/v1alpha1` upstream. The
next sync carries it here.

<!-- This index is regenerated on every sync. Add prose to a kind's own page,
     which the bot writes once and never touches again. -->

| Kind | Short name | Fields |
| --- | --- | --- |
| [KrknFileType](krknfiletypes/) | `kft` | 2 |
| [KrknGraphRun](krkngraphruns/) | `kgr` | 47 |
| [KrknOperatorTarget](krknoperatortargets/) | `kot` | 9 |
| [KrknOperatorTargetProvider](krknoperatortargetproviders/) | `kotp` | 3 |
| [KrknOperatorTargetProviderConfig](krknoperatortargetproviderconfigs/) | `kotpc` | 8 |
| [KrknScenarioRun](krknscenarioruns/) | `ksr` | 53 |
| [KrknTargetRequest](krkntargetrequests/) | `ktr` | 6 |
| [KrknUser](krknusers/) | `ku` | 10 |
| [KrknUserGroup](krknusergroups/) | `kug` | 4 |
