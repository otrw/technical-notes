# Basic `vim` use

## Editing
- Jumpt to the start of the next word `w`
- Jump to the end of a word `e`
- Jump backwards by word `b`
- Insert (before the cursor) `i`
- Insert (at the beginning of a line) `I`
- Append (after the cursor) `a`
- Append at the end of a line `A`
- New Line under the current line `o`
## Saving
- Write, don't exit `:w`
- Write, don't exit, as root `:w !sudo tee %`
- Write and Quit `:wq` or `ZZ`
- Quit `:q`
- Force Quit (Do not save) `:q!`
- Save, Quit & Close Active tabs `:wqa`
## Copy, Cut & Paste
- Copy (yank) a line `yy`
- Copy 2 lines `2yy`
- Copy to the end of the line `y$`
- Paste (put) after the cursor `p`
- Paste before the cursor `P`
- Cut a line `dd`
- Cut 2 lines `2dd`
- Cut to the end of the line `D`
- Cut a character `x`
## Searching
- Search forward for a pattern `/pattern`
- Search backwards for a pattern `?pattern`
- Repeat the search in the same direction `n`
- Repeat the search in the opposite direction `N`
- Search & Replace `:%s/old/new/g`
- Use `grep` with `:vimgrep`

## Resources
- [Online Vim Cheat Sheet](https://vim.rtorr.com/)
- In `Vim` use `:vimtutor`
- `vimrc` example can be found in the `configs` directory


