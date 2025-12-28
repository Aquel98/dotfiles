Requirements: stow installed (sudo apt install stow)

This repository is designed to use the GNU stow feature which creates SYM-links from the original location Of the files to the location within their package directory in this repo. It is important that the file structure in the directory that will become a package reflects any file strucre that may have existed between the $$HOME-dir and the moved file.
For example: to move the nvim-dir from the .config-dir (/home/<username>/.config/nvim) to the dotfiles-repo (/home/<username>/dotfiles) we first want to create a directory in the dotfiles repo that can be turned into a package, /home/<username>/dotfiles/neovim. In the 'neovim'-dir we recreate the file structure as seen from the $$HOME-dir, that is we make it: /home/<username>/dotfiles/neovim/.config/nvim/. Then we can move the existing nvim-dir to the new one:
cd
mv .config/nvim dotfiles/neovim/.config/nvim
Now with the nvim-dir moved we can create a SYM-link to its new location by running the command:
cd dotfiles
stow --target=/home/<username>/ neovim
You can now double check that a SYM-link was actually created by going to /home/<username>/.config/ and running "ls"

If the file you wanted to move to dotfiles was simply residing directly in $$HOME, as .bashrc might, then you simply create a new directory in dotfiles, e.g. /home/<username>/dotfiles/bash. Move the file there:
cd 
mv .bashrc dotfiles/bash
Go to dotfiles and create a new symnlink:
cd dotfiles
stow --target=/home/<username>/ bash

A makefile has been created to streamline this process, it takes all the directories in dotfiles and tries to create a symlink in $$HOME for them, it also removed unused SYM-links.
make all (refresh SYM-links)
make delete (delete SYM-links)
