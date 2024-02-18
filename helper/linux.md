---
tags: cheatshee. 
---
# Symlink
- Create symlink to a file
```
ln -s existing_source_file optional_symbolic_link
```
- Example, create a symlink of file `.zshrc` from `~/dotfiles/.zshrc` to `~/`
```
ln -s ~/dotfiles/.zshrc ~/
```
# Permission
- Make the script executable
```
chmod +x my_script.sh
```
- Run the script
```
bash my_script.sh
```