# The command-line on Bianca

!!! info "Objectives"
    - Tips and tricks for Bianca users


## Aliases on your desktop

1. Be logged in with ThinLinc.
2. Open a terminal.
3. Run `cd Desktop\`
4. Make shortcuts to your heart's content:
  - `PROJ=sens2023531`
  - `ln -s /proj/$PROJ/ proj`
  - `ln -s /proj/$PROJ/nobackup nobackup`
  - `ln -s /proj/$PROJ/nobackup/wharf/<yourusername>/<yourusername-$PROJ> wharf`

You can also make aliases to executables, like the convenient `interactive`-job starting script in `proj/useful_files`.

## The terminal and the GUI are friends

On a clean terminal, try typing `cd` and then dragging a folder from the GUI to the terminal.

It types the absolute path for you!

## Use `chmod` to protect important files

Most projects rely on data that should in principle never be changed. Run `chmod -R -w data/` to remove write permissions on everything inside the `data` directory. 

Note that e.g. `rm --force` can still delete files, and you can overwrite or delete data by confirming when Bash prompts (if you own the files). However, this will protect you from most programmatic mistakes, the mistakes of others, and give you an opportunity to regret a typo.

Some people use an alias for `rm` that causes it to always prompt for confirmation. I don't recommend this because it detracts from the effectiveness of write-protecting your own files.
