---
title: "Error Code Reference"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication-v3-error-code-reference"
---

When the API returns an error, use the error code to diagnose the issue and either fix the request or surface a clear message to the end user.

&nbsp;


|**Code** |**Message** |**Resolution** |
|---|---|---|
|45001001 |Invalid request parameters |Review the parameters against the API spec, ensure all required fields are provided, and confirm enum values are valid. |
|45001101 |Audio upload failed |Retry the upload. Check your network connection and timeout settings, and confirm the audio format and size meet the documented limits. |
|45001102 |ASR transcription failed |Retry with a clearer recording (distinct speech, low background noise), or use a different sample. |
|45001104 |Voiceprint check failed |Try a different sample or speaker, and avoid voices that resemble protected targets. |
|45001105 |Failed to read audio data |Make sure the audio field is not empty, the base64 encoding is valid, and the URL is reachable. Re\-upload if the issue persists. |
|45001107 |SpeakerID not found |Verify the speaker_id against the speaker list. If it has been deleted, create a new one. |
|45001108 |Audio transcoding failed |Confirm the audio format and sample rate are supported, and provide a decodable file. Retry or use a different sample. |
|45001109 |WER check failed |Retry, and make sure the prompt audio matches the prompt text. |
|45001110 |Voice deletion failed |Retry, and confirm that the speaker_id exists. |
|45001112 |SNR check failed |Retry with audio that has a higher signal\-to\-noise ratio, and verify the sample rate and format. |
|45001113 |Denoising failed |Retry. If the issue persists, disable denoising, switch models, or use a different audio sample. |
|45001114 |Audio quality too low |Provide a higher\-quality audio sample. |
|45001122 |ASR detected no speech |Use audio with clear, prominent speech and minimal background noise. |
|45001123 |Upload quota exhausted |Switch to a speaker_id that still has training credits available. |
|45001124 |ASR text rejected by review |Replace the audio content and avoid sensitive material. Request a manual review or whitelist if appropriate. |
|45001125 |Demo text rejected by review |Edit the demo text to remove sensitive wording and ensure it complies with policy. |
|45001126 |Demo text length error |Adjust the text to meet the length limits—trim or expand as needed. |
|45001127 |Prompt audio rejected by review |Replace the audio with compliant material, avoiding any sensitive or non\-compliant content. |
|45001128 |Prompt audio text rejected by review |Replace the audio or text, avoiding sensitive content. Request whitelisting if necessary. |
|55001301 |Database query failed |Server\-side error. Please retry; contact support if the issue persists. |
|55001302 |Database insert failed |Server\-side error. Please retry; contact support if the issue persists. |
|55001303 |Database update failed |Server\-side error. Please retry; contact support if the issue persists. |
|55001304 |Database delete failed |Server\-side error. Please retry; contact support if the issue persists. |
|55001305 |TOS upload failed |Server\-side error. Please retry; contact support if the issue persists. |
|55001306 |TOS download failed |Server\-side error. Please retry; contact support if the issue persists. |
|55001307 |Voice cloning failed |Server\-side error. Please retry; contact support if the issue persists. |
