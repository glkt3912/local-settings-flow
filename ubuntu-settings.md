# Ubuntu Desktop 22.04 LTS Development(WSL2)

## WSL2(PowerShell)

### 「Linux 用 Windows サブシステム」 または 「Windows Subsystem for Linux」 を有効
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

### 「仮想マシン プラットフォーム」 を有効
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

wsl --install
wsl --set-default-version 2
wsl --list --online
wsl --install -d Ubuntu-22.04

## CLI Basic

sudo apt update
sudo apt upgrade

## zsh(default shell)

sudo apt install zsh
chsh -s $(which zsh)

## zprezto

git clone --recursive https://github.com/sorin-ionescu/prezto.git "${ZDOTDIR:-$HOME}/.zprezto"
touch ~/script/config-zprezto.sh
vim ~/script/config-zprezto.sh

```
setopt EXTENDED_GLOB
for rcfile in "${ZDOTDIR:-$HOME}"/.zprezto/runcoms/^README.md(.N); do
  ln -s "$rcfile" "${ZDOTDIR:-$HOME}/.${rcfile:t}"
done
```

chmod +x config-zprezto.sh

source ~/.zshrc

zsh ~/script/config-zprezto.sh

## curl

sudo apt install curl

## vim

sudo apt install vim

### ~/.vimrc

```
scriptencoding utf-8i
set encoding=utf-8

filetype plugin indent on
:set tabstop=2
:set shiftwidth=2
:set expandtab

cnoremap w!! w !sudo tee > /dev/null %<CR> :e!<CR>

set list
set listchars=tab:»-,trail:-,extends:»,precedes:«,nbsp
```

## node (nodenv + pnpm)

git clone https://github.com/nodenv/nodenv.git ~/.nodenv
echo 'export PATH="$HOME/.nodenv/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(nodenv init -)"' >> ~/.zshrc
source ~/.zshrc
nodenv -v