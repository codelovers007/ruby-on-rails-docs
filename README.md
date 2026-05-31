# 💎 Ruby on Rails Installation Guide with RVM

> A complete step-by-step guide to installing **Ruby on Rails** using **RVM (Ruby Version Manager)** on macOS, Linux, and Windows (WSL 2).

---

## 📋 Table of Contents

- [What is RVM?](#what-is-rvm)
- [macOS](#-macos)
- [Linux](#-linux)
- [Windows (WSL 2)](#-windows-wsl-2)
- [Pro Tips](#-pro-tips)

---

## What is RVM?

**Ruby Version Manager (RVM)** is a command-line tool that lets you install, manage, and switch between multiple Ruby versions on the same machine. It also provides **gemsets** — isolated collections of gems per project — so dependencies never conflict across applications.

---

## 🍎 macOS

> Tested on macOS Ventura, Sonoma, and Sequoia

### Prerequisites

**Step 1 — Install Xcode Command Line Tools**

```bash
xcode-select --install
```

> Accept the licence prompt when it appears. Skip if already installed.

---

**Step 2 — Install Homebrew** *(recommended)*

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

> 💡 On Apple Silicon, run the `eval` command printed by the Homebrew installer to add it to your PATH.

---

**Step 3 — Install RVM dependencies via Homebrew**

```bash
brew install gnupg libgpg-error openssl readline libyaml
```

---

### Install RVM

**Step 4 — Import GPG keys**

```bash
gpg --keyserver keyserver.ubuntu.com --recv-keys \
  409B6B1796C275462A1703113804BB82D39DC0E3 \
  7D2BAF1CF37B13E2069D6956105BD0E739499BDB
```

> If the keyserver is unreachable, try: `curl -sSL https://rvm.io/mpapis.asc | gpg --import -`

---

**Step 5 — Install RVM**

```bash
\curl -sSL https://get.rvm.io | bash -s stable
```

---

**Step 6 — Load RVM into your shell session**

```bash
source ~/.rvm/scripts/rvm
```

> 💡 Add this line to `~/.zshrc` (or `~/.bash_profile` for Bash) so RVM loads automatically every time you open a new terminal.

---

### Install Ruby

**Step 7 — Install the latest stable Ruby**

```bash
rvm install ruby --latest
rvm use ruby --default
```

**Step 8 — Verify the installation**

```bash
ruby -v     # e.g. ruby 3.3.x
rvm list    # shows all installed versions
```

---

### Install Rails

**Step 9 — Install the Rails gem**

```bash
gem install rails
rails -v    # e.g. Rails 7.x.x
```

---

**Step 10 — Create your first Rails application**

```bash
rails new myapp
cd myapp
rails server
```

Open [http://localhost:3000](http://localhost:3000) in your browser — you should see the Rails welcome page. 🎉

---

## 🐧 Linux

> Ubuntu 22.04 / 24.04 · Debian · Fedora / RHEL

### Prerequisites

**Step 1 — Update packages and install build dependencies**

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl gnupg2 build-essential \
  libssl-dev libreadline-dev zlib1g-dev \
  libsqlite3-dev nodejs yarn
```

> For Fedora / RHEL, substitute `apt` with `dnf` and adjust package names: e.g. `openssl-devel`, `readline-devel`, `zlib-devel`.

---

### Install RVM

**Step 2 — Import GPG keys**

```bash
gpg --keyserver keyserver.ubuntu.com --recv-keys \
  409B6B1796C275462A1703113804BB82D39DC0E3 \
  7D2BAF1CF37B13E2069D6956105BD0E739499BDB
```

---

**Step 3 — Install RVM**

```bash
\curl -sSL https://get.rvm.io | bash -s stable
```

---

**Step 4 — Load RVM into the current shell**

```bash
source ~/.rvm/scripts/rvm
```

> 💡 Add this to `~/.bashrc` or `~/.zshrc` so it loads automatically on every new terminal session.

---

### Install Ruby & Rails

**Step 5 — Install Ruby**

```bash
rvm install ruby --latest
rvm use ruby --default
ruby -v
```

**Step 6 — Install Rails**

```bash
gem install rails
rails -v
```

**Step 7 — Create your first Rails application**

```bash
rails new myapp
cd myapp
gem install bundler
bundle install
rake db:create
rake db:migrate
rails server
```

Visit [http://localhost:3000](http://localhost:3000) to confirm Rails is running. 🎉

---

## 🪟 Windows (WSL 2)

> ⚠️ **RVM is not natively supported on Windows.** The recommended approach is to use **WSL 2** (Windows Subsystem for Linux), which gives you a full Ubuntu environment with complete RVM support. Requires Windows 10 version 2004+ or Windows 11.

---

### Step 1 — Enable WSL 2

**Step 1 — Open PowerShell as Administrator and run**

```powershell
wsl --install
```

> This installs WSL 2 and Ubuntu by default. **Restart your computer** when prompted.

---

**Step 2 — Verify WSL version**

```powershell
wsl --list --verbose
```

> Confirm your distro shows `VERSION 2`. If not, run: `wsl --set-default-version 2`

---

### Step 2 — Inside your WSL Ubuntu terminal

**Step 3 — Install build dependencies**

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl gnupg2 build-essential \
  libssl-dev libreadline-dev zlib1g-dev \
  libsqlite3-dev nodejs yarn
```

---

**Step 4 — Import GPG keys**

```bash
gpg --keyserver keyserver.ubuntu.com --recv-keys \
  409B6B1796C275462A1703113804BB82D39DC0E3 \
  7D2BAF1CF37B13E2069D6956105BD0E739499BDB
```

---

**Step 5 — Install RVM and load it**

```bash
\curl -sSL https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
```

---

### Step 3 — Install Ruby & Rails

**Step 6 — Install Ruby**

```bash
rvm install ruby --latest
rvm use ruby --default
ruby -v
```

**Step 7 — Install Rails**

```bash
gem install rails
rails -v
```

**Step 8 — Create your first Rails application**

```bash
rails new myapp
cd myapp
rails server
```

Open [http://localhost:3000](http://localhost:3000) in your Windows browser to see the Rails welcome page. 🎉

> 💡 Install **Windows Terminal** from the Microsoft Store for the best WSL experience. **VS Code's Remote - WSL** extension also integrates seamlessly.

---

## 🧠 Pro Tips

### RVM Gemsets — isolate per-project dependencies

Gemsets prevent gem version conflicts between projects.

```bash
rvm gemset create myapp
rvm gemset use myapp
rvm gemset list          # see all gemsets
rvm gemset delete myapp  # remove a gemset
```

---

### Pin Ruby version per project

A `.ruby-version` file in your project root tells RVM which version to use automatically when you `cd` into the directory.

```bash
echo '3.3.0' > .ruby-version
```

---

### Install a specific Ruby version

```bash
rvm install 3.2.2
rvm use 3.2.2
rvm list           # see all installed versions
rvm list known     # see all available versions
```

---

### Using Bundler with Rails

Bundler manages gem dependencies declared in your `Gemfile`.

```bash
bundle install        # install all gems from Gemfile
bundle exec rails s   # run rails within the bundle
bundle update         # update gems to latest allowed versions
```

---

### GPG key troubleshooting

If the keyserver is unreachable, import keys directly from rvm.io:

```bash
curl -sSL https://rvm.io/mpapis.asc | gpg --import -
curl -sSL https://rvm.io/pkuczynski.asc | gpg --import -
```

---

### Update RVM itself

Keep RVM up to date to get the latest Ruby versions and bug fixes:

```bash
rvm get stable
rvm reload
```

---

## 📚 Useful Links

| Resource | URL |
|----------|-----|
| RVM Official Site | https://rvm.io |
| Ruby Downloads | https://www.ruby-lang.org/en/downloads |
| Rails Guides | https://guides.rubyonrails.org |
| Homebrew | https://brew.sh |
| WSL 2 Setup | https://learn.microsoft.com/en-us/windows/wsl/install |

### Install OpenSSL 3
```bash
brew install openssl@3
rvm install 3.0.0 --with-openssl-dir=$(brew --prefix openssl@3)
```
---

> Made with ❤️ — covers macOS, Linux, and Windows (WSL 2)
