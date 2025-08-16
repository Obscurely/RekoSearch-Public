# RekoSearch Pricing

The Pricing structure for RekoSearch.
All prices are listed in credits, where 1 credit equals $0.1 USD.

**Important Note**: Credit calculations are always rounded up to the next
whole number. For example, 1.01 credits will be charged as 2 credits.

<!--toc:start-->

- [Storage Costs](#storage-costs)
- [AI Processing Costs](#ai-processing-costs)
  - [Amazon Rekognition](#amazon-rekognition)
  - [Amazon Textract](#amazon-textract)
  - [Amazon Transcribe](#amazon-transcribe)
- [Infrastructure Costs](#infrastructure-costs)
- [Processing Time Costs](#processing-time-costs)
- [Additional Fees](#additional-fees)
- [Pricing Examples](#pricing-examples)
  - [Single File Processing](#single-file-processing)
  - [Batch Processing (Multiple Files in One Job)](#batch-processing-multiple-files-in-one-job)
  <!--toc:end-->

## Storage Costs

- **Content Storage**: 0.00028 credits per MB (0.000028 USD)
  (includes 20% for result retention)
- **Data Transfer**: 0.0025 credits per MB (0.00025 USD)
  - S3 Data in/out (S3 Accelerated): 0.002 credits per MB (0.0002 USD)
  - S3 Requests: 0.0005 credits per MB (0.00005 USD)

## AI Processing Costs

### Amazon Rekognition

- Images: 0.036 credits per image (0.0036 USD) (label detection,
  facial analysis & text detection)
- Videos: 3.6 credits per minute (0.36 USD) (label detection,
  facial analysis & text detection)

### Amazon Textract

- PDF/TIFF: 0.015 credits per page (0.0015 USD) (basic text detection)

### Amazon Transcribe

- Audio: 0.004 credits per second (0.0004 USD) (standard processing, 15-second minimum)

## Infrastructure Costs

- SQS: 0.05 credits (0.005 USD)
- SES: 0.005 credits (0.0005 USD) (covers emails sent outside the job)
- DynamoDB: 0.002 credits (0.0002 USD) (database operations throughout the application)
- API Gateway: 0.001 credits (0.0001 USD) (API calls throughout the application)
- Lambda: 0.001 credits (0.0001 USD) (all Lambda functions executions)
- CloudFront: 0.002 credits (0.0002 USD) (requests and data transfer)

## Processing Time Costs

- Images: 0.004 credits per image (0.0004 USD)
- Videos: 0.004 credits per second (0.0004 USD)
- Documents: 0.004 credits per page (0.0004 USD)
- Audio: 0.004 credits per second (0.0004 USD)

## Additional Fees

- Base job fee: 0.5 credits (0.05 USD) (maintenance and other operational costs)
- 25% operational buffer
- 15% service fee

**NOTE**: Fee multipliers are not added on top of one another, but separately

## Pricing Examples

### Single File Processing

**NOTE**: Check batch examples below to see how much more
you can save on processing multiple files

1. **Single Image (5MB)**

   - Base fee: 0.5 credits (0.05 USD)
   - Storage: 0.00028 × 5 = 0.0014 credits (0.00014 USD)
   - AI Processing: 0.036 credits (0.0036 USD)
   - Processing Time: 0.004 credits (0.0004 USD)
   - Infrastructure: 0.061 credits (0.0061 USD)
   - Subtotal: 0.6024 credits (0.06024 USD)
   - With buffer & service fee: 0.8434 credits (0.08434 USD)
   - **Total (rounded up): 1 credit (0.1 USD)**

2. **1-minute Video (50MB)**
   - Base fee: 0.5 credits (0.05 USD)
   - Storage: 0.00028 × 50 = 0.014 credits (0.0014 USD)
   - AI Processing: 3.6 credits (0.36 USD)
   - Processing Time: 0.004 × 60 = 0.24 credits (0.024 USD)
   - Infrastructure: 0.061 credits (0.0061 USD)
   - Subtotal: 4.415 credits (0.4415 USD)
   - With buffer & service fee: 6.181 credits (0.6181 USD)
   - **Total (rounded up): 7 credits (0.7 USD)**

### Batch Processing (Multiple Files in One Job)

1. **5 Images (25MB total)**

   - Base fee: 0.5 credits (0.05 USD) (only charged once per job)
   - Storage: 0.00028 × 25 = 0.007 credits (0.0007 USD)
   - AI Processing: 0.036 × 5 = 0.18 credits (0.018 USD)
   - Processing Time: 0.004 × 5 = 0.02 credits (0.002 USD)
   - Infrastructure: 0.061 credits (0.0061 USD)
   - Subtotal: 0.768 credits (0.0768 USD)
   - With buffer & service fee: 1.0752 credits (0.10752 USD)
   - **Total (rounded up): 2 credit (0.2 USD)**

2. **Mixed Batch (2 images, 1 minute video, 5-page PDF)**
   - Base fee: 0.5 credits (0.05 USD) (only charged once)
   - Storage (assuming 70MB total): 0.00028 × 70 = 0.0196 credits (0.00196 USD)
   - AI Processing:
     - Images: 0.036 × 2 = 0.072 credits (0.0072 USD)
     - Video: 3.6 credits (0.36 USD)
     - PDF: 0.015 × 5 = 0.075 credits (0.0075 USD)
   - Processing Time:
     - Images: 0.004 × 2 = 0.008 credits (0.0008 USD)
     - Video: 0.004 × 60 = 0.24 credits (0.024 USD)
     - PDF: 0.004 × 5 = 0.02 credits (0.002 USD)
   - Infrastructure: 0.061 credits (0.0061 USD)
   - Subtotal: 4.5956 credits (0.45956 USD)
   - With buffer & service fee: 6.43384 credits (0.643384 USD)
   - **Total (rounded up): 7 credits (0.7 USD)**

**Note**: As demonstrated in the examples above, processing multiple files
in a single job is more cost-effective as the base job fee is only charged once,
resulting in significant savings for batch processing.
