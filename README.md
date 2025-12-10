# Backend endpoints documentation
- [Auth](#auth-endpoint) <br>
- [Users](#users-endpoint) <br>
- [Workspaces](#workspaces-endpoint) <br>
- [Invites](#invites) <br>
- [Research Papers](#research-papers-endpoint) <br>
- [AI](#ai-endpoint) <br>
- [Search](#search-endpoint)
- [PDF](#pdf-endpoint)



## Auth endpoint

#### Log Out

HTTP Method: DELETE <br>
API endpoint: `/auth/logout` <br> 

#### Request for new access token

HTTP Method: POST <br>
API endpoint: `/auth/token` <br> 

<br><br>




## Users endpoint
#### User details
HTTP Method: GET <br>
API endpoint: `/users/me` <br> 

JSON payload (response):
```
{
    "Id": number,
    "UserName": string,
    "FullName": string,
    "Email": string
}
```


#### Delete user account
HTTP Method: DELETE <br>
API endpoint: `/users/me` <br> 

<br><br>




## Workspaces endpoint
#### Create new workspace
HTTP Method: POST <br>
API endpoint: `/workspaces`

JSON payload (request):
```
{
    "workspaceName": string,
    "dateCreated": string
}
```
> [!NOTE]
> Date format is: yyyy-mm-dd


#### Get all user's owned workspaces
HTTP Method: GET <br>
API endpoint: `/workspaces/owned`

JSON payload (response):
```
[
    {
        "Id": number,
        "Name": string,
        "DateCreated": string
    }
]
```

#### Get the workspaces shared by other users
HTTP Method: GET <br>
API endpoint: `/workspaces/shared`

JSON payload (response):
```
[
    {
        "Id": number,
        "Name": string,
        "DateCreated": string,
        "OwnerName": string
    }
]
```

#### Leave a shared workspace
HTTP Method: DELETE <br>
API endpoint: `/workspaces/:workspaceId/shared/leave`

> [!IMPORTANT]
> Only users in a shared workspace whose role is "Member" can leave the workspace

#### Get the individual workspace details
HTTP Method: GET <br>
API endpoint: `/workspaces/:workspaceId`

JSON payload (response):
```
{
    "Id": number,
    "Name": string,
    "DateCreated": string
}
```

#### Get all the users in a workspace
HTTP Method: GET <br>
API endpoint: `/workspaces/:workspaceId/users`

```
[
    {
        "UserName": string,
        "Role": string
    }
]
```

#### Delete a workspace
HTTP Method: DELETE <br>
API endpoint: `/workspaces/:workspaceId`

> [!IMPORTANT]
> Only users who created the workspace can delete it

#### Update Workspace Name
HTTP Method: PUT <br>
API endpoint: `/workspaces/:workspaceId`

JSON payload (request):
```
{
    "newWorkspaceName": string
}
```


<br><br>


## Invites
#### Search for a user (for inviting into a workspace)
HTTP Method: GET <br>
API endpoint: `/users/:userName` <br>

JSON payload (response):
```
[
    {
        "Id": number,
        "UserName": string
    }
]
```
#### Invite a user to a workspace
HTTP Method: POST <br>
API endpoint: `/invites` <br>

JSON payload (request):
```
{
    "dateSent": string,
    "targetUserId": number,
    "workspaceId ": number
}
```
> [!NOTE]
> Date format is: yyyy-mm-dd

#### See all invitations the user sent to others
HTTP Method: GET <br>
API endpoint: `/invites/sent` <br>

JSON payload (response):
```
{
    "Id": number,
    "DateSent": string,
    "TargetUserName": string,
    "WorkspaceId ": number
}
```

#### See all invitations sent by other users
HTTP Method: GET <br>
API endpoint: `/invites/fromOthers` <br>

JSON payload (response):
```
{
    "Id": number,
    "DateSent": string,
    "RequesterUserName": string,
    "WorkspaceId ": number
}
```

#### Delete invites to other users / Reject invites from other users
HTTP Method: DELETE <br>
API endpoint: `/invites/:invitationId` <br>

#### Accept workspace invitation
HTTP Method: POST <br>
API endpoint: `/invites/accept` <br>
```
{
    "workspaceId": number,
    "invitationId": number
}
```

<br><br>





## Research Papers endpoint
#### All Research papers
HTTP Method: GET <br>
API endpoint: `/workspaces/:workspaceId/researchPapers` <br> 

JSON payload (response):
```
[
    {
        "majorObjective": string,
        "methods": {
            "researchDesign": string,
            "localeOfTheStudy": string,
            "informantsOfTheStudy": string,
            "dataGatheringProcedure": string,
            "dataAnalysis": string
        },
        "majorFindings": string,
        "apa": string,
        "ieee": string,
        "pdfKey": string,
        "pdfName": string
    }
]

```
#### Create new Research paper
HTTP Method: POST <br>
API endpoint: `/workspaces/:workspaceId/researchPapers` <br> 

JSON payload (request):
```
{
    "majorObjective": string,
    "methods": {
        "researchDesign": string,
        "localeOfTheStudy": string,
        "informantsOfTheStudy": string,
        "dataGatheringProcedure": string,
        "dataAnalysis": string
    },
    "majorFindings": string,
    "apa": string,
    "ieee": string,
    "pdfKey": string,
    "pdfName": string, 
    "pdfHash": string
}
```
#### Update Research paper column
HTTP Method: PUT <br>
API endpoint: `/researchPapers/:researchPaperId` <br> 

JSON payload (request):
```
{
    "columnName": string,
    "value": string
}
```

Editable Research paper columns are: 
- MajorObjective
- Methods
- MajorFindings


> [!NOTE]
> "columnName" = column of research paper in the database <br>
> "value" = updated value of the column to be pushed to the database

#### Delete Research paper
HTTP Method: DELETE <br>
API endpoint: `/researchPapers/:researchPaperId` <br> 


<br><br>


## AI endpoint

#### Extract Lit matrix table
HTTP Method: POST <br>
API endpoint: `/ai/extract/:workspaceId` <br>

JSON payload (request):
```
{
    PDF files
}
```
> [!IMPORTANT]
> Should contain 1 - 3 PDF files. (File limit is set to 1 during development) <br>
> Max file size of an individual file is 10 mb.

JSON payload (response):
```
[
    {
        "majorObjective": string,
        "methods": {
            "researchDesign": string,
            "localeOfTheStudy": string,
            "informantsOfTheStudy": string,
            "dataGatheringProcedure": string,
            "dataAnalysis": string
        },
        "majorFindings": string,
        "apa": string,
        "ieee": string,
        "pdfKey": string,
        "pdfName": string,
        "pdfHash": string
    }
]
```
> [!NOTE]
> Properties: `pdfKey`, `pdfName` and `pdfHash` is not generated by AI. <br>
> They are metadata for storing of pdf files in the Digital Ocean object storage.

#### Possible error responses by the server:

```
status: 400 | message: [MULTER ERROR]: Too many files
- Files sent are greater than 4.

status: 400 | message: [MULTER ERROR]: File too large
- One of the file sent is too large. 

status: 400 | message: <file name> cannot be read. Either remove it or replace it with a new one.
- One of the file's contents cannot be read, thus cannot be used with the AI model. 

status: 400 | message: The extracted details of the file you sent is already in this workspace.
- The file sent is already extracted and saved in the workspace
```


<br> <br>




## Search endpoint
#### Get research papers using SerpAPI
HTTP Method: GET <br>
API endpoint: `/search/papers?q={encodeURIComponent(queryValue)}&offset={encodeURIComponent(offsetValue)}` <br>



JSON payload (response):
```
{
    "organic_results": [
        {
            "title": string,
            "snippet": string,
            "link": string,
            "publication_info": {
                "summary": string
            },
            "resources": [ 
                {
                    "title": string,
                    "file_format": string,
                    "link": string
                }
            ]
        }
    ]

}
```
<img width="1602" height="621" alt="Image" src="https://github.com/user-attachments/assets/fa8c09d5-b4e9-413f-8727-0e2eb7028892" /> <br>

> [!IMPORTANT]
> Not all organic result objects have the resources array 

> [!NOTE]
> offset: 0 is equal to the 1st page in the pagination, offset: 10 is the 2nd page, offset: 20 is the 3rd page, etc. <br>
> each offset has 10 research papers


| offset value | pagination/page |
| --- | --- |
| 0 | 1 |
| 10 | 2 |
| 20 | 3 |
| 30 | 4 |
| 40 | 5 |
| 50 | 6 |

<br><br>

## PDF endpoint
#### Get view link
HTTP Method: GET <br>
API endpoint: `/pdf/viewUrl?pdfKey=value` <br>

JSON payload (response): 
```
PDF view link
```

#### Get download link
HTTP Method: GET <br>
API endpoint: `/pdf/downloadUrl?pdfKey=value&pdfName=value` <br>

JSON payload (response): 
```
PDF download link
```

#### Delete PDF
HTTP Method: DELETE <br>
API endpoint: `/pdf/:pdfKey` <br>
