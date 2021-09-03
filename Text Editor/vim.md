---
date updated: '2021-09-03T16:10:05+07:00'

---

# Switch mode

|   Mode  |                                                                           How to turn mode on                                                                           |
| :-----: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|  INSERT |                                                           `I` key. `INSERT` mode allow you to edit your buffer                                                          |
| COMMAND |                                           `ESC` key. `COMMAND` mode allow you to run specified command in Vim like quit, save                                           |
|  VISUAL | `V` key. This mode allow you to selected characters to interact with them like copy, paste or delete. There is a cursor for you to select text when `VISUAL` is enabled |
|  NORMAL |                                                            Like temporary mode to switch between other modes                                                            |

# Action

| Action               |                                  How to archive action                                 |  Mode  ||
| -------------------- | :------------------------------------------------------------------------------------: | :----: |
| Selected all file    |                                         `ggVG`                                         | VISUAL |
| Delete selected text |                                           `d`                                          | VISUAL |
| Delete current line  |                                          `dd`                                          | VISUAL |
| Copy selectex text   |                                           `y`                                          | VISUAL |
| Paste                |             `p` to paste after cursor. `Shift` + `P` to paste befor cursor             | VISUAL |
| Copy current line    |                                          `y+`                                          | VISUAL |
| Go to top| `gg`| NORMAL|
| Go to nth line       |                                  `<ntn>G` (e.x: `42G`)                                 | NORMAL |
| Undo                 |                                           `u`                                          | VISUAL |
| Redo                 |                                      `Ctrl` + `r`                                      | NORMAL |
| Search `keyword`     | `/` + `keyword` => `Enter`, then press `n` or `Shift` + `N` to go next/previous result | NORMAL |

# Command

|    Command   | How to archive command |
| :----------: | :--------------------: |
|     Quit     |          `:q`          |
|  Force quit  |          `:q!`         |
| Write & quit |          `:wq`         |

# My customs

| Action                                    |          How to archive action         |  Mode  |
| ----------------------------------------- | :------------------------------------: | :----: |
| Open NerdTree (File Browser)              |              `Space` + `n`             | NORMAL |
| Open NerdTree menu (add, edit, move file) | Press `m`. NerdTree must be focused on | NORMAL |
| Go to file                                |              `Space` + `g`             | NORMAL |
| Open buffer in new tab                    |              `Ctrl` + `t`              | NORMAL |
| Toggle Terminal                           |              `Space` + `t`             | NORMAL |
| Go to defintion                           |   `gd`. Then `Ctrl` + `o` to go back   | VISUAL |
| Show documentation                        |                   `K`                  | VISUAL |

Tags: #vim
