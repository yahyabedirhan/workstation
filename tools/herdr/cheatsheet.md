# herdr cheat sheet

Prefix is `ctrl+b` (same as tmux): press, release, then the key. `ctrl+b ?` opens the live help overlay.

## Terminology

```text
Session (the herdr server, one per machine)
 └─ Workspace (one per repo or task)
     └─ Tab (a layout inside the workspace)
         └─ Pane (one running process: shell, claude, a log tail)
```

## Detach vs close vs kill

| Action | Keys | Effect on processes |
|---|---|---|
| Detach | `ctrl+b q` | Nothing dies. Server, workspaces, panes, agents keep running. This is "pause". |
| Close pane | `ctrl+b x` | Kills that one process. |
| Close tab | `ctrl+b shift+x` | Kills every pane in the tab. |
| Close workspace | `ctrl+b shift+d` | Kills every tab and pane in it. Asks first. |
| Stop server | `herdr server stop` | Kills everything. Only way to stop the server. |

Rule: for a long-running agent, always detach. Closing the tab kills the agent mid-task.

## Create and name

| Action | Keys |
|---|---|
| New workspace | `ctrl+b shift+n` |
| Rename workspace | `ctrl+b shift+w` |
| New tab | `ctrl+b c` |
| Rename tab | `ctrl+b shift+t` |
| Rename pane | `ctrl+b shift+p` |
| New git worktree | `ctrl+b shift+g` |
| Split right / down | `ctrl+b v` / `ctrl+b -` |

## Navigate

| Action | Keys |
|---|---|
| Workspace picker | `ctrl+b w` |
| Session navigator (all machines) | `ctrl+b g` |
| Jump to tab N | `ctrl+b 1`..`9` |
| Next / previous tab | `ctrl+b n` / `ctrl+b p` |
| Focus pane | `ctrl+b h/j/k/l` |
| Cycle panes | `ctrl+b tab` / `ctrl+b shift+tab` |

## Arrange and inspect

| Action | Keys |
|---|---|
| Swap pane with neighbor | `ctrl+b shift+h/j/k/l` |
| Resize mode | `ctrl+b r` then arrows |
| Zoom pane fullscreen | `ctrl+b z` |
| Toggle sidebar | `ctrl+b b` |
| Scrollback in `$EDITOR` | `ctrl+b e` |
| Copy mode | `ctrl+b [` |
| Settings | `ctrl+b s` |

Mouse works: click panes and tabs, drag borders, right-click for a menu.
