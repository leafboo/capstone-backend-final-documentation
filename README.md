
# Backend endpoints documentation
- [Auth](#auth-endpoint) <br>
- [Users](#users-endpoint) <br>
- [Workspaces](#workspaces-endpoint) <br>
- [Research Papers](#research-papers-endpoint) <br>
- [AI](#ai-endpoint) <br>
- [Search](#search-endpoint)



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
{
    "Id": number,
    "Title": string,
    "Authors": string,
    "PublicationYear": number,
    "Keywords": string,
    "Objectives": string,
    "Methods": string,
    "Findings": string,
    "APA": string,
    "IEEE": string,
    "PDFURL": string
}
```
#### Create new Research paper
HTTP Method: POST <br>
API endpoint: `/workspaces/:workspaceId/researchPapers` <br> 

JSON payload (request):
```
{
    "title": string,
    "authors": string,
    "publicationYear": number,
    "keywords": string,
    "objectives": string,
    "methods": string,
    "findings": string,
    "apa": string,
    "ieee": string,
    "pdfUrl": string
}
```
#### Update Research paper column
HTTP Method: PUT <br>
API endpoint: `/workspaces/:workspaceId/researchPapers` <br> 

JSON payload (request):
```
{
    "columnName": string,
    "value": string
}
```

Editable Research paper columns are: 
- Keywords
- Methods
- Findings


> [!NOTE]
> "columnName" = column of research paper in the database <br>
> "value" = updated value of the column to be pushed to the database




## AI endpoint

> [!NOTE]
> This endpoint is not yet in service <br>

#### Extract Lit matrix table
HTTP Method: POST <br>
API endpoint: `/ai/extract` <br>

JSON payload (request):
```
{
    "pdfURLs": string[]
}
```
> [!IMPORTANT]
> The array pdfURLs should only contain 1 - 3 PDF URLs

<br>

JSON payload (response):
```
[
    {
        "title": string,
        "authors": string,
        "publicationYear": number,
        "keywords": string,
        "abstract": string,
        "methods": string,
        "findings": string,
        "apa": string,
        "ieee": string
    }
]
```



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
