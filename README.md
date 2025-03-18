# Google Cloud Storage

Publisher: Splunk Community \
Connector Version: 1.0.5 \
Product Vendor: Google \
Product Name: Cloud Storage \
Minimum Product Version: 5.3.5

This app integrates with Google Cloud Storage API to support various investigative and generic actions

### Configuration variables

This table lists the configuration variables required to operate Google Cloud Storage. These variables are specified when configuring a Cloud Storage asset in Splunk SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**key_json** | required | password | Contents of Service Account JSON file |
**project** | required | string | Project ID |

### Supported Actions

[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration \
[delete object](#action-delete-object) - Deletes object from a bucket \
[list objects](#action-list-objects) - Retrieves a list of objects matching the criteria from the bucket \
[get object](#action-get-object) - Retrieves object metadata and optionally downloads contents to vault \
[create object](#action-create-object) - Creates object in a given bucket \
[describe bucket](#action-describe-bucket) - Get information about a bucket \
[list buckets](#action-list-buckets) - Retrieves a list of buckets for the configured project \
[create bucket](#action-create-bucket) - Create a new bucket

## action: 'test connectivity'

Validate the asset configuration for connectivity using supplied configuration

Type: **test** \
Read only: **True**

#### Action Parameters

No parameters are required for this action

#### Action Output

No Output

## action: 'delete object'

Deletes object from a bucket

Type: **generic** \
Read only: **False**

Deletes an object and its metadata. Deletions are permanent if versioning is not enabled for the bucket.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**bucket** | required | Name of the bucket | string | `gcloud storage bucket` |
**object** | required | Name of the object | string | `gcloud storage object` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.object | string | `gcloud storage object` | |
action_result.parameter.bucket | string | `gcloud storage bucket` | |
action_result.data | string | | |
action_result.status | string | | success failed |
action_result.message | string | | |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'list objects'

Retrieves a list of objects matching the criteria from the bucket

Type: **investigate** \
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**bucket** | required | Name of the bucket | string | `gcloud storage bucket` |
**prefix** | optional | Filter objects returned by prefix | string | |
**max_objects** | optional | Maximum number of objects to list | numeric | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.bucket | string | `gcloud storage bucket` | |
action_result.parameter.prefix | string | | |
action_result.parameter.max_objects | numeric | | |
action_result.data.0.items.\*.name | string | | |
action_result.data.0.items.\*.timeCreated | string | | 2020-07-14T11:13:15.950Z |
action_result.data.0.items.\*.storageClass | string | | STANDARD |
action_result.data.0.items.\*.md5Hash | string | | |
action_result.data.0.items.\*.bucket | string | | |
action_result.data.0.items.\*.updated | string | | 2020-07-14T11:13:15.950Z |
action_result.data.0.items.\*.crc32c | string | | |
action_result.data.0.items.\*.mediaLink | string | | |
action_result.data.0.items.\*.timeStorageClassUpdated | string | | 2020-07-14T11:13:15.950Z |
action_result.data.0.items.\*.id | string | | |
action_result.data.0.items.\*.size | numeric | | 41432 |
action_result.status | string | | success failed |
action_result.message | string | | |
action_result.summary | string | | |
action_result.summary.num_objects | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get object'

Retrieves object metadata and optionally downloads contents to vault

Type: **investigate** \
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**object** | required | Name of the object | string | `gcloud storage object` |
**bucket** | required | Name of the bucket | string | `gcloud storage bucket` |
**download_file** | optional | Whether or not to download the file contents to vault | boolean | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.object | string | `gcloud storage object` | |
action_result.parameter.bucket | string | `gcloud storage bucket` | |
action_result.parameter.download_file | boolean | | |
action_result.data.0.name | string | | |
action_result.data.0.timeCreated | string | | 2020-07-14T11:13:15.950Z |
action_result.data.0.storageClass | string | | STANDARD |
action_result.data.0.md5Hash | string | | |
action_result.data.0.bucket | string | | |
action_result.data.0.updated | string | | 2020-07-14T11:13:15.950Z |
action_result.data.0.crc32c | string | | |
action_result.data.0.mediaLink | string | | |
action_result.data.0.timeStorageClassUpdated | string | | 2020-07-14T11:13:15.950Z |
action_result.data.0.id | string | | |
action_result.data.0.size | numeric | | 41432 |
action_result.status | string | | success failed |
action_result.message | string | | |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'create object'

Creates object in a given bucket

Type: **generic** \
Read only: **False**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**bucket** | required | Name of the bucket | string | `gcloud storage bucket` |
**vault_id** | required | Vault ID of the file to upload | string | `vault id` |
**path** | optional | Path in the bucket where to place the object | string | `file path` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.path | string | `file path` | |
action_result.parameter.bucket | string | `gcloud storage bucket` | |
action_result.parameter.vault_id | string | `vault id` | |
action_result.data.0.name | string | | |
action_result.data.0.timeCreated | string | | 2020-07-14T11:13:15.950Z |
action_result.data.0.storageClass | string | | STANDARD |
action_result.data.0.md5Hash | string | | |
action_result.data.0.bucket | string | | |
action_result.data.0.updated | string | | 2020-07-14T11:13:15.950Z |
action_result.data.0.crc32c | string | | |
action_result.data.0.mediaLink | string | | |
action_result.data.0.timeStorageClassUpdated | string | | 2020-07-14T11:13:15.950Z |
action_result.data.0.id | string | | |
action_result.data.0.size | numeric | | 41432 |
action_result.status | string | | success failed |
action_result.message | string | | |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'describe bucket'

Get information about a bucket

Type: **investigate** \
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**bucket** | required | Name of the bucket | string | `gcloud storage bucket` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.bucket | string | `gcloud storage bucket` | |
action_result.data.0.name | string | | |
action_result.data.0.timeCreated | string | | 2020-07-14T11:13:15.950Z |
action_result.data.0.updated | string | | 2020-07-14T11:13:15.950Z |
action_result.data.0.locationType | string | | multi-region |
action_result.data.0.projectNumber | string | | |
action_result.data.0.location | string | | US |
action_result.data.0.id | string | | |
action_result.data.0.selfLink | string | | https://www.googleapis.com/storage/v1/b/XXXXXXXX |
action_result.data.0.storageClass | string | | STANDARD |
action_result.status | string | | success failed |
action_result.message | string | | |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'list buckets'

Retrieves a list of buckets for the configured project

Type: **investigate** \
Read only: **True**

#### Action Parameters

No parameters are required for this action

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.data.0.name | string | | |
action_result.data.0.items.\*.timeCreated | string | | 2020-07-14T11:13:15.950Z |
action_result.data.0.items.\*.updated | string | | 2020-07-14T11:13:15.950Z |
action_result.data.0.items.\*.locationType | string | | multi-region |
action_result.data.0.items.\*.projectNumber | string | | |
action_result.data.0.items.\*.location | string | | US |
action_result.data.0.items.\*.id | string | | |
action_result.data.0.items.\*.selfLink | string | | https://www.googleapis.com/storage/v1/b/XXXXXXXX |
action_result.data.0.items.\*.storageClass | string | | STANDARD |
action_result.status | string | | success failed |
action_result.message | string | | |
action_result.summary | string | | |
action_result.summary.total_objects | numeric | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'create bucket'

Create a new bucket

Type: **generic** \
Read only: **False**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**bucket** | required | Name of the bucket | string | `gcloud storage bucket` |
**location** | required | Location where to create the bucket | string | `gcloud storage location` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.bucket | string | `gcloud storage bucket` | |
action_result.parameter.location | string | `gcloud storage location` | |
action_result.data.0.name | string | | |
action_result.data.0.timeCreated | string | | 2020-07-14T11:13:15.950Z |
action_result.data.0.updated | string | | 2020-07-14T11:13:15.950Z |
action_result.data.0.locationType | string | | multi-region |
action_result.data.0.projectNumber | string | | |
action_result.data.0.location | string | | US US-EAST1 |
action_result.data.0.id | string | | |
action_result.data.0.selfLink | string | | https://www.googleapis.com/storage/v1/b/XXXXXXXX |
action_result.data.0.storageClass | string | | STANDARD |
action_result.status | string | | success failed |
action_result.message | string | | |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

______________________________________________________________________

Auto-generated Splunk SOAR Connector documentation.

Copyright 2025 Splunk Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and limitations under the License.
