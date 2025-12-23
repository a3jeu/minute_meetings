# minute_meetings

Convert a meeting audio/video into minutes (in French) with optional agenda
template support. Each step saves its outputs locally so you can resume without
re-running previous steps.

## Installation

Install the environment using either:
**Option 1: Using uv (recommended)**
```bash
uv sync
```

**Option 2: Using requirements.txt**
```bash
pip install -r requirements.txt
```

**Option 3: Using pyproject.toml**
```bash
pip install -e .
```

## Configuration

Create a `.env` file in the project root and add your API keys:

```
HF_TOKEN=hf_...
OPENAI_API_KEY=sk-proj-...
GROQ_API_KEY=gsk_...
```

## Usage

Generate minutes from a video:
```bash
python meeting_minutes.py generate --video videos/my_meeting.mkv
```

Generate minutes from an audio file:
```bash
python meeting_minutes.py generate --audio audio/my_meeting.mp3
```

Use an agenda template (docx):
```bash
python meeting_minutes.py generate --audio audio/my_meeting.mp3 --agenda agendas/my_agenda.docx
```

Select providers and models:
```bash
python meeting_minutes.py generate --audio audio/my_meeting.mp3 --provider openai
python meeting_minutes.py generate --audio audio/my_meeting.mp3 --provider groq
python meeting_minutes.py generate --audio audio/my_meeting.mp3 --provider local
python meeting_minutes.py generate --audio audio/my_meeting.mp3 --provider openai --transcript-model gpt-4o-mini-transcribe --minutes-model gpt-4o-mini
```

Check GPU availability:
```bash
python meeting_minutes.py check-gpu
```

Convert between docx and markdown:
```bash
python meeting_minutes.py docx-to-md agendas/my_agenda.docx
python meeting_minutes.py md-to-docx minutes/markdown/my_meeting.md
```

## Outputs

- Audio extracted from video: `audio/`
- Audio chunks: `audio/*_partN.mp3`
- Transcripts: `transcripts/*.txt`
- Merged transcript: `transcripts/*_full.txt`
- Minutes (markdown): `minutes/markdown/*.md`
- Minutes (docx): `minutes/word/*.docx`
- Agenda markdown: `agendas/markdown/*.md`

## Function summary

- Convert Word to Markdown: `docx-to-md` subcommand
- Convert Markdown to Word: `md-to-docx` subcommand
- Convert video to audio: `generate --video`
- Split audio into chunks: automatic when audio is longer than the threshold
- Transcribe audio: `--provider` (openai, groq, or local)
- Load agenda template: `--agenda`
- Generate minutes: `--provider` (openai, groq, or local)
- Check GPU: `check-gpu`
