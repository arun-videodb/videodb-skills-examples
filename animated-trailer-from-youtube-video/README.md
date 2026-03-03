# Animated Trailer from a YouTube Video

Transform any movie trailer into an AI-generated animated trailer with consistent style, coherent storyline, and original score — using natural language prompts in [Claude Code](https://claude.com/claude-code) with [VideoDB Skills](https://github.com/video-db/skills).

## Example Output

**Original:** [Inception (2010) Official Trailer](https://www.youtube.com/watch?v=YoHD9XEInc0) (2m 23s)

**Generated:** [30-second Animated Inception Trailer](https://console.videodb.io/player?url=https://stream.videodb.io/v3/published/manifests/950b5c8d-1eba-4490-a565-8c58b7702806.m3u8)

https://github.com/user-attachments/assets/placeholder-animated-trailer-demo.mp4

## How It Works

```
Upload trailer → Analyze scenes & dialogue → Design storyline → Generate animated clips → Add music → Compose timeline
```

| Step | What happens | VideoDB API |
|------|-------------|-------------|
| Upload | Ingest the original trailer | `coll.upload()` |
| Analyze | Extract dialogue and detect scenes | `index_spoken_words()`, `index_scenes()` |
| Storyline | LLM distills key moments into a narrative arc | `get_transcript_text()`, `get_scene_index()` |
| Animate | Generate clips with a shared style prompt | `coll.generate_video()` |
| Score | Generate background music | `coll.generate_music()` |
| Compose | Sequence clips and overlay music | `Timeline`, `VideoAsset`, `AudioAsset` |

## Prompts Used

**1. Generate the trailer**
> /videodb upload this trailer https://www.youtube.com/watch?v=YoHD9XEInc0, analyse it, and create a 30 second animated version. Use a consistent dark cinematic anime style across all scenes with a coherent storyline.

**2. Refine scenes that don't match** *(iterate as needed)*
> Regenerate scene 2 in the same animation style as the other scenes.

**3. Add music and polish**
> Add 30 seconds of intense orchestral background music that fades out on a mysterious note at the end.

## Generated Storyline

The LLM analyzed 88 detected scenes and distilled them into a 6-scene arc:

| Scene | Description |
|-------|-------------|
| **The Dreamer** | A man washed ashore on a dark stormy beach |
| **The Dream Folds** | A city street bending and folding upward on itself |
| **Going Deeper** | A hotel hallway rotating with zero-gravity combat |
| **The Fortress** | A snow fortress under siege with an approaching avalanche |
| **The Fall** | A city skyline shattering and collapsing into an abyss |
| **The Question** | A spinning top wobbling on a table — will it fall? |

## Key Technique: Consistent Animation Style

Append a **shared style anchor** to every video generation prompt:

```python
style = "dark cinematic anime style, deep blue and warm amber color palette, dramatic lighting, detailed digital illustration, film grain"

vid = coll.generate_video(
    prompt=f"A city skyline shattering like glass, buildings crumbling into a dark abyss, debris floating upward, epic scale, {style}",
    duration=5,
)
```

This ensures all scenes share the same visual language. Individual scenes can be regenerated and swapped in without redoing the whole project.

## Try It Yourself

```
/videodb upload this trailer <YOUR_VIDEO_URL>, analyse it, and create a 30 second animated version. Use a consistent animation style across all scenes with a coherent storyline.
```

### Ideas

- **Game trailers** — Turn a live-action game trailer into anime style
- **Documentary teasers** — Reimagine a nature documentary as stylized animation
- **Music videos** — Create an animated music video from a lyric video
- **Product demos** — Transform a product walkthrough into an animated explainer

---

Built with [VideoDB Skills](https://github.com/video-db/skills) and [Claude Code](https://claude.com/claude-code).
