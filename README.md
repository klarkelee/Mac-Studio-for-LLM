# Mac-Studio-for-LLM
configure a raw Mac Studio for private local LLM

## Mac hardware configure
* `CPU` Apple M3 Ultra
* `MEM` Uniform memory: 256G
* `SSD` 2T

## Mac software configure
* `OS`  Tahoe 26.5

## Step 1: 
### Install brew, uv, pnpm
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install uv pnpm

### Install node and python
pnpm env use --global lts
uv python install
