# VSS Block API - cURL Commands

This document contains cURL commands converted from the VSS Block Postman collection.

## Variables

Replace these variables in the commands below:
- `{{server}}` - Your storage server hostname (e.g., `tevssb.ecoe.io`)
- `{{username}}` - Your username (default: `admin`)
- `{{password}}` - Your password
- `{{token}}` - Session token obtained from authentication
- Other variables like `{{serverId}}`, `{{volumeId}}`, `{{poolId}}`, etc. should be replaced with actual IDs

---

## Basic Operations

### Get Session Token
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  "https://192.168.180.30/ConfigurationManager/simple/v1/objects/sessions"
```

### Get Version (No Auth Required)
```bash
curl -k -X GET \
  "https://{{server}}/ConfigurationManager/simple/configuration/version"
```

### Get License
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/licenses"
```

### Get License by ID
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/licenses/{{license}}"
```

### Get License Setting
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/license-setting"
```

### Get Jobs
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/jobs"
```

### Get Specific Job
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/jobs/f4246100-ec78-4791-9f79-8d611f025b7f"
```

### Get Storages
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/storage"
```

### Get Event Logs
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/jobs"
```

### Apply License
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Expect:" \
  -H "Content-Type: application/json" \
  -d '{
    "keyCode": "0OEDWW402K4ZZZC2A7GU2MKLZFOXEVCTAR8P6N4L2J0HYFWDUBSAQ7O41IZGXEVCEWU6EKW6UXM"
}' \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/licenses"
```

### Upload License
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -H "Expect:" \
  -d '{"keyCode":"UCN5I5YRZG321NG59OJ7VRDBJC49KV6HS3EP0BMX8JU5GR2DOZAMW7ISJU5GR2DOKWO6LUOPNRG"}' \
  "https://tevssb.ecoe.io/ConfigurationManager/simple/v1/objects/licenses"
```

### Get Software Update File Details
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "content-type: multipart/form-data" \
  -H "Expect:" \
  -H "Authorization: Session {{token}}" \
  -F "softwareUpdateFile=@/home/user/update/hsds-update-01050000-2345.tar" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/storage/actions/upload-software-update-file/invoke"
```

### Apply Software Update
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -H "Expect:" \
  -d '{ "mode": "Non-disruptive" }' \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/storage/actions/update-software/invoke"
```

---

## Snapshot Operations

### Create Snapshot
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -d '{
    "masterVolumeId": "b7582c29-db57-433e-9930-8afd89f1de8e"
}' \
  "https://192.168.181.120/ConfigurationManager/simple/v1/objects/volumes/actions/create-snapshot/invoke"
```

### Delete Snapshot
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Accept: application/json" \
  -H "Content-Type: application/json" \
  -d '{
    "snapshotVolumeId": "78025a99-1b5d-42d0-a257-09373fe5d8f3"
}' \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/volumes/actions/delete-snapshot/invoke"
```

### Restore Snapshot
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -d '{
    "masterVolumeId": "b7582c29-db57-433e-9930-8afd89f1de8e",
    "snapshotVolumeId": "e91daea3-08f2-457e-bcd0-dece69d73d78"
}' \
  "https://192.168.181.120/ConfigurationManager/simple/v1/objects/volumes/actions/restore-snapshot/invoke"
```

### Get Snapshot Information
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  "https://tevssb.ecoe.io/ConfigurationManager/simple/v1/objects/volumes/"
```

---

## Server Operations

### Get Servers
```bash
curl -k -X GET \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/servers"
```

### Get Servers (with Basic Auth)
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/servers"
```

### Get Server by ID
```bash
curl -k -X GET \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/servers/{{serverId}}"
```

### Create Server
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -d '{
    "serverNickname": "iqn.1994-05.com.redhat:4f9f75fac",
    "osType": "Linux",
    "vpsId": "system"
}' \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/servers"
```

### Delete Server
```bash
curl -k -X POST \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/servers/{{serverId}}"
```

### Get Server HBAs
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/servers/5bca8018-4a14-4aa2-ba4a-789ffea4fa35/hbas"
```

### Add Server HBA
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -d '{ "protocol": "iSCSI", "iscsiName": "iqn.1994-05.com.redhat:4f9f75fac"}' \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/servers/5bca8018-4a14-4aa2-ba4a-789ffea4fa35/hbas"
```

### Get Server Paths
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/servers/{{serverId}}/paths"
```

### Add Server Path
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -d '{
    "hbaId": "ef838a5a-4d07-483f-a82e-33a87c86faf8",
    "portId": "1f1c241e-c9dc-44d8-a028-2219b99f27fc"
}' \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/servers/5bca8018-4a14-4aa2-ba4a-789ffea4fa35/paths"
```

### Delete Server Path
```bash
curl -k -X DELETE \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/servers/{{serverId}}/paths/fa0e6f04-2009-4c97-9080-e336a3738178,7a32ad93-cfde-4493-83bd-4ad845235ce4"
```

---

## Port Operations

### Get Ports
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/ports"
```

---

## Drive Operations

### Get Drives
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/drives"
```

### Remove Drive
```bash
curl -k -X POST \
  -H "Authorization: Session {{token}}" \
  "https://{{bmserver}}/ConfigurationManager/simple/v1/objects/drives/197b416a-4826-418c-a1d6-7f083695104e/actions/remove/invoke"
```

### Suspend Drive Relocation
```bash
curl -k -X POST \
  -H "Content-Type: application/json" \
  -H "Expect:" \
  -H "Authorization: Session {{token}}" \
  -d '{"keyCode":"3PG94PTAZQNCHTKURLRMZFJIO76NXCR6L0FU9O3IXCR6L0FU9O3JXCR50FU9O3IXXD7FRJUVAVP"}' \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/protection-domains/d23bfce6-ea31-414e-8795-4c2c89409905/actions/suspend-drive-data-relocation/invoke"
```

### Resume Drive Relocation
```bash
curl -k -X POST \
  -H "Content-Type: application/json" \
  -H "Expect:" \
  -H "Authorization: Session {{token}}" \
  -d '{"keyCode":"3PG94PTAZQNCHTKURLRMZFJIO76NXCR6L0FU9O3IXCR6L0FU9O3JXCR50FU9O3IXXD7FRJUVAVP"}' \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/protection-domains/d23bfce6-ea31-414e-8795-4c2c89409905/actions/suspend-drive-data-relocation/invoke"
```

---

## Pool Operations

### Get Pools
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/pools"
```

### Expand Pool
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -H "Expect:" \
  -d '{
    "driveIds": [
        "0d543c2b-ab0a-43a5-bd7d-6baf20cb5a67",
        "122a6398-a9db-4ce2-b96a-2ab694b927ca",
        "1453458a-5f70-461e-b694-08e92f16b8cc"
    ]
}' \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/pools/16b01f77-73fa-4f4d-a24c-3a9cdc4b45a7/actions/expand/invoke"
```

---

## Storage Node Operations

### Get Capacity Balance
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/storage-node-capacity-settings"
```

### Set Capacity Balance
```bash
curl -k -X PATCH \
  -H "Authorization: Session {{token}}" \
  -H "Content-Type: application/json" \
  -d '{ "capacityBalancingSetting" :{ "isEnabled": false }}' \
  "https://{{bmserver}}/ConfigurationManager/simple/v1/objects/storage-node-capacity-settings/f0b71b7d-774d-4b3b-88da-016df12ad7c5"
```

### Get Storage Nodes
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/storage-nodes"
```

### Get Specific Storage Node
```bash
curl -k -X GET \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/storage-nodes/4bb4aec3-3f5d-4401-a451-49d6f99d635a"
```

### Add Storage Node
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Expect:" \
  -F "setupUserPassword={{password}}" \
  -F "configurationFile=@/path/to/SystemConfigurationFile.csv" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/storage-nodes"
```

### Add Spare Node
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -H "Expect:" \
  -d '{
    "faultDomainId": "f562460a-c0c5-4fa6-b102-2cb6ee1c89bc",
    "controlPortIpv4Address": "192.168.183.115",
    "setupUserPassword": "{{password}}",
    "bmcName": "192.168.183.105",
    "bmcUser": "{{bmcUser}}",
    "bmcPassword": "{{bmcPassword}}"
}' \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/spare-nodes"
```

### Get Spare Nodes
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Expect:" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/spare-nodes"
```

### Place Storage Node in Maintenance
```bash
curl -k -X POST \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/storage-nodes/029b12f6-a682-4623-8c69-822a791c4e7e/actions/block-for-maintenance/invoke"
```

### Restore Storage Node from Maintenance
```bash
curl -k -X POST \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/storage-nodes/029b12f6-a682-4623-8c69-822a791c4e7e/actions/recover/invoke"
```

### Replace Storage Node
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  -H "Content-Type: application/json" \
  -d '{
    "setupUserPassword":"{{password}}"
}' \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/storage-nodes/{{storage_node}}/actions/replace/invoke"
```

### Get Storage Master Node Primary Flag
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  "https://{{server}}/ConfigurationManager/simple/configuration/storage-master-node-primary-flag"
```

---

## Volume Operations

### Get Volumes
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/volumes/43059b3d-797f-44ac-b5ec-e773a45bdd14"
```

### Create Volume on Storage Controller
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -H "Expect:" \
  -d '{ 
    "capacity":3957320, 
    "nicknameParam":{ "baseName": "dbvol1" },
    "poolId":"59ce830b-07c7-4dd6-a7ba-9e85c7af4eba", 
    "storageControllerId": "02381a4c-dafb-4f6b-85d6-f8bce92a428a" 
}' \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/volumes"
```

### Create Volume with Server Connections
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -H "Expect:" \
  -d '{ 
    "capacity":3957320, 
    "nicknameParam":{ "baseName": "dbvol1" },
    "poolId":"59ce830b-07c7-4dd6-a7ba-9e85c7af4eba", 
    "storageControllerId": "02381a4c-dafb-4f6b-85d6-f8bce92a428a" 
}' \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/volumes"
```

### Delete Volume
```bash
curl -k -X DELETE \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -H "Expect:" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/volumes/{{volumeId}}"
```

---

## User Operations

### Get User Groups
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/user-groups"
```

### Delete User Group
```bash
curl -k -X DELETE \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/user-groups/jpmcusers"
```

### Get External Authentication Server Settings
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/external-auth-server-setting"
```

### Upload AD Root Certificate
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  -F "rootCertificate=@/path/to/cacert.pem" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/external-auth-server-root-certificates/primary1/actions/import/invoke"
```

### Get Users
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/users"
```

### Get User Authentication Settings
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/user-auth-setting"
```

### Add User to Groups
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  -H "Content-Type: application/json" \
  -d '{ "userGroupIds":["SystemAdministrators"] }' \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/users/openshift/actions/add-user-group/invoke"
```

### Set External Authentication Server
```bash
curl -k -X PATCH \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  -H "Content-Type: application/json" \
  -d '{
    "isEnabled": true,
    "authProtocol": "LDAP",
    "ldapSetting": {
        "mappingMode": "Group",
        "primaryLdapServerUrl": "ldap://192.168.183.121:636",
        "secondaryLdapServerUrl": "",
        "isStartTlsEnabled": false,
        "baseDn": "DC=ecoe,DC=local",
        "bindDn": "CN=JPMC Service Account,CN=Users,DC=ecoe,DC=local",
        "bindDnPassword": "{{bindDnPassword}}",
        "userIdAttribute": "sAMAccountName",
        "userTreeDn": "CN=Users,DC=acoe,DC=local",
        "userObjectClass": "user",
        "userGroupIdAttribute": "sAMAccountName",
        "userGroupTreeDn": "CN=te-vssbusers,DC=ecoe,DC=local",
        "userGroupObjectClass": "Group"
    }
}' \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/external-auth-server-setting"
```

### Set User Authentication Settings
```bash
curl -k -X PATCH \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -H "Expect:" \
  -d '{
    "passwordComplexitySetting": {
        "minLength": 4,
        "minNumberOfUpperCaseChars": 0,
        "minNumberOfLowerCaseChars": 0,
        "minNumberOfNumerals": 0,
        "minNumberOfSymbols": 0,
        "numberOfPasswordHistory": 1
    },
    "passwordAgeSetting": {
        "requiresInitialPasswordReset": false,
        "minAgeDays": 0,
        "maxAgeDays": 0
    },
    "lockoutSetting": {
        "maxAttempts": 3,
        "lockoutSeconds": 60
    },
    "sessionSetting": {
        "maxLifetimeSeconds": 86400,
        "maxIdleSeconds": 1800
    }
}' \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/user-auth-setting"
```

### Create User
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  -H "Content-Type: application/json" \
  -d '{ "userId":"FrankHayer", "password":"{{password}}", "userGroupIds":["SystemAdministrators"] }' \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/users"
```

### Delete User
```bash
curl -k -X DELETE \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  -H "Content-Type: application/json" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/users/{{vpsUser}}"
```

### Change User Password
```bash
curl -k -X PATCH \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  -H "Content-Type: application/json" \
  -d '{"currentPassword":"{{currentPassword}}", "newPassword":"{{newPassword}}"}' \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/users/admin/password"
```

### Reset Expired User Password
```bash
curl -k -X PATCH \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  -H "Content-Type: application/json" \
  -d '{"currentPassword":"{{currentPassword}}", "newPassword":"{{newPassword}}"}' \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/users/admin/password"
```

---

## VPS Operations

### Get VPS
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/virtual-private-storages"
```

### Get VPS Details
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/virtual-private-storages/{{vps}}"
```

### Patch VPS
```bash
curl -k -X PATCH \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -d '{
    "upperLimitForCapacityOfVolumes": 1000000
}' \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/virtual-private-storages/{{vps}}"
```

### Create VPS
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "VPS_01",
    "upperLimitForNumberOfServers": 100,
    "volumeSettings": [
        {
            "poolId": "{{poolId}}",
            "upperLimitForCapacityOfVolumes": 100,
            "upperLimitForNumberOfVolumes": 50,
            "upperLimitForCapacityOfSingleVolume": -1,
            "upperLimitForIopsOfVolume": -1,
            "upperLimitForTransferRateOfVolume": -1,
            "upperAlertAllowableTimeOfVolume": -1
        }
    ]
}' \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/virtual-private-storages"
```

### Delete VPS
```bash
curl -k -X DELETE \
  -u "{{username}}:{{password}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/virtual-private-storages/{{vips}}"
```

### Add VPS to User Group
```bash
curl -k -X PATCH \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -H "Expect:" \
  -d '{
    "scope": [
        "system",
        "{{vps}}",
        "{{vps02}}"
    ]
}' \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/user-groups/{{group}}"
```

### Create User Group for VPS
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -H "Expect:" \
  -d '{
    "userGroupId": "{{vpsGroup02}}",
    "roleNames": [
        "VpsSecurity",
        "VpsStorage",
        "VpsMonitor"
    ],
    "vpsId": "{{vps02}}",
    "scope": [
        "{{vps02}}"
    ]
}' \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/user-groups"
```

### Create User for VPS
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -H "Expect:" \
  -d '{ "userId":"{{vpsUsername}}", "password":"{{vpsPassword}}", "userGroupIds":["{{vpsGroup02}}"] }' \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/users"
```

### Create Volume on VPS
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -H "Expect:" \
  -d '{ 
    "capacity":3957320, 
    "nicknameParam":{ "baseName": "dbvol1" },
    "poolId":"59ce830b-07c7-4dd6-a7ba-9e85c7af4eba", 
    "storageControllerId": "02381a4c-dafb-4f6b-85d6-f8bce92a428a" 
}' \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/volumes"
```

### Change VPS Admin Password
```bash
curl -k -X PATCH \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  -H "Content-Type: application/json" \
  -d '{"currentPassword":"{{currentPassword}}", "newPassword":"{{newPassword}}"}' \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/users/admin/password"
```

---

## Cluster Operations

### Get Storage Controllers
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/storage-controllers"
```

### Get Software Update File
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/storage/software-update-file"
```

### Get Fault Sets
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/fault-sets"
```

### Get Fault Domains
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/fault-domains"
```

### Get Protection Domains (Volumes)
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/volumes"
```

### Get Storage Cluster ID
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/storage"
```

### Get Dump Status
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/dump-status"
```

### Download Dump File
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/dump-file/download"
```

### Create Dump File
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Authorization: Session {{token}}" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/dump-file/actions/create-file/invoke"
```

### Upload System Configuration File
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: multipart/form-data" \
  -H "Expect:" \
  -F "systemRequirementsFile=@/path/to/SystemConfigurationFile.csv" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/system-requirements-file/actions/import/invoke"
```

### Create System Configuration File
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Length: 0" \
  -H "Accept: application/json" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/configuration-file/actions/create/invoke"
```

### Download System Configuration File
```bash
curl -k -X GET \
  -u "{{username}}:{{password}}" \
  -H "Content-Length: 0" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/configuration-file/download"
```

### Upload Software Update
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: multipart/form-data" \
  -H "Expect:" \
  -F "softwareUpdateFile=@/path/to/hsds-update-01150040-0212.tar" \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/storage/actions/upload-software-update-file/invoke"
```

### Invoke Software Update
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "Content-Type: application/json" \
  -d '{
    "mode": "Non-disruptive"
}' \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/storage/actions/update-software/invoke"
```

### Transfer Software Update File
```bash
curl -k -X POST \
  -u "{{username}}:{{password}}" \
  -H "content-type: multipart/form-data" \
  -H "Expect:" \
  -H "Authorization: Session {{token}}" \
  -F "softwareUpdateFile=@/home/user/update/hsds-update-01050000-2345.tar" \
  "https://{{server}}/ConfigurationManager/simple/v1/objects/storage/actions/upload-software-update-file/invoke"
```

---

## Encryption Settings

### Enable Encryption Environment
```bash
curl -k -X PATCH \
  -u "{{username}}:{{password}}" \
  -H "Accept: application/json" \
  -H "Content-Type: application/json" \
  -d '{
    "isEnabled": true
}' \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/encryption-settings"
```

### Enable Pool Encryption
```bash
curl -k -X PATCH \
  -u "{{username}}:{{password}}" \
  -H "Accept: application/json" \
  -H "Content-Type: application/json" \
  -d '{
    "isEnabled": true
}' \
  "https://192.168.183.121/ConfigurationManager/simple/v1/objects/encryption-settings"
```

---

## Notes

- The `-k` flag is used to skip SSL certificate verification (for self-signed certificates)
- Replace all `{{variable}}` placeholders with actual values
- Session tokens can be obtained from the "Get Session Token" endpoint and used in subsequent requests
- Some endpoints support both Basic Authentication (`-u username:password`) and Session Authentication (`-H "Authorization: Session {{token}}"`)
