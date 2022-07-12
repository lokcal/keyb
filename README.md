# keyb

<p align="center">
	<img width="660" src="https://github.com/kencx/keyb/blob/master/assets/keyb.gif?raw=true">
</p>

<p align="center">Create and view your own custom hotkey cheatsheet in the terminal</p>

### Features
- Lightweight
- Fully customizable
- Fuzzy search
- Vim key bindings
- Export to stdout for fzf, rofi support

### Non-Features
keyb does **not** support:

- Auto detection of hotkeys
- Command selection

## Motivation

I had trouble remembering the various hotkeys that I sometimes use. It got
annoying to look them up so I resorted to writing them down on a paper
cheatsheet. Then, I thought: maybe there's a tool that does this better. I
didn't find one I liked so I built `keyb`.

With `keyb`, I can list:

- Hotkeys that I occasionally forget or am new to
- Custom key combinations that I defined for my own workflow
- Short commands that I sometimes use

It is best used as a popup cheatsheet binded to a hotkey.

## Install
keyb is still a work in progress. Use it at your own risk.

```bash
$ go get -u github.com/kencx/keyb
```

## Usage

```text
usage: keyb [options] [file]

Flags:
  -p, --print           Print to stdout
  -e, --export [file]   Export to file
  -k, --key [file]      Pass custom hotkeys file
  -c, --config [file]   Pass custom config file
  -v, --version         Version info
  -h, --help            help for keyb
```

### Printing

keyb supports printing to stdout for use with other tools:

```bash
$ keyb -p | fzf
$ keyb -p | rofi -dmenu
```

### keyb File

keyb requires a `yaml` file with a list of hotkeys to work. A default file is
generated at `$XDG_CONFIG_HOME/keyb/keyb.yml` if no other file is specified.

Hotkeys are classified into sections with a name and (optional) prefix field.
When displayed, sections are sorted by alphabetical order while the keys
themselves are arranged in their defined order.

The prefix is a key combination that will be prepended to every hotkey in the
section. A key can choose to opt out by including a `ignore_prefix: true` field.
Prefixes are useful for applications with a common leading hotkey like tmux.

```yaml
- name: bspwm
  keybinds:
    - name: terminal
      key: Super + Return

- name: tmux
  prefix: ctrl + a
  keybinds:
    - name: split vertical
      key: "|"
    - name: split horizontal
      key: "-"
    - name: {next, prev} window
      key: shift + {>, <}
      ignore_prefix: true
```

Refer to the defaults provided in `examples` for more details.

### Configuration
A config file is generated on the first run of `keyb`.

By default, the following options are included:

| Option      | Default                       | Description |
| ----------- | ----------------------------- | ----------- |
| `keyb_path` | `"$XDG_CONFIG_HOME/keyb/keyb.yml"` | keyb file path |
| `debug`       | `false`     | Debug mode |
| `mouse`       | `true`      | Mouse enabled |
| `reverse`     | `false`     | Swap the name and key columns |
| `title`       | `""`        | Title text |
| `prompt`      | `"keys > "` | Prompt text |
| `placeholder` | `"..."`     | Placeholder text |
| `prefix_sep`  | `";"`       | Separator symbol between prefix and key |
| `sep_width`   | `4`         | Separation width between columns |
| `margin`      | `0`         | Space between window and border |
| `padding`     | `1`         | Space between border and text |
| `border`      | `"hidden"`  | Border style: `normal, rounded, double, thick, hidden`|

#### Color
Both ANSI and hex color codes are supported.

| Color Option | Description |
| ------------ | ----------- |
| `prompt`       | Prompt text color |
| `cursor_fg`    | Cursor foreground |
| `cursor_bg`    | Cursor background |
| `filter_fg`    | Filter matching text foreground |
| `filter_bg`    | Filter matching text background |
| `border_color` | Border color |

#### Hotkeys

| Hotkey                     | Description      |
|--------------------------- | ---------------- |
| <kbd>j, k / Up, Down</kbd> | Move cursor      |
| <kbd>Ctrl + u, d</kbd>     | Move half window |
| <kbd>Ctrl + b, f</kbd>     | Move full window |
| <kbd>H, M, L</kbd>         | Go to top, middle, bottom of screen |
| <kbd>g, G</kbd>            | Go to first, last line |
| <kbd>/</kbd>               | Enter search mode|
| <kbd>alt + d</kbd>         | Clear current search |
| <kbd>Esc</kbd>             | Exit search mode |
| <kbd>Ctrl + c, q</kbd>     | Quit		        |

## Similar Tools

- [showkeys](https://github.com/adamharmansky/showkeys) offers a keybinding popup similar to awesomewm
- [cheat](https://github.com/cheat/cheat) is a CLI tool to view cheatsheets for
  commands and hotkeys for just about any topic
- Refer to [shortcut-pages](https://github.com/mt-empty/shortcut-pages), [cheat/cheatsheets](https://github.com/cheat/cheatsheets) for more cheatsheets

## License
[MIT](LICENSE)
