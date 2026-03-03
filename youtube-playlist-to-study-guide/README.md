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

## Reproduce It With Any Playlist

You can use this same workflow with any YouTube playlist:

```python
import videodb

conn = videodb.connect()
coll = conn.get_collection()

# Upload videos from your playlist
urls = [...]  # Your YouTube video URLs
videos = []
for url in urls:
    video = conn.upload(url=url)
    videos.append(video)

# Index and extract transcripts
transcripts = []
for video in videos:
    video.index_spoken_words()
    transcript = video.get_transcript_text()
    transcripts.append({
        "title": video.name,
        "transcript": transcript
    })

# Feed transcripts to an LLM to generate your study guide
```

## Ideas for Other Playlists

- MIT OpenCourseWare lecture series
- Conference talk collections
- Language learning courses
- Coding tutorial series
- Documentary series
