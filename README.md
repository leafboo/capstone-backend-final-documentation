# Backend endpoints documentation
- [Auth](#auth-endpoint) <br>
- [Users](#users-endpoint) <br>
- [Workspaces](#workspaces-endpoint) <br>
- [Research Papers](#research-papers-endpoint) <br>
- [AI](#ai-endpoint) <br>
- [Search](#search-endpoint)
- [PDF](#pdf-endpoint)



## Auth endpoint
#### Log In 

HTTP Method: POST <br>
API endpoint: `/auth/login` <br> 

JSON payload (request):
```
{
    "userName": string,
    "password": string
}
```

#### Log Out

HTTP Method: DELETE <br>
API endpoint: `/auth/logout` <br> 

#### Request for new access token

HTTP Method: POST <br>
API endpoint: `/auth/token` <br> 

<br><br>




## Users endpoint
#### Signup

HTTP Method: POST <br>
API endpoint: `/users` <br> 

JSON payload (request):
```
{
    "userName": string,
    "email": string,
    "password": string
}
```
#### User details
HTTP Method: GET <br>
API endpoint: `/users/me` <br> 

JSON payload (response):
```
{
    "Id": number,
    "UserName": string,
    "Email": string
}
```
#### Update user password
HTTP Method: PUT <br>
API endpoint: `/users/me/password` <br> 

JSON payload (request):
```
{
    "oldPassword": string,
    "newPassword": string
}
```
#### Delete user account
HTTP Method: DELETE <br>
API endpoint: `/users/me` <br> 

<br><br>




## Workspaces endpoint
#### All Workspaces
HTTP Method: GET <br>
API endpoint: `/workspaces` <br> 

JSON payload (response):
```
{
    "Id": number,
    "Name": string,
    "DateCreated": string
}
```
#### Workspace
HTTP Method: GET <br>
API endpoint: `/workspaces/:workspaceId` <br> 

JSON payload (response):
```
{
    "Id": number,
    "Name": string,
    "DateCreated": string
}
```
#### Create new Workspace
HTTP Method: POST <br>
API endpoint: `/workspaces` <br> 

JSON payload (request):
```
{
    "workspaceName": string,
    "dateCreated": string
}
```

#### Update Workspace Name
HTTP Method: PUT <br>
API endpoint: `/workspaces/:workspaceId`

JSON payload (request):
```
{
    "newWorkspaceName": string
}
```

#### Delete Workspace
HTTP Method: DELETE <br>
API endpoint: `/workspaces/:workspaceId`


<br><br>




## Research Papers endpoint
#### All Reseach papers
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
            "dataGatheringProcedure": string
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
        "dataGatheringProcedure": string
    },
    "majorFindings": string,
    "apa": string,
    "ieee": string,
    "pdfKey": string,
    "pdfName": string
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
API endpoint: `/ai/extract` <br>

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
        "methods": string,
        "majorFindings": string,
        "apa": string,
        "ieee": string
    }
]
```


#### Possible error responses by the server:

```
status: 400 | message: [MULTER ERROR]: Too many files
- Files sent are greater than 4.

status: 400 | message: [MULTER ERROR]: File too large
- One of the file sent is too large. 

status: 400 | message: <file name> cannot be read. Either remove it or replace it with a new one.
- One of the file's contents cannot be read, thus cannot be used with the AI model. 
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
API endpoint: `/pdf/viewUrl` <br>

JSON payload (request):
```
{
    "PdfKey": string
}
```
JSON payload (response): 
```
PDF view link
```

#### Get download link
HTTP Method: GET <br>
API endpoint: `/pdf/downloadUrl` <br>

JSON payload (request):
```
{
    "PdfKey": string,
    "PdfName": string
}
```
JSON payload (response): 
```
PDF download link
```
