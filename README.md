# AI Photo Search using AWS

This project is a serverless web application that allows users to upload and search photos using natural language queries powered by AI and AWS services. It leverages AWS Lambda, Amazon Lex, Amazon Rekognition, OpenSearch, S3, and API Gateway.

---

## Architecture Overview

```
                         +---------------------+
                         |       Browser       |
                         | (Upload & Search UI)|
                         +---------------------+
                                   |
                                   v
                         +---------------------+
                         |    API Gateway      |
                         +---------------------+
                          |                 |
                          v                 v
             +------------------+     +----------------------+
             | Lambda:          |     | Lambda:              |
             | index-photos.py  |     | search-photos.py     |
             +------------------+     +----------------------+
               |        |                     |
       +-------+        |                     +---------------------+
       |                v                                           |
       |       +--------------------+                               |
       |       | Amazon Rekognition |                               |
       |       +--------------------+                               |
       |                |                                           |
       |                v                                           v
       |       +--------------------+                     +--------------------+
       |       |  Amazon OpenSearch |<--------------------|     Amazon Lex     |
       |       +--------------------+                     +--------------------+
       |                |
       v                v
+----------------+   +----------------+
| Amazon S3      |   | Search Results |
| (Photo Storage)|   +----------------+
+----------------+
```

---

## Features

- Upload images and generate automatic labels using Amazon Rekognition
- Natural language photo search via Amazon Lex and OpenSearch
- Web-based frontend for uploading and searching photos
- Serverless backend with Lambda functions and API Gateway
- IAM roles and permissions configured for secure access

---

## Project Structure

```
AI-Photo-Search-using-AWS-main/
├── Frontend/                      # Static frontend for photo upload/search
│   ├── index.html                 # Main UI page
│   ├── apigClient.js              # API Gateway client for invoking backend
│   ├── lib/                       # Supporting libraries (CryptoJS, Axios, etc.)
│   └── README.md                  # Frontend-specific README
│
├── Lambda_functions/             # AWS Lambda functions
│   ├── index-photos.py           # Handles image upload and indexing via Rekognition
│   └── search-photos.py          # Handles natural language search via Lex and OpenSearch
│
├── otherscripts/                 # CI/CD and infrastructure scripts
│   ├── backend-buildspec.yml     # Build spec for backend Lambda deployment
│   ├── frontend-buildspec.yml    # Build spec for frontend deployment
│   └── photo-search-stack.yaml   # CloudFormation template to deploy full stack
│
├── photo-album-api-dev-swagger.yaml  # Swagger/OpenAPI definition for REST API
└── README.md                     # Project documentation (this file)
```

---

## Setup & Deployment

### Prerequisites

- AWS account with IAM roles for Lambda, S3, OpenSearch, Lex
- AWS CLI & SAM/CloudFormation tools

### Steps

1. **Deploy Infrastructure**  
   Use the `photo-search-stack.yaml` CloudFormation script to deploy the stack.

2. **Upload Lambda Functions**  
   Deploy `index-photos.py` and `search-photos.py` using the Lambda console or CI/CD (`backend-buildspec.yml`).

3. **Configure Lex Bot**  
   Create a Lex bot for photo search intent with slot types for labels.

4. **Frontend Deployment**  
   Upload contents of `Frontend/` to an S3 static website bucket.

---

## Testing

- Upload a photo through the web interface
- Use the search box with queries like:
  - "Show me pictures of beaches"
  - "Find sunset photos"

---

## Tech Stack

- AWS Lambda
- Amazon Lex
- Amazon Rekognition
- Amazon OpenSearch
- Amazon S3
- API Gateway
- JavaScript (Frontend)

---

## License

MIT License. See `LICENSE` file (if included) for details.
