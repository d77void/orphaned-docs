# tmux and screen: terminals inside a terminal

**Packages:** `tmux`, `screen`

```sh
tmux                 # start a session
tmux new -s rescue   # … with a name
tmux ls              # sessions
tmux attach -t rescue
```

Inside tmux: `Ctrl+b` then `c` new window, `n`/`p` next/previous,
`%` and `"` split, `d` detach (the session keeps running).

Run long jobs (a `ddrescue` copy, an image hash) inside tmux: they survive
a closed terminal or an SSH connection that drops.

`screen` does the same with `Ctrl+a` instead of `Ctrl+b`
(`screen -S name`, `screen -ls`, `screen -r name`).
