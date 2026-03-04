---
title: "Volatility 2 and 3 Install (Kali/Debian)"
slug: "volatility-install-kali"
category: "tools"
tool: "Volatility"
use_case: ["triage", "analysis"]
environment: ["linux"]
risk: "caution"
last_reviewed: "2026-03-03"
---

# Volatility 2 and 3 Install (Kali/Debian)

This page captures a practical install workflow for **Volatility 2 (Python 2.7)** and **Volatility 3 (Python 3)** on Kali/Debian-based systems.

## Notes and cautions

- Volatility 2 depends on **Python 2.7**, which is end-of-life. Use it only when you specifically need Vol2 plugins/workflows.
- Prefer Volatility 3 for most modern work.
- Run installs on a dedicated analysis VM when possible.

---

## Volatility 2 install

### 1) Install system dependencies

```bash
sudo apt install -y build-essential git libdistorm3-dev yara libraw1394-11 libcapstone-dev capstone-tool tzdata
sudo apt install -y python2 python2.7-dev libpython2-dev
sudo apt install -y curl
2) Install pip for Python 2.7
curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py
sudo python2 get-pip.py
3) Install Python packages
sudo python2 -m pip install -U setuptools wheel
python2 -m pip install -U distorm3 yara pycrypto pillow openpyxl ujson pytz ipython capstone
sudo python2 -m pip install yara
4) Create YARA library symlink (if needed)
sudo ln -s /usr/local/lib/python2.7/dist-packages/usr/lib/libyara.so /usr/lib/libyara.so
5) Install Volatility 2 from GitHub
python2 -m pip install -U git+https://github.com/volatilityfoundation/volatility.git
Volatility 3 install
1) Install system dependencies
sudo apt install -y python3 python3-dev libpython3-dev python3-pip python3-setuptools python3-wheel
2) Install Python packages
python3 -m pip install -U distorm3 yara pycrypto pillow openpyxl ujson pytz ipython capstone
3) Install Volatility 3 from GitHub
python3 -m pip install -U git+https://github.com/volatilityfoundation/volatility3.git
Add vol.py and related commands to your PATH

These steps make it easier to run Volatility commands by ensuring ~/.local/bin is on your PATH.

Replace username with your actual username.

bash (default on many systems)
echo 'export PATH=/home/username/.local/bin:$PATH' >> ~/.bashrc
. ~/.bashrc
fish
mkdir -p ~/.config/fish
echo 'set -x PATH /home/username/.local/bin $PATH' >> ~/.config/fish/config.fish
. ~/.config/fish/config.fish
ksh or sh
echo 'export PATH=/home/username/.local/bin:$PATH' >> ~/.profile
. ~/.profile
zsh
echo 'export PATH=/home/username/.local/bin:$PATH' >> ~/.zshrc
. ~/.zshrc
Quick verification (optional)

After install, confirm you can import the modules:

python2 -c "import volatility; print('Volatility2 import OK')"
python3 -c "import volatility3; print('Volatility3 import OK')"

If imports fail, re-check package installs and whether your environment is using the expected Python version.
