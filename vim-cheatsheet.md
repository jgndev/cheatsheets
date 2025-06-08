# Vim & Neovim Cheatsheet

## Installation

### Vim
- **macOS**: `brew install vim`
- **Ubuntu/Debian**: `sudo apt-get install vim`
- **Fedora**: `sudo dnf install vim`
- **Windows**: [Download from vim.org](https://www.vim.org/download.php)

### Neovim
- **macOS**: `brew install neovim`
- **Ubuntu/Debian**: `sudo apt-get install neovim`
- **Fedora**: `sudo dnf install neovim`
- **Windows**: [Download from neovim.io](https://neovim.io/)

---

## Opening Files

| Command | Description |
|---------|-------------|
| `vim file.txt` | Open file.txt in Vim |
| `nvim file.txt` | Open file.txt in Neovim |
| `vim +42 file.txt` | Open file.txt at line 42 |
| `vim +/pattern file.txt` | Open file.txt at the first occurrence of 'pattern' |
| `vim +/word +42 file.txt` | Open file.txt at line 42, then search for 'word' |
| `vim +"normal! G" file.txt` | Open file.txt at the end of the file |
| `vim +"normal! gg" file.txt` | Open file.txt at the start of the file |

- You can use the same commands with `nvim` instead of `vim` for Neovim.

---

## Useful Startup Options

| Option | Description |
|--------|-------------|
| `-R` | Open in read-only mode |
| `-u NONE` | Start with no config |
| `-O` | Open files in vertical splits (e.g., `vim -O file1 file2`) |
| `-o` | Open files in horizontal splits |

---

## Quick Navigation (once inside Vim/Neovim)

| Command | Description |
|---------|-------------|
| `:42` | Go to line 42 |
| `/word` | Search for 'word' |
| `gg` | Go to the first line |
| `G` | Go to the last line |
| `n` | Next search result |
| `N` | Previous search result |

### Common Motions

| Command | Description |
|---------|-------------|
| `h` | Move left |
| `j` | Move down |
| `k` | Move up |
| `l` | Move right |
| `w` | Jump forward to the start of the next word |
| `b` | Jump backward to the start of the previous word |
| `e` | Jump forward to the end of the word |
| `0` | Go to the beginning of the line |
| `^` | Go to the first non-blank character of the line |
| `$` | Go to the end of the line |
| `f<char>` | Move to the next occurrence of <char> on the line |
| `F<char>` | Move to the previous occurrence of <char> on the line |
| `t<char>` | Move before the next occurrence of <char> on the line |
| `T<char>` | Move before the previous occurrence of <char> on the line |
| `gg` | Go to the first line of the file |
| `G` | Go to the last line of the file |
| `}` | Jump to next paragraph or block |
| `{` | Jump to previous paragraph or block |
| `%` | Jump to matching bracket/parenthesis |

---

## Resources
- [Vim Documentation](https://vimhelp.org/)
- [Neovim Documentation](https://neovim.io/doc/) 