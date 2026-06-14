# Mac-Studio-for-LLM
configure a raw Mac Studio for private local LLM

## Mac hardware configure
* `CPU` Apple M3 Ultra
* `MEM` Uniform memory: 256G
* `SSD` 2T

## Mac software configure
* `OS`  Tahoe 26.5

## Step 1: Install dependencies
### Install brew, uv, pnpm
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    brew install node
    brew install uv pnpm

### Install node and python
    pnpm env use --global lts
    uv python install
  or download installer from :https://www.python.org/downloads/macos/

### hf to manage model downloads from Hugging Face:
    brew install hf
    export HF_TOKEN="your_actual_token_here"
    hf auth login
    

### Claude Code:
    brew install --cask claude-code

## Step 2: Maximize GPU memory
* By default, macOS caps the GPU to 75% of total memory. 
* Set 6GB for operating system overhead 
* Set iogpu.wired_lwm_mb to 10GB to encourage memory reclamation and compression.
### Code:  
    TOTAL_MEMORY=$(($(sysctl -n hw.memsize) / 1024 / 1024))
    sudo sysctl -w iogpu.wired_limit_mb=$((TOTAL_MEMORY - 6144))
    sudo sysctl -w iogpu.wired_lwm_mb=$((TOTAL_MEMORY - 10240))

## Step 3: Configure MLX servers
### Start the MLX server:
    uv tool install mlx-lm
    mlx_lm.server --model "mlx-community/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-8bit"
By default, models are saved to ~/.cache/huggingface/hub.
