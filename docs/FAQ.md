# RekoSearch FAQ

<!--toc:start-->

- [1. How accurate is RekoSearch's AI recognition for different types of content?](#1-how-accurate-is-rekosearchs-ai-recognition-for-different-types-of-content)
- [2. Can I search for multiple criteria simultaneously?](#2-can-i-search-for-multiple-criteria-simultaneously)
- [3. How long does it typically take to process files of different sizes?](#3-how-long-does-it-typically-take-to-process-files-of-different-sizes)
- [4. Is there a limit to how many files I can upload in a single job?](#4-is-there-a-limit-to-how-many-files-i-can-upload-in-a-single-job)
- [5. Can I organize my search results into collections or categories?](#5-can-i-organize-my-search-results-into-collections-or-categories)
- [6. Does RekoSearch work with files in languages other than English?](#6-does-rekosearch-work-with-files-in-languages-other-than-english)
- [7. How can I refine my search if I get too many results?](#7-how-can-i-refine-my-search-if-i-get-too-many-results)
- [8. Can I share my search results with team members?](#8-can-i-share-my-search-results-with-team-members)
- [9. Is my data used to train the AI models?](#9-is-my-data-used-to-train-the-ai-models)
- [10. What happens to my files after processing - are they stored, and for how long?](#10-what-happens-to-my-files-after-processing-are-they-stored-and-for-how-long)
- [11. Can I integrate RekoSearch with other applications or services?](#11-can-i-integrate-rekosearch-with-other-applications-or-services)
- [12. How do I export or download the search analysis for a file?](#12-how-do-i-export-or-download-the-search-analysis-for-a-file)
- [13. Are there any advanced search techniques to improve my results?](#13-are-there-any-advanced-search-techniques-to-improve-my-results)
- [14. Can I search for specific people or faces across my media?](#14-can-i-search-for-specific-people-or-faces-across-my-media)
- [15. What should I do if a file fails to process correctly?](#15-what-should-i-do-if-a-file-fails-to-process-correctly)
<!--toc:end-->

## 1. How accurate is RekoSearch's AI recognition for different types of content?

- **Images**: Highly accurate for clear images, especially faces and common objects, but accuracy may drop with poor lighting or unusual angles.
- **Videos**: Highly accurate for slow and medium paced videos with good quality, but may drop with fast paced and lower quality videos.
- **Audio**: 90% accurate with clear audio files, but accuracy may drop with noisy backgrounds.
- **Documents**: Highly accurate for standard typed documents; can struggle a little with handwriting, complex layouts, or low-quality scans.

_Note: The above is true for almost all AI (Machine Learning) powered detection software._

## 2. Can I search for multiple criteria simultaneously?

Yes, you can use prefixes to define what you are searching for and add more separated by spaces or simply use search terms without any prefixes. You can also chain terms using AND, OR and NOT operators to find what you're looking for more precisely.

## 3. How long does it typically take to process files of different sizes?

Processing time depends on queue status and media length:

- If resources are limited, jobs may remain "QUEUED" for a few minutes before changing to "PROCESSING"
- **Images**: ~1 second per image
- **Videos**: 1-2x the video length
- **Audio**: Almost real-time, slightly longer in some cases
- **Documents**: 1 to 3 seconds per page

The server takes approximately 30 seconds extra to finalize results and mark the job as finished.

## 4. Is there a limit to how many files I can upload in a single job?

Yes, there is a limit of 1000 files per job.

## 5. Can I organize my search results into collections or categories?

Currently, you can only save searches to run them again later, but you cannot name them or selectively choose which results to keep without refining the search filters. A collections/categories feature is planned for future development.

## 6. Does RekoSearch work with files in languages other than English?

Yes, for all file types except audio files.

## 7. How can I refine my search if I get too many results?

You can use prefixes to be more specific about what you're looking for or use filters to limit yourself to one or just a few detection types.

## 8. Can I share my search results with team members?

Sharing results and file access between accounts is currently not possible and not planned for the immediate future. However, we are developing a feature to download search results in various friendly formats. Downloading analysis for individual files is already possible.

## 9. Is my data used to train the AI models?

No, your data is not shared or used for anything other than processing it to give you the ability to search through it.

## 10. What happens to my files after processing - are they stored, and for how long?

Your files, including the results, will be stored for 30 days, after which they, including the job, will be completely and permanently deleted.

## 11. Can I integrate RekoSearch with other applications or services?

Soon. The API exists and is used by the frontend using OAuth 2.0 authentication, but an API Key system for user implementation is still in development.

## 12. How do I export or download the search analysis for a file?

When viewing a file processing job, each file in the list has three buttons on the right: one for downloading the complete analysis, one for downloading the minified analysis, and one for downloading the actual file.

## 13. Are there any advanced search techniques to improve my results?

You can combine multiple prefixes and search terms with the AND, OR, and NOT operators.

## 14. Can I search for specific people or faces across my media?

You can search for people with specific expressions (e.g., happy), but not by their name (except for celebrities).

## 15. What should I do if a file fails to process correctly?

You don't need to do anything, as you will be automatically refunded for files that fail to process. If all files in a job fail, you can request a refund at refund@rekosearch.com. If we determine you didn't intentionally upload malformed files, you will be refunded the other fees as well.
