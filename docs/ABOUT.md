# About RekoSearch

Below you will find information about RekoSearch, including what it is, how it works, and its supported file types. You can also find information about privacy and security, as well as links to additional resources.

<!--toc:start-->

- [What is RekoSearch?](#what-is-rekosearch)
- [Why Use RekoSearch?](#why-use-rekosearch)
- [How It Works](#how-it-works)
- [Supported File Types & Limitations](#supported-file-types-limitations)
  - [Images](#images)
  - [Videos](#videos)
  - [Documents](#documents)
  - [Audio](#audio)
  - [All Supported Extensions](#all-supported-extensions)
- [Requirements](#requirements)
- [Privacy & Security](#privacy-security)
  - [How is my data handled?](#how-is-my-data-handled)
  - [How is the analysis done?](#how-is-the-analysis-done)
- [Additional Resources](#additional-resources)
<!--toc:end-->

## What is RekoSearch?

RekoSearch is an AI-powered file search engine for images, videos, documents and audio that understands the content of your files. It enables simultaneous semantic search across:

- **Images & Videos**: Find objects, scenes, activities, landmarks, facial attributes and text.
- **Documents**: Search through the actual content (text).
- **Audio**: Search through what's being said.

You can plainly search for what you want, or use advanced search syntax like the example below:

```
label:dog AND face:smiling NOT text:warning
```

(This will find images and videos with a dog and a person smiling, but no text spelling "warning".)

Alternatively, you can also download just the results files.

## Why Use RekoSearch?

Some of the use cases include:

1. **Time-Saving Media Discovery**:

   - Save time by quickly and accurately finding specific content in large media libraries without manually reviewing each file.
   - Locate that 'needle in a haystack' image, video clip, document reference, or audio segment using natural language queries.

2. **Content Filtering**:

   - Filter media containing specific objects, scenes, text, facial expressions, spoken phrases and more.
   - Create precise collections by combining multiple search criteria (e.g., `label:product AND text:promotion NOT face:unhappy`)
   - Help organize media based on content rather than just metadata.

3. **Knowledge Mining**:
   - Discover connections between concepts mentioned in documents, shown in images/videos, or discussed in audio recordings.
   - Extract insights from unstructured data.

## How It Works

RekoSearch has a simple and easy to use workflow:

1. **Upload Your Files**:

   - In the Jobs tab, click '+ New Job' and select the files you want to process and search through.
   - Optionally, give your job a name and choose whether you want to receive email updates.

2. **AI Analysis**:

   - Once created, your job will appear in the Jobs List. Wait for the status to change to 'Success'.
   - Multiple AI tools analyze and index the content within your files, identifying objects, text, faces, and more.

3. **Search & Discover**:
   - After processing is complete, click on your job and either click on 'Search Analysis' or download the analysis files.
   - Use natural language or advanced queries to find exactly what you're looking for across all your media.

## Supported File Types & Limitations

RekoSearch supports various media formats to help you find what you need.

### Images

- **Formats**: PNG, JPEG
- **Limitations**:
  - Maximum file size: 15MB

### Videos

- **Formats**: MP4, MOV
- **Limitations**:
  - Maximum file size: 10GB
  - Maximum duration: 2 hours

### Documents

- **Formats**: PDF, TIFF
- **Limitations**:
  - Maximum file size: 500MB
  - Maximum pages per document: 50 pages
  - Maximum total pages across all files: 3,000 pages
  - Maximum dimensions: 40 inches in height and width
  - **Note**: PDFs cannot be password-protected

### Audio

- **Formats**: MP3, WAV, FLAC, AMR, OGG, WEBM
- **Limitations**:
  - Maximum file size: 2GB
  - Maximum duration: 4 hours
  - Must be in English (US)

### All Supported Extensions

`.png`, `.jpeg`, `.mp4`, `.mov`, `.tiff`, `.pdf`, `.mp3`, `.wav`, `.flac`, `.amr`, `.ogg`, `.webm`

## Requirements

- **Web Browser**: A Chromium or Firefox based release from 2022 and newer should suffice.
- **Internet Speed**: A speed of at least 112 kbps exclusively allocated to the app will suffice.
- **Geo Location**: You must be in the US or Europe.
- **Age**: You must be 18 or older to use this service.
- **Policies**: You agree to and comply with the [Terms of Service](../TOS.md) and [Privacy Policy](../PRIVACY.md).

## Privacy & Security

### How is my data handled?

Your personal information, such as name, email, birthdate, and password, is handled by AWS Cognito, an authentication service and user database developed by Amazon with the highest security standards and constantly checked and updated by them. Authentication with this service is done using the OAuth 2.0 framework, one of the most secure standards used by companies like Amazon, Google, Meta, Microsoft and Twitter.

Your files are encrypted end-to-end in transit and at rest using AWS S3 storage service. Processing of your files is done using AWS services (Rekognition, Transcribe and Textract); these services do not share or distribute your data anywhere. Nothing you upload will be shared with any other entity.

Your files, including the results, will be stored for 30 days, after which they, including the job, will be completely and permanently deleted.

### How is the analysis done?

The file analysis is done using AWS services. These AWS services do not use your data to train their models, share it with anybody, or use it for any other purposes.

Your data is not uploaded to these services, instead they read it from S3 with limited access only during the execution

The analysis is then stored in the same secure S3 bucket

## Additional Resources

- Check [Pricing](./PRICING.md) for pricing information.
- Check [Features](./FEATURES.md) for a list of available features in RekoSearch.
- Check [API Docs](./API/README.md) for details on integrating with the RekoSearch API.
- Check [FAQ](./FAQ.md) if you have any questions.
- If you wish to get in contact, check [Contact](../CONTACT.md)
