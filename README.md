# AI Video Assistant

Turn a YouTube video or local audio/video file into a searchable meeting
record: transcript, summary, action items, key decisions, open questions,
and a chat interface (RAG) to ask questions about the content.

## Tech stack

- **UI**: Streamlit
- **Transcription**: OpenAI Whisper (local, English) / Sarvam AI (Hinglish → English)
- **Summarization & extraction**: Mistral (via LangChain)
- **RAG / chat**: LangChain + ChromaDB + HuggingFace sentence-transformer embeddings
- **Audio/video acquisition**: yt-dlp, pydub, ffmpeg

## Local setup

1. Clone the repo:
   ```bash
   git clone https://github.com/Yogi06-U/AI-Video-Assistant.git
   cd AI-Video-Assistant
   ```

2. Install [ffmpeg](https://ffmpeg.org/download.html) on your system (not installable via pip).

3. Create a virtual environment and install dependencies:
   ```bash
   python -m venv venv
   source venv/bin/activate   # Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

4. Copy `.env.example` to `.env` and fill in your keys:
   ```bash
   cp .env.example .env
   ```
   - `MISTRAL_API_KEY` — required (summarization, extraction, chat)
   - `SARVAM_API_KEY` — only required if you'll use the "hinglish" language option
   - `WHISPER_MODEL` — `tiny`/`base`/`small`/`medium`/`large` (default `tiny`; bigger = more accurate but slower/heavier)

5. Run it:
   ```bash
   streamlit run app.py
   ```

## Known limitations

- Whisper transcription on CPU is slow — expect roughly real-time or slower for the `small` model and up.
- Free hosting tiers (Streamlit Community Cloud free tier, etc.) may struggle with `small`/`medium`/`large` Whisper models due to RAM limits — use `tiny` or `base` there.
- The Chroma vector store is rebuilt per session and persisted to a local `vector_db/` folder, which is ephemeral on most free hosts (fine for demo use, not for long-term storage).

## License

see [LICENSE](LICENSE).
