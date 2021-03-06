---
layout: layout.pug
navigationTitle: dcos storage device
title: dcos storage device
menuWeight: 10
excerpt:
---

This command manages physical devices.

There are typically storage devices that present as Linux devices on agents in the cluster.
The devices on a node can be assembled into volume providers that expose their storage capacity to the rest of the cluster.
For example, some SSDs `xvdb` and `xvde` on node `2aada917-0ba0-4041-bb1e-4f16a57cd1a0-S0` can be assembled into a LVM2 volume group on that node creating a new volume provider and specifying the `plugin` as `lvm` and listing `xvdb` and `xvde` as the devices.

# `list`

This sub-command lists physical devices.

**Note:** All devices will be listed, regardless of whether they are already in use or not.

## Usage

```bash
$ dcos storage device list [<devices>] [flags]
```

## Flags

```bash
-h, --help          help for list
    --json          Display the list of devices in json format.
    --node string   Only list devices on node.
```

## Arguments

```bash
<devices>   A space-separated list of devices to list. This argument is
            optional. If it is not provided all devices will be listed.
```

## Examples:

List all devices in the cluster.

```bash
$ dcos storage device list
NODE                                     NAME   STATUS  ROTATIONAL  TYPE  FSTYPE  MOUNTPOINT
c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1  xvda   ONLINE  false       disk  -       -
c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1  xvda1  ONLINE  false       part  xfs     /
c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1  xvdb   ONLINE  false       disk  ext4    -
c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1  xvde   ONLINE  false       disk  xfs     /var/lib/mesos
c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1  xvdf   ONLINE  false       disk  xfs     /var/lib/docker
c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1  xvdg   ONLINE  false       disk  xfs     /dcos/volume0
c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1  xvdh   ONLINE  false       disk  xfs     /var/log
```

```bash
$ dcos storage device list --json
{
    "devices": [
        {
            "name": "xvda",
            "status": {
                "state": "ONLINE",
                "node": "c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1",
                "metadata": {
                    "major": "202",
                    "minor": "0",
                    "name": "xvda",
                    "read-only": "false",
                    "removable": "false",
                    "rotational": "false",
                    "size": "161061273600",
                    "type": "disk"
                },
                "last-changed": "0001-01-01T00:00:00Z",
                "last-updated": "0001-01-01T00:00:00Z"
            }
        },
        {
            "name": "xvda1",
            "status": {
                "state": "ONLINE",
                "node": "c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1",
                "metadata": {
                    "fs-label": "root",
                    "fs-type": "xfs",
                    "fsuuid": "7f34470c-22e4-4c21-ad5d-64bc64b42ef3",
                    "major": "202",
                    "minor": "1",
                    "mount-point": "/",
                    "name": "xvda1",
                    "parent-name": "xvda",
                    "read-only": "false",
                    "removable": "false",
                    "rotational": "false",
                    "size": "161060208128",
                    "type": "part"
                },
                "last-changed": "0001-01-01T00:00:00Z",
                "last-updated": "0001-01-01T00:00:00Z"
            }
        },
        {
            "name": "xvdb",
            "status": {
                "state": "ONLINE",
                "node": "c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1",
                "metadata": {
                    "fs-label": "/mnt",
                    "fs-type": "ext4",
                    "fsuuid": "76dad0b0-f5d9-4408-8427-1a702676acea",
                    "major": "202",
                    "minor": "16",
                    "name": "xvdb",
                    "read-only": "false",
                    "removable": "false",
                    "rotational": "false",
                    "size": "161061273600",
                    "type": "disk"
                },
                "last-changed": "0001-01-01T00:00:00Z",
                "last-updated": "0001-01-01T00:00:00Z"
            }
        },
        {
            "name": "xvde",
            "status": {
                "state": "ONLINE",
                "node": "c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1",
                "metadata": {
                    "fs-type": "xfs",
                    "fsuuid": "b9e0cea3-9978-4cc7-a1df-0fe1440bde41",
                    "major": "202",
                    "minor": "64",
                    "mount-point": "/var/lib/mesos",
                    "name": "xvde",
                    "read-only": "false",
                    "removable": "false",
                    "rotational": "false",
                    "size": "53687091200",
                    "type": "disk"
                },
                "last-changed": "0001-01-01T00:00:00Z",
                "last-updated": "0001-01-01T00:00:00Z"
            }
        },
        {
            "name": "xvdf",
            "status": {
                "state": "ONLINE",
                "node": "c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1",
                "metadata": {
                    "fs-type": "xfs",
                    "fsuuid": "9fc123b8-2925-4d1b-b3db-a94363abae7d",
                    "major": "202",
                    "minor": "80",
                    "mount-point": "/var/lib/docker",
                    "name": "xvdf",
                    "read-only": "false",
                    "removable": "false",
                    "rotational": "false",
                    "size": "107374182400",
                    "type": "disk"
                },
                "last-changed": "0001-01-01T00:00:00Z",
                "last-updated": "0001-01-01T00:00:00Z"
            }
        },
        {
            "name": "xvdg",
            "status": {
                "state": "ONLINE",
                "node": "c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1",
                "metadata": {
                    "fs-type": "xfs",
                    "fsuuid": "eeeec093-3d2b-4bb9-96c0-efbddf6b61ab",
                    "major": "202",
                    "minor": "96",
                    "mount-point": "/dcos/volume0",
                    "name": "xvdg",
                    "read-only": "false",
                    "removable": "false",
                    "rotational": "false",
                    "size": "53687091200",
                    "type": "disk"
                },
                "last-changed": "0001-01-01T00:00:00Z",
                "last-updated": "0001-01-01T00:00:00Z"
            }
        },
        {
            "name": "xvdh",
            "status": {
                "state": "ONLINE",
                "node": "c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1",
                "metadata": {
                    "fs-type": "xfs",
                    "fsuuid": "2b9ee19c-3e51-4dd1-a769-329029afedf5",
                    "major": "202",
                    "minor": "112",
                    "mount-point": "/var/log",
                    "name": "xvdh",
                    "read-only": "false",
                    "removable": "false",
                    "rotational": "false",
                    "size": "21474836480",
                    "type": "disk"
                },
                "last-changed": "0001-01-01T00:00:00Z",
                "last-updated": "0001-01-01T00:00:00Z"
            }
        }
    ]
}
```

List all devices on a given node.

```bash
$ dcos node
   HOSTNAME         IP                         ID                    TYPE               REGION      ZONE
  10.10.0.39    10.10.0.39  c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1  agent            us-west-2  us-west-2c
master.mesos.  10.10.0.139    c67efa5d-34fa-4bc5-8b21-2a5e0bd52385   master (leader)  us-west-2  us-west-2c
```

```bash
$ dcos storage device list --node c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1
NODE                                     NAME   STATUS  ROTATIONAL  TYPE  FSTYPE  MOUNTPOINT
c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1  xvda   ONLINE  false       disk  -       -
c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1  xvda1  ONLINE  false       part  xfs     /
c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1  xvdb   ONLINE  false       disk  ext4    -
c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1  xvde   ONLINE  false       disk  xfs     /var/lib/mesos
c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1  xvdf   ONLINE  false       disk  xfs     /var/lib/docker
c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1  xvdg   ONLINE  false       disk  xfs     /dcos/volume0
c67efa5d-34fa-4bc5-8b21-2a5e0bd52385-S1  xvdh   ONLINE  false       disk  xfs     /var/log
```
