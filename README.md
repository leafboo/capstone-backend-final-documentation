# Backend endpoints documentation
Documentation for using the api endpoints
## Endpoints: 
- [Auth](#auth-endpoint) <br>
- [Users](#users-endpoint) <br>
- [Workspaces](#workspaces-endpoint) <br>
- [Research Papers](#research-papers-endpoint) <br>

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
---
#### Log Out

HTTP Method: DELETE <br>
API endpoint: `/auth/logout` <br> 

---
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
---
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
---
#### Update user password
HTTP Method: PUT <br>
API endpoint: `/users/me/password` <br> 

JSON payload (request):
```
{
    "newPassword": number
}
```
---
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
---
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
---
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
---
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
    "Abstract": string,
    "Methods": string,
    "Findings": string,
    "APA": string,
    "IEEE": string,
    "PDFURL": string
}
```
---
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
    "abstract": string,
    "methods": string,
    "findings": string,
    "apa": string,
    "ieee": string,
    "pdfUrl": string
}
```
---
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


> Note: <br> <br>
"columnName" = column of research paper in the database <br>
"value" = updated value of the column to be pushed to the database

## AI endpoint
no contents yet
