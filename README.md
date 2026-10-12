# Using Linux Help Commands: man, whatis, and apropos

> **Disclaimer:** This project was completed as part of the Google Cybersecurity Certificate (Coursera). The scenario comes from the course. The commands, outputs, and explanations are my own documentation of the work I performed.

## Project description
As a security analyst, you won't have every answer memorized, but you need to know where to find them. In this project, I used Linux's built-in help tools to look up what commands do, find the right option for a task, compare similar commands, and discover which command to use when I didn't know its name. These skills let an analyst work independently on the command line without relying on outside resources.

## Commands Used
| Command | Purpose |
|---|---|
| `whatis` | Show a short, one-line description of a command |
| `man` | Open the full manual page for a command, including all options |
| `apropos` | Search manual pages by keyword to find a command |
| `apropos -a` | Same as `apropos`, but only returns results that match all keywords |

## Learn more about commands
**Get a quick reminder of what `cat` does.** `whatis` returns a one-line description:

```bash
whatis cat
```
Output:
```
cat (1)    - concatenate files and print on the standard output
```

**Get full details and every option for `cat`.** `man` opens the manual page, which shows the synopsis, description, and each option:

```bash
man cat
```
From the manual page, `-n, --number` numbers all output lines. (`-b, --number-nonblank` numbers only nonempty lines and overrides `-n`.) Press `Q` to exit a manual page.

**Find a command by describing what it does.** I couldn't remember the command that prints the first part of a file, so I searched by keyword with `apropos`. The `-a` option limits results to commands that match all keywords:

```bash
apropos -a first part file
```
Output:
```
head (1)    - output the first part of files
```
The command is `head`.

## Explore the useradd command
To set an expiration date on a temporary user account, I needed to find the right option for `useradd`. I opened its manual page:

```bash
man useradd
```
The manual describes `useradd` as a command to "create a new user or update default new user information," and lists every option it accepts. The option for setting an account expiration date is `-e` (`--expiredate`).

## Explore the rm and rmdir commands
To understand the difference between `rm` and `rmdir`, I used `whatis` on each one for a quick comparison:

```bash
whatis rm
whatis rmdir
```
Output:
```
rm (1)       - remove files or directories
rmdir (1)    - remove empty directories
```
`rm` removes files or directories, while `rmdir` removes only empty directories. That makes `rmdir` the safer choice, because it refuses to delete a directory that still has contents.

## Determine which command to use
I needed to create a new group but couldn't remember the command, so I searched with the keywords "create new group":

```bash
apropos -a create new group
```
Output:
```
groupadd (8)    - create a new group
```
The command is `groupadd`.

## Full Command Sequence
```bash
whatis cat
man cat
apropos -a first part file
man useradd
whatis rm
whatis rmdir
apropos -a create new group
```

## Summary
I used `whatis` for quick command descriptions, `man` for full documentation and options, and `apropos` to find commands by keyword. With these, I identified the `-n` option for `cat`, found `head` as the command that outputs the first part of a file, located the `-e` option for setting a `useradd` expiration date, compared `rm` and `rmdir`, and found `groupadd` for creating groups. Knowing how to find answers directly in the shell makes me faster and more self-sufficient as a security analyst.

## Key Takeaways
- `whatis` is best for a fast reminder, and `man` is best when you need every option and detail.
- `apropos` finds a command when you only know what it does. Using `-a` narrows the results to commands matching all of your keywords, which cuts out a lot of noise.
- Without `-a`, `apropos` returns every page matching any keyword, which can be hundreds of results.
- Manual pages show one page at a time. Use the space bar for the next page, Enter for the next line, and `Q` to quit.
- The number in parentheses, like `(1)` or `(8)`, is the manual section: user commands are in section 1 and system administration commands like `useradd` and `groupadd` are in section 8.
- `rm` and `rmdir` both delete, but `rmdir` only works on empty directories, so it protects against accidental data loss.
