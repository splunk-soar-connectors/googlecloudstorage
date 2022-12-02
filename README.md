[comment]: # "Auto-generated SOAR connector documentation"
# Google Cloud Storage

Publisher: Splunk Community  
Connector Version: 1\.0\.5  
Product Vendor: Google  
Product Name: Cloud Storage  
Product Version Supported (regex): "\.\*"  
Minimum Product Version: 5\.3\.5  

This app integrates with Google Cloud Storage API to support various investigative and generic actions

[comment]: # " File: README.md"
[comment]: # "  Copyright (c) 2021-2022 Splunk Inc."
[comment]: # ""
[comment]: # "  Licensed under the Apache License, Version 2.0 (the 'License');"
[comment]: # "  you may not use this file except in compliance with the License."
[comment]: # "  You may obtain a copy of the License at"
[comment]: # ""
[comment]: # "      http://www.apache.org/licenses/LICENSE-2.0"
[comment]: # ""
[comment]: # "  Unless required by applicable law or agreed to in writing, software distributed under"
[comment]: # "  the License is distributed on an 'AS IS' BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,"
[comment]: # "  either express or implied. See the License for the specific language governing permissions"
[comment]: # "  and limitations under the License."
[comment]: # ""
Actions in this app utilize the following API: https://cloud.google.com/storage/docs/json_api

## Explanation of Asset Configuration Parameters

The asset configuration parameters affect \[test connectivity\] and all the other actions of the
application. Below are the explanation and usage of all those parameters.

-   **Contents of Service Account JSON file -** After creating a Service Account for authenticating
    with Google Cloud Storage (https://console.cloud.google.com/iam-admin/serviceaccounts/project),
    the file can be downloaded. Paste the contents into the asset configuration input as-is.
-   **Project ID -** The Google Cloud Project ID.


### Configuration Variables
The below configuration variables are required for this Connector to operate.  These variables are specified when configuring a Cloud Storage asset in SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**key\_json** |  required  | password | Contents of Service Account JSON file
**project** |  required  | string | Project ID

### Supported Actions  
[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration  
[delete object](#action-delete-object) - Deletes object from a bucket  
[list objects](#action-list-objects) - Retrieves a list of objects matching the criteria from the bucket  
[get object](#action-get-object) - Retrieves object metadata and optionally downloads contents to vault  
[create object](#action-create-object) - Creates object in a given bucket  
[describe bucket](#action-describe-bucket) - Get information about a bucket  
[list buckets](#action-list-buckets) - Retrieves a list of buckets for the configured project  
[create bucket](#action-create-bucket) - Create a new bucket  

## action: 'test connectivity'
Validate the asset configuration for connectivity using supplied configuration

Type: **test**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
No Output  

## action: 'delete object'
Deletes object from a bucket

Type: **generic**  
Read only: **False**

Deletes an object and its metadata\. Deletions are permanent if versioning is not enabled for the bucket\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**bucket** |  required  | Name of the bucket | string |  `gcloud storage bucket` 
**object** |  required  | Name of the object | string |  `gcloud storage object` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.object | string |  `gcloud storage object` 
action\_result\.parameter\.bucket | string |  `gcloud storage bucket` 
action\_result\.data | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list objects'
Retrieves a list of objects matching the criteria from the bucket

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**bucket** |  required  | Name of the bucket | string |  `gcloud storage bucket` 
**prefix** |  optional  | Filter objects returned by prefix | string | 
**max\_objects** |  optional  | Maximum number of objects to list | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.bucket | string |  `gcloud storage bucket` 
action\_result\.parameter\.prefix | string | 
action\_result\.parameter\.max\_objects | numeric | 
action\_result\.data\.0\.items\.\*\.name | string | 
action\_result\.data\.0\.items\.\*\.timeCreated | string | 
action\_result\.data\.0\.items\.\*\.storageClass | string | 
action\_result\.data\.0\.items\.\*\.md5Hash | string | 
action\_result\.data\.0\.items\.\*\.bucket | string | 
action\_result\.data\.0\.items\.\*\.updated | string | 
action\_result\.data\.0\.items\.\*\.crc32c | string | 
action\_result\.data\.0\.items\.\*\.mediaLink | string | 
action\_result\.data\.0\.items\.\*\.timeStorageClassUpdated | string | 
action\_result\.data\.0\.items\.\*\.id | string | 
action\_result\.data\.0\.items\.\*\.size | numeric | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
action\_result\.summary\.num\_objects | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get object'
Retrieves object metadata and optionally downloads contents to vault

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**object** |  required  | Name of the object | string |  `gcloud storage object` 
**bucket** |  required  | Name of the bucket | string |  `gcloud storage bucket` 
**download\_file** |  optional  | Whether or not to download the file contents to vault | boolean | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.object | string |  `gcloud storage object` 
action\_result\.parameter\.bucket | string |  `gcloud storage bucket` 
action\_result\.parameter\.download\_file | boolean | 
action\_result\.data\.0\.name | string | 
action\_result\.data\.0\.timeCreated | string | 
action\_result\.data\.0\.storageClass | string | 
action\_result\.data\.0\.md5Hash | string | 
action\_result\.data\.0\.bucket | string | 
action\_result\.data\.0\.updated | string | 
action\_result\.data\.0\.crc32c | string | 
action\_result\.data\.0\.mediaLink | string | 
action\_result\.data\.0\.timeStorageClassUpdated | string | 
action\_result\.data\.0\.id | string | 
action\_result\.data\.0\.size | numeric | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'create object'
Creates object in a given bucket

Type: **generic**  
Read only: **False**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**bucket** |  required  | Name of the bucket | string |  `gcloud storage bucket` 
**vault\_id** |  required  | Vault ID of the file to upload | string |  `vault id` 
**path** |  optional  | Path in the bucket where to place the object | string |  `file path` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.path | string |  `file path` 
action\_result\.parameter\.bucket | string |  `gcloud storage bucket` 
action\_result\.parameter\.vault\_id | string |  `vault id` 
action\_result\.data\.0\.name | string | 
action\_result\.data\.0\.timeCreated | string | 
action\_result\.data\.0\.storageClass | string | 
action\_result\.data\.0\.md5Hash | string | 
action\_result\.data\.0\.bucket | string | 
action\_result\.data\.0\.updated | string | 
action\_result\.data\.0\.crc32c | string | 
action\_result\.data\.0\.mediaLink | string | 
action\_result\.data\.0\.timeStorageClassUpdated | string | 
action\_result\.data\.0\.id | string | 
action\_result\.data\.0\.size | numeric | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'describe bucket'
Get information about a bucket

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**bucket** |  required  | Name of the bucket | string |  `gcloud storage bucket` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.bucket | string |  `gcloud storage bucket` 
action\_result\.data\.0\.name | string | 
action\_result\.data\.0\.timeCreated | string | 
action\_result\.data\.0\.updated | string | 
action\_result\.data\.0\.locationType | string | 
action\_result\.data\.0\.projectNumber | string | 
action\_result\.data\.0\.location | string | 
action\_result\.data\.0\.id | string | 
action\_result\.data\.0\.selfLink | string | 
action\_result\.data\.0\.storageClass | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list buckets'
Retrieves a list of buckets for the configured project

Type: **investigate**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.data\.0\.name | string | 
action\_result\.data\.0\.items\.\*\.timeCreated | string | 
action\_result\.data\.0\.items\.\*\.updated | string | 
action\_result\.data\.0\.items\.\*\.locationType | string | 
action\_result\.data\.0\.items\.\*\.projectNumber | string | 
action\_result\.data\.0\.items\.\*\.location | string | 
action\_result\.data\.0\.items\.\*\.id | string | 
action\_result\.data\.0\.items\.\*\.selfLink | string | 
action\_result\.data\.0\.items\.\*\.storageClass | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
action\_result\.summary\.total\_objects | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'create bucket'
Create a new bucket

Type: **generic**  
Read only: **False**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**bucket** |  required  | Name of the bucket | string |  `gcloud storage bucket` 
**location** |  required  | Location where to create the bucket | string |  `gcloud storage location` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.bucket | string |  `gcloud storage bucket` 
action\_result\.parameter\.location | string |  `gcloud storage location` 
action\_result\.data\.0\.name | string | 
action\_result\.data\.0\.timeCreated | string | 
action\_result\.data\.0\.updated | string | 
action\_result\.data\.0\.locationType | string | 
action\_result\.data\.0\.projectNumber | string | 
action\_result\.data\.0\.location | string | 
action\_result\.data\.0\.id | string | 
action\_result\.data\.0\.selfLink | string | 
action\_result\.data\.0\.storageClass | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric | 