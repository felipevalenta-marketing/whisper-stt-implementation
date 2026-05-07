## Whisper STT Implementation Lab – Brief Report
# Introduction

This project focused on implementing a Speech-to-Text (STT) transcription system using OpenAI Whisper API. The objective was to transcribe meeting audio recordings, generate timestamps, process long recordings through chunking, and compare guided (prompted) versus unguided transcription approaches.

The system successfully processed audio files, generated timestamped transcriptions, and exported the results into multiple formats including TXT, JSON, and SRT.

Differences Between Prompted and Unprompted Transcriptions

Two transcription approaches were tested during the lab:

# 1. Unguided Transcription

The audio was transcribed without providing additional context or instructions to the model.

Advantages:

Faster and simpler implementation
Works well for clear and general speech
No need for domain-specific preparation

Disadvantages:

Lower accuracy for technical vocabulary
Greater chance of misinterpreting names or specialized terms
Less contextual understanding
# 2. Prompted (Guided) Transcription

A prompt was added to provide context about the meeting topic, including references to AI, APIs, automation, and business terminology.

Advantages:

Improved recognition of technical and business-related vocabulary
Better contextual understanding
More accurate interpretation of specialized terms

Disadvantages:

Requires additional prompt engineering
Results depend on prompt quality

Overall, the guided transcription produced more context-aware results and demonstrated better handling of domain-specific language.

Benefits of Chunking for Long Audio

Chunking divides large audio files into smaller segments before transcription.

# Main Benefits:
Avoids API file size limitations
Improves processing reliability
Makes error handling easier
Reduces the risk of transcription failure on large files
Enables timestamp synchronization across long recordings

Chunking is essential in production environments where meetings, interviews, or podcasts may last several hours.

In this lab, timestamps from each chunk were adjusted using chunk offsets, allowing the final transcription to preserve the original timeline accurately.

Challenges Faced

Several technical challenges were encountered during the implementation process:

# 1. Python Compatibility Issues

The pydub library generated errors because Python 3.13 removed the audioop module.

Solution:
FFmpeg was used directly instead of relying on pydub.

# 2. FFmpeg Configuration

FFmpeg was initially not recognized by the system.

Solution:
FFmpeg was installed and added to the system PATH.

# 3. API Errors

Different API-related issues appeared during testing, including quota and authentication errors.

Solution:
The API key was updated and verified using environment variables stored securely in a .env file.

# 4. Timestamp Synchronization

Chunk timestamps initially did not align correctly with the original audio timeline.

Solution:
Chunk offsets were added to each segment timestamp during transcription merging.

# Recommendations for Improving Accuracy

Several improvements can increase transcription quality:

- Use guided prompts with domain-specific vocabulary
- Record high-quality audio with minimal background noise
- Use larger chunk sizes for better context continuity
- Specify the spoken language when possible
- Normalize audio volume before processing
- Use better microphones for recording meetings

Additionally, implementing speaker diarization could improve transcript readability by identifying different speakers automatically.

# Conclusion

The Whisper STT implementation successfully demonstrated how to build a scalable speech-to-text pipeline capable of handling long audio recordings with timestamps and multiple export formats.

The project highlighted the importance of chunking, prompt engineering, and proper audio preprocessing for achieving reliable and accurate transcription results in real-world business applications.