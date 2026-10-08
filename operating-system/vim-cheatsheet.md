# Vim Cheat Sheet (from `vimtutor`)

Part of the terminal notes: see [[terminal-cheatsheet]] and [[terminal-course]]. Run `vimtutor` in a terminal to practise.

Two modes: **Normal** (keys are commands, default) and **Insert** (typing text). `Esc` always returns to Normal. Pattern: **operator + motion** (`d` + `w` = delete word). Add a count: `3dw`, `2dd`.

| Goal | Keys |
| --- | --- |
| Move | `h` `j` `k` `l` (←↓↑→) · `w` next word · `b` back word · `0` line start · `$` line end |
| Jump | `gg` top · `G` bottom · `42G` line 42 · `%` matching bracket |
| Insert | `i` before cursor · `a` after · `A` end of line · `o` new line below · `O` above |
| Delete | `x` char · `dw` word · `d$` to end of line · `dd` line |
| Change | `cw` word · `r` one char · `R` overwrite mode |
| Copy / paste | `yy` copy line · `yw` copy word · `p` paste |
| Undo / redo | `u` undo · `Ctrl+R` redo |
| Search | `/text` then `n` next, `N` previous · `?text` backward |
| Replace | `:%s/old/new/g` whole file · add `c` to confirm each (`/gc`) |
| Select | `v` then move, then `d` / `y` / `c` |
| Save / quit | `:w` save · `:wq` save + quit · `:q!` quit, discard · `:w file` save as |
| Run shell cmd | `:!ls` |
| Help | `:help topic` |

## Survival set

Enough to edit any config over SSH:

```
i / Esc      insert / back to normal
dd           delete line
u            undo
/text  n     search, next match
:%s/a/b/g    replace all
:wq   :q!    save+quit / quit without saving
```

## Speedrun order for `vimtutor` (~10 min)

1. **Lesson 1:** `hjkl`, `x`, `i`, `A`, `Esc`, `:wq`, `:q!`
2. **Lesson 2:** `dw`, `d$`, `dd`, `u`, `Ctrl+R` (operator + motion)
3. **Lesson 3:** `p`, `r`, `cw`
4. **Lesson 4:** `gg`, `G`, `/text`, `n`, `%`
5. **Lesson 5:** `:%s/old/new/g`

Repeat on separate days (3 passes total); do lessons 5-7 properly on the second pass. For harder practice, try Vim Golf (vimgolf.com).
