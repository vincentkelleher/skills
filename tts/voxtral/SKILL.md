---
name: voxtral
description: Use Mistral's Voxtral TTS model to generate speech from text.
---

## Authentication

Prefer reading `MISTRAL_API_KEY` from the environment or another local secret source.

If it is missing, ask the user once for the key or for permission to set it locally, then keep it in memory only for the current session.

Never repeat the key back to the user or write it to disk.

## List Available Voices

To list the available voices for the Voxstral TTS model, you can make a GET request to the Mistral API. This will allow you to retrieve a list of voices that you can use for text-to-speech conversion.

```shell
curl "https://api.mistral.ai/v1/audio/voices?limit=10&offset=0" \
  -H "Authorization: Bearer $MISTRAL_API_KEY"
```

## Generate Speech

To generate speech from text using the Voxstral TTS model, you can make a POST request to the Mistral API with the desired text and voice ID.

Always ask the user which voice ID they want to use for the text-to-speech conversion. You can provide them with the list of available voices retrieved in the previous step.

```shell
curl -X POST "https://api.mistral.ai/v1/audio/speech" \
  -H "Authorization: Bearer $MISTRAL_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "voxtral-mini-tts-2603",
    "input": "$TEXT_TO_CONVERT",
    "voice_id": "$VOICE_ID$",
    "response_format": "mp3"
  }' | jq -r '.audio_data' | base64 -d > output.mp3
```
