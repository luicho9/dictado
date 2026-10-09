# dictado

Voice dictation for Hyprland, like Wispr Flow. Press **SUPER+D**, talk, press **SUPER+D** again, and your words get typed wherever your cursor is.

It uses Groq's Whisper API, so it's fast even on old laptops and costs basically nothing (the free tier is plenty). Spanish by default.

## Setup

You need a Groq API key from [console.groq.com/keys](https://console.groq.com/keys).

```sh
sudo pacman -S wtype

mkdir -p ~/.config/dictado
echo 'GROQ_API_KEY=gsk_...' > ~/.config/dictado/env
chmod 600 ~/.config/dictado/env

ln -s "$PWD/dictado" ~/.local/bin/dictado
```

Then add the shortcut to `~/.config/hypr/hyprland.lua`:

```lua
hl.bind(mainMod .. " + D", hl.dsp.exec_cmd("dictado toggle"))
```

## Usage

1. Click where you want the text.
2. Press SUPER+D and start talking.
3. Press SUPER+D again when you're done. The text shows up a second later.

Tap the keys and let go. If you're still holding SUPER when the text is typed, the letters can trigger your Hyprland shortcuts.

## Options

Want English or another language? Set `DICTADO_LANGUAGE` (e.g. `en`). To change the model, set `DICTADO_MODEL` (default `whisper-large-v3-turbo`).
