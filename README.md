# internal-tool

A Python package and CLI for internal data management in the PR Agent project.  
It discovers documents from Google Drive and Notion, extracts raw text, generates summaries and embeddings, and stores metadata as per‑document JSON files.  

## Features

- Discover new documents in Google Drive and Notion
- Process pending documents: extract raw text, generate summary, create embeddings
- Store per-document metadata, raw text, and embeddings in configurable directories
- Clean, spreadsheet-free workflow using JSON metadata files
- Use CLI commands to:  
	-  List document IDs
	- Fetch URLs for specified documents
	- Directly download files by entering document ID

## Installation

You can install **_internal-tool_** from PyPI:  
`pip install internal-tool`

## One-time Configuration

Before running, create a file called `.env` in your working directory (or set environment variables directly).  
Provide the following required values:  

#### Google Drive configuration
```plaintext   
GDRIVE_CRED_FILE=/full/path/to/your-service-account.json  
GDRIVE_FOLDER_ID=your-drive-root-folder-id
```

#### Notion configuration  
```plaintext
NOTION_TOKEN=your-notion-integration-token  
NOTION_ROOT_PAGE_ID=your-notion-root-page-id  
```

#### Pinecone Setup
```plaintext
PINECONE_API_KEY="your-pinecone-key"
PINECONE_ENV="your-pinecone-region"
PINECONE_INDEX="your-index"
```

#### GEMINI Setup
```plaintext
GEMINI_API_KEY="your-gemini-api-key"
GEMINI_MODEL="gemini-1.5-flash-latest"
```

#### Optionally override output locations:**
```plaintext
#Where metadata JSONs will be written  
METADATA_DIR=/path/to/metadata

#Where raw-text JSONs will be written  
RAW_DIR=/path/to/raw

#Where embedding .npy files will be stored  
EMBEDDINGS_DIR=/path/to/embeddings 

#Where original file will be downloaded
DOWNLOAD_DIR=/path/to/downloads
``` 
#### Set up GEMINI API KEY for summarizer  
This package uses GEMINI's model `gemini-1.5-flash-latest` to generate summaries for the raw text. You can set it up by creating an API Key as follows:  
- Navigate to https://aistudio.google.com/app/apikey
- Sign up/Register with your google email
- Create a project or choose an existing project when prompted
- Click on `+ Create API Key` on the top right
- Store this key in your `.env` file by following the steps above

## Usage  

### Command Line
After installation and configuration:   
`# Set up Pinecone Connection`  
`pinecone-setup`   
`# Discover new documents and write metadata JSONs`    
`internal-discover`   
`# Process pending documents and push embeddings into Pinecone`  
`internal-process`  
`# Show list of processed documents`  
`pr-agent list-docs`  
`# Show the download URL for specific document`  
`pr-agent show-url`  
`# Download the required document`  
`pr-agent download <DOCUMENT_ID>`
 

## Directory Layout
By default, your project root will contain:  
```plaintext
outputs/internal-processed-docs/
metadata/       # per-document metadata JSON files
raw/            # per-document raw-text JSON files
embeddings/     # per-document .npy embedding files
downloads/      # all the dowloaded files 
```
You can change these via the `.env` overrides shown above.




