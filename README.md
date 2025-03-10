# Whisper for IWSLT low resource

## Results

### BigC S2TT
| BLEU    | Model | Language Token | Beam Size | Temperature |
|---------|-------|--------------- |-----------|-------------|
|   | large | sw             | 0         | 0.2         |

### BembaSpeech ASR
| WER     | Model | Language Token | Beam Size | Temperature |
|---------|-------|--------------- |-----------|-------------|
| 1.3467  | turbo | none           | 0         | 0.0         |
| 1.1781  | turbo | sw             | 0         | 0.0         |
| 1.0453  | large | sw             | 0         | 0.0         |
| 1.0444  | large | sw             | 0         | 0.2         |

### BigC ASR
| WER    | Model | Language Token | Beam Size | Temperature |
|---------|-------|--------------- |-----------|-------------|
|   | large | sw             | 0         | 0.2         |


## Setup

### Environment
```shell
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
chmod +x Miniconda3-latest-Linux-x86_64.sh
./Miniconda3-latest-Linux-x86_64.sh
# answer yes to terms and to automatically setting up Miniconda
# reopen terminal
conda deactivate
conda create -n whisper python=3.10
conda activate whisper
```
### Repo

    pip install git+https://github.com/Alexgichamba/whisper.git 

To update the package to the latest version of this repository, please run:

    pip install --upgrade --no-deps --force-reinstall git+https://github.com/Alexgichamba/whisper.git

It also requires the command-line tool [`ffmpeg`](https://ffmpeg.org/) to be installed on your system, which is available from most package managers:

```bash
# on Ubuntu or Debian
sudo apt update && sudo apt install ffmpeg

# on Arch Linux
sudo pacman -S ffmpeg

# on MacOS using Homebrew (https://brew.sh/)
brew install ffmpeg

# on Windows using Chocolatey (https://chocolatey.org/)
choco install ffmpeg

# on Windows using Scoop (https://scoop.sh/)
scoop install ffmpeg
```

You may need [`rust`](http://rust-lang.org) installed as well, in case [tiktoken](https://github.com/openai/tiktoken) does not provide a pre-built wheel for your platform. If you see installation errors during the `pip install` command above, please follow the [Getting started page](https://www.rust-lang.org/learn/get-started) to install Rust development environment. Additionally, you may need to configure the `PATH` environment variable, e.g. `export PATH="$HOME/.cargo/bin:$PATH"`. If the installation fails with `No module named 'setuptools_rust'`, you need to install `setuptools_rust`, e.g. by running:

```bash
pip install setuptools-rust
```


## Evaluate
First generate the task specific files. For bembaspeech, this is done using:
```shell
python3 iwslt/utils/dataprep_bembaspeech.py
```

You can then run inference on the test set using:
```shell
python3 iwslt/evaluate/run_eval.py --data corpora/test 
```

## License

Whisper's code and model weights are released under the MIT License. See [LICENSE](https://github.com/openai/whisper/blob/main/LICENSE) for further details.
