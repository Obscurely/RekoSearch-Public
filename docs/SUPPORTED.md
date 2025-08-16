# AWS Services and File Types used by RekoSearch

Below is a list of the AWS services used by RekoSearch and the file types they support. Each service has its own limitations, which are also listed.

<!--toc:start-->

- [AWS Rekognition](#aws-rekognition)
- [AWS Textract](#aws-textract)
- [AWS Transcribe](#aws-transcribe)
- [All Supported File Extensions](#all-supported-file-extensions)
<!--toc:end-->

## AWS Rekognition

- **Image Formats**: PNG, JPEG
- **Video Formats**: MP4, MOV
- **Limits**:
  - **Images**: Maximum file size of 15MB
  - **Videos**: Maximum file size of 10GB, maximum length of 2 hours

## AWS Textract

- **Document Formats**: PDF, TIFF
- **Limits**:
  - Maximum file size: 500MB
  - Maximum pages per document: 50 pages
  - Maximum total pages across all files: 3,000 pages
  - Maximum dimensions: 40 inches or 2880 points in height and width
  - **Note**: PDFs cannot be password protected. PDFs can contain
    JPEG 2000 formatted images.

## AWS Transcribe

- **Audio Formats**: MP3, WAV, FLAC, AMR, OGG
- **Video Formats**: WEBM
- **Limits**:
  - Maximum file size: 2GB
  - Maximum length: 4 hours
  - Audio must be in English (US).

## All Supported File Extensions

`.png`, `.jpeg`, `.mp4`, `.mov`, `.tiff`, `.pdf`, `.mp3`, `.wav`,
`.flac`, `.amr`, `.ogg`, `.webm`
