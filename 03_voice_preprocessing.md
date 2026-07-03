# Voice Preprocessing Checklist
### Run if voice input is part of the build

- [ ] Transcription quality tested with real users — actual accent, pace, and vocabulary, not generic benchmark
- [ ] Transcription error handling defined — common errors identified, correction layer or low-confidence fallback exists
- [ ] Speaker context preserved if needed — diarization implemented if who-said-what matters for retrieval
- [ ] Temporal context preserved if needed — sequence and timing maintained if order matters
- [ ] Full pipeline tested end-to-end — voice to transcription to query to retrieval to answer tested as complete chain
