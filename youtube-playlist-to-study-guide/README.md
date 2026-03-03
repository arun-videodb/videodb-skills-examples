# YouTube Playlist to Study Guide

Turn any YouTube playlist into a comprehensive, structured study guide by extracting transcripts from every video and synthesizing them into organized notes.

## Example Output

See the generated study guide: [Essence of Linear Algebra Study Guide](./essence_of_linear_algebra_study_guide.md) — built from [3Blue1Brown's "Essence of Linear Algebra"](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab) playlist (16 videos).

## How It Works

```
YouTube Playlist
      │
      ▼
┌─────────────┐
│  Upload all  │  videodb.upload(url=youtube_url)
│   videos     │
└─────┬───────┘
      │
      ▼
┌─────────────┐
│ Index spoken │  video.index_spoken_words()
│   words      │
└─────┬───────┘
      │
      ▼
┌─────────────┐
│   Extract    │  video.get_transcript_text()
│ transcripts  │
└─────┬───────┘
      │
      ▼
┌─────────────┐
│  Synthesize  │  LLM processes all transcripts
│ study guide  │  into structured notes
└─────────────┘
```

## VideoDB Skills Used

| Skill | Purpose |
|---|---|
| `videodb.upload()` | Upload each YouTube video to VideoDB by URL |
| `video.index_spoken_words()` | Index the audio track for transcript extraction |
| `video.get_transcript_text()` | Extract the full spoken transcript as text |

## Step-by-Step Workflow

1. **Get playlist videos** — Fetch all video URLs from a YouTube playlist
2. **Upload to VideoDB** — Upload each video using `videodb.upload(url=youtube_url)`
3. **Index spoken words** — Run `video.index_spoken_words()` on each video to process the audio
4. **Extract transcripts** — Call `video.get_transcript_text()` to get the full text transcript for each video
5. **Synthesize** — Feed all transcripts to an LLM with a prompt to generate a structured study guide, organized by chapter/topic with key concepts, examples, and takeaways

## Prompts Used

This study guide was created using [Claude Code](https://claude.com/claude-code) with VideoDB skills enabled. Here's the exact prompt sequence:

**Prompt 1** — Kick off the entire workflow with a single request:

> /videodb upload all videos from this playlist https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab, extract transcripts, and create a structured study guide in a .md file

That's it. VideoDB skills automatically upload all 16 videos, index spoken words, extract transcripts, and the LLM synthesizes everything into the structured study guide.

## Reproduce It With Any Playlist

Swap in your own playlist URL and adjust the output format to taste:

> /videodb upload all videos from this playlist `<YOUR_PLAYLIST_URL>`, extract transcripts, and create a structured study guide in a .md file

You can also get more specific with what you want:

> /videodb upload all videos from this playlist `<YOUR_PLAYLIST_URL>`, extract transcripts, and create a cheat sheet with key formulas and definitions

> /videodb upload all videos from this playlist `<YOUR_PLAYLIST_URL>`, extract transcripts, and generate a Q&A revision guide with practice questions for each video

## Ideas for Other Playlists

- MIT OpenCourseWare lecture series
- Conference talk collections
- Language learning courses
- Coding tutorial series
- Documentary series
