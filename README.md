# dictado

Hold-to-talk dictation for Hyprland, like Wispr Flow. Hold a key, speak (Spanish by default), release, and the text is typed into the focused window. Transcription by Groq `whisper-large-v3-turbo`.

## Acceptance criteria

1. Holding the hotkey starts recording and shows a "listening" notification.
2. Releasing it stops recording and sends the audio to Groq with `language=es`.
3. The transcript is typed into the focused window with accents and ñ intact, ~1-2s after release for a short phrase.
4. Silence or a too-short press (<0.4s) types nothing.
5. Errors (missing key, network, API) show a notification and never type garbage.
6. The API key lives outside the repo, in `~/.config/dictado/env`.
7. No Python dependencies: stdlib plus `pw-record`, `wtype`, `notify-send`.

## Setup

```sh
sudo pacman -S wtype
mkdir -p ~/.config/dictado
echo 'GROQ_API_KEY=gsk_...' > ~/.config/dictado/env
chmod 600 ~/.config/dictado/env
ln -s "$PWD/dictado" ~/.local/bin/dictado
```

Add to `~/.config/hypr/hyprland.lua`:

```lua
hl.bind(mainMod .. " + D", hl.dsp.exec_cmd("dictado start"))
hl.bind(mainMod .. " + D", hl.dsp.exec_cmd("dictado stop"), { release = true })
```

## Config

Environment variables: `DICTADO_LANGUAGE` (default `es`), `DICTADO_MODEL` (default `whisper-large-v3-turbo`).

`dictado toggle` is available if you prefer press-to-start, press-to-stop.
