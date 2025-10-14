# Changelog v1.1

## Features


 - **[module]** Added the `D8VirtualizationDVCRInsufficientCapacityRisk` alert, which warns of the risk of insufficient free space in the virtual machine image storage (DVCR). [#1461](https://github.com/deckhouse/virtualization/pull/1461)
 - **[module]** Added the `KubeNodeAwaitingVirtualMachinesEvictionBeforeShutdown` alert, which is triggered when the node hosting the virtual machines is about to shut down but VM evacuation is not yet complete. [#1268](https://github.com/deckhouse/virtualization/pull/1268)
 - **[observability]** Added Prometheus metrics for virtual machine and virtual disk snapshots (d8_virtualization_virtualmachinesnapshot_info and d8_virtualization_virtualdisksnapshot_info), allowing users to monitor the presence of snapshots through their observability dashboards. [#1555](https://github.com/deckhouse/virtualization/pull/1555)
 - **[vm]** Added the ability to migrate VMs using disks on local storage. Restrictions:
    - The feature is not available in the CE edition.
    - Migration is only possible for running VMs (`phase: Running`).
    - Migration of VMs with local disks connected via `VirtualMachineBlockDeviceAttachment` (hotplug) is not supported yet.
    
    Added the ability to migrate storage for VM disks (change `StorageClass`). Restrictions:
    - The feature is not available in the CE edition.
    - Migration is only possible for running VMs (`phase: Running`).
    - Storage migration for disks connected via `VirtualMachineBlockDeviceAttachment` (hotplug) is not supported yet. [#1360](https://github.com/deckhouse/virtualization/pull/1360)
 - **[vmop]** Added an operation with the `Clone` type to create a clone of a VM from an existing VM (`VirtualMachineOperation` `.spec.type: Clone`). [#1418](https://github.com/deckhouse/virtualization/pull/1418)

## Fixes


 - **[core]** Fixed hot-plugging of disks with volume mode `Filesystem` on containerdv2. [#1548](https://github.com/deckhouse/virtualization/pull/1548)
 - **[core]** Added error reporting in the status of disks and images when the data source url is broken. [#1534](https://github.com/deckhouse/virtualization/pull/1534)
 - **[observability]** Fixed the graph on the virtual machine dashboard that displays memory copy statistics during VM migration. [#1474](https://github.com/deckhouse/virtualization/pull/1474)
 - **[vd]** respect user-specified storage class when restoring from snapshot [#1417](https://github.com/deckhouse/virtualization/pull/1417)
 - **[vi]** Virtual images now honor `spec.persistentVolumeClaim.storageClassName` when created from virtual disk snapshots. Previously, this setting was ignored in this case. [#1533](https://github.com/deckhouse/virtualization/pull/1533)
 - **[vm]** The `Network` condition of virtual machine will now be displayed only if the sdn module is present or if there are user-actionable messages. Previously, it remained in the Unknown state. [#1567](https://github.com/deckhouse/virtualization/pull/1567)
 - **[vm]** Prohibit duplicate networks in the virtual machine `.spec.network` specification. [#1545](https://github.com/deckhouse/virtualization/pull/1545)
 - **[vmbda]** Fixed an issue where detaching a hot-attached image from a virtual machine could hang. Previously, deletion of the `VirtualMachineBlockDeviceAttachment` resource could get stuck in the Terminating state. [#1542](https://github.com/deckhouse/virtualization/pull/1542)
 - **[vmclass]** Use qemu64 CPU model for Discovery and Features types to fix nested virtualization on AMD hosts [#1446](https://github.com/deckhouse/virtualization/pull/1446)
 - **[vmip]** Added validation for static ip addresses to ensure that the requested address is not already in use within the cluster. [#1530](https://github.com/deckhouse/virtualization/pull/1530)
 - **[vmop]** This PR enhances the `VirtualMachineOperation` CRD by adding validation rules to ensure safe and valid resource naming during clone operations. [#1522](https://github.com/deckhouse/virtualization/pull/1522)
 - **[vmop]** Fix the problem where a disk that in the "Terminating" phase  was wrongly added to kvvm's volumes during a restore operation in Strict mode. [#1493](https://github.com/deckhouse/virtualization/pull/1493)
 - **[vmop]** Fixed garbage collector behavior: previously, all VMOP objects were deleted after restarting the virtualization controller, ignoring cleanup rules. [#1471](https://github.com/deckhouse/virtualization/pull/1471)

