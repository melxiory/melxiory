<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com/?font=Fira+Code&size=28&duration=2800&pause=2000&color=CC785C&center=true&vCenter=true&width=600&height=70&lines=Claude+Code+Account+Switcher;Shell+Script" alt="Typing SVG" />
</p>

<div align="center">

![Bash](https://img.shields.io/badge/Bash-5.0+-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)
![Claude Code](https://img.shields.io/badge/Claude%20Code-Supported-CC785C?style=for-the-badge&logo=anthropic&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-macOS_WSL-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

</div>

---

## 📋 Overview

A convenient **Bash script** for switching between multiple **Claude Code** accounts and configurations. Perfect for developers who use different Claude accounts for different projects or clients.

### Key Features

- 🔄 **Quick Account Switching** with a single command
- ⚙️ **Configuration Profiles** for different setups
- 🛡️ **Safe Storage** of credentials (locally encrypted)
- 📝 **Session History** tracking
- 🎯 **Auto-completion** support
- 💻 **Cross-platform** (Linux, macOS, WSL)
- 🔒 **No credentials in source** - uses encrypted config

---

## 🚀 Tech Stack

| Component | Technology |
|-----------|------------|
| **Language** | Bash 5.0+ |
| **Encryption** | OpenSSL |
| **Config Storage** | JSON/YAML |
| **Compatibility** | Linux, macOS, WSL |

---

## 📦 Installation

### Prerequisites

- Bash 5.0 or higher
- OpenSSL (for credential encryption)
- jq (for JSON parsing)

### Step 1: Clone the Repository

```bash
git clone https://github.com/melxiory/cc-account-switcher.git
cd cc-account-switcher
```

### Step 2: Make Script Executable

```bash
chmod +x cc-switch.sh
```

### Step 3: Install Dependencies

```bash
# Ubuntu/Debian
sudo apt-get install openssl jq

# macOS
brew install openssl jq

# Fedora
sudo dnf install openssl jq
```

### Step 4: Setup Initial Configuration

```bash
./cc-switch.sh setup
```

---

## 📁 Project Structure

```
cc-account-switcher/
├── cc-switch.sh             # Main switcher script
├── lib/                     # Library functions
│   ├── config.sh           # Configuration management
│   ├── crypto.sh           # Encryption utilities
│   └── validator.sh        # Input validation
├── config/                  # Configuration directory
│   ├── accounts.json       # Encrypted account storage
│   └── profiles/           # Profile configurations
│       ├── default.json
│       └── work.json
├── scripts/                 # Additional scripts
│   ├── install.sh          # Installation script
│   └── uninstall.sh        # Uninstallation script
├── completion/              # Shell completions
│   ├── bash_completion.sh
│   └── zsh_completion.zsh
└── README.md
```

---

## 🎯 Usage

### Basic Commands

```bash
# List all available accounts
./cc-switch.sh list

# Switch to an account
./cc-switch.sh switch <account_name>

# Add a new account
./cc-switch.sh add

# Remove an account
./cc-switch.sh remove <account_name>

# Show current account
./cc-switch.sh current

# Setup wizard
./cc-switch.sh setup
```

### Interactive Mode

```bash
./cc-switch.sh
# or
./cc-switch.sh interactive
```

### Examples

```bash
# Switch to work account
./cc-switch.sh switch work

# Switch to personal account
./cc-switch.sh switch personal

# Add a new client account
./cc-switch.sh add
# Follow the prompts to enter account details

# List all accounts with details
./cc-switch.sh list --verbose
```

---

## ⚙️ Configuration

### Account Configuration Format

```json
{
  "accounts": {
    "default": {
      "name": "Default Account",
      "api_key": "encrypted_api_key_here",
      "endpoint": "https://api.anthropic.com",
      "model": "claude-3-opus",
      "timeout": 120
    },
    "work": {
      "name": "Work Account",
      "api_key": "encrypted_api_key_here",
      "endpoint": "https://api.anthropic.com",
      "model": "claude-3-sonnet",
      "timeout": 60
    }
  },
  "current": "default"
}
```

### Environment Variables

```bash
# Override default config location
export CC_CONFIG_DIR="$HOME/.config/cc-switcher"

# Set default account
export CC_DEFAULT_ACCOUNT="default"

# Enable verbose logging
export CC_DEBUG=1
```

---

## 🔒 Security

### Credential Encryption

The script uses **OpenSSL AES-256-CBC** encryption for storing API keys:

```bash
# Encryption happens automatically
# Keys are never stored in plain text

# Encryption command (internal)
openssl enc -aes-256-cbc -salt -in "$plain_key" -out "$encrypted_key" -pass pass:"$master_password"
```

### Security Best Practices

- ✅ API keys encrypted with AES-256
- ✅ Master password for decryption
- ✅ File permissions: 600 (user read/write only)
- ✅ No credentials in shell history
- ✅ Secure temporary file handling

---

## 🔧 Installation Options

### System-wide Installation

```bash
sudo ./scripts/install.sh --system
```

This installs to:
- Binary: `/usr/local/bin/cc-switch`
- Config: `/etc/cc-switcher`
- Completions: `/usr/share/bash-completion/completions/cc-switch`

### User Installation

```bash
./scripts/install.sh --user
```

This installs to:
- Binary: `~/.local/bin/cc-switch`
- Config: `~/.config/cc-switcher`
- Completions: `~/.local/share/bash-completion/completions/cc-switch`

### Manual Installation

Add to your `~/.bashrc` or `~/.zshrc`:

```bash
# Add cc-switch to PATH
export PATH="$PATH:/path/to/cc-account-switcher"

# Enable auto-completion
source /path/to/cc-account-switcher/completion/bash_completion.sh
```

---

## 🎪 Shell Integration

### Bash Completion

Enable tab completion by adding to `~/.bashrc`:

```bash
source /path/to/cc-account-switcher/completion/bash_completion.sh
```

### Zsh Completion

Add to `~/.zshrc`:

```bash
source /path/to/cc-account-switcher/completion/zsh_completion.zsh
```

### Aliases (Optional)

```bash
# Add to ~/.bashrc or ~/.zshrc
alias ccs='cc-switch'
alias ccsl='cc-switch list'
alias ccsi='cc-switch interactive'
```

---

## 📊 Usage Examples

### Scenario 1: Work vs Personal

```bash
# At work
cc-switch work
# Now using work account with corporate API key

# At home
cc-switch personal
# Now using personal account
```

### Scenario 2: Client Projects

```bash
# Switch to client-specific configuration
cc-switch client-acme
cc-switch client-startup
cc-switch client-enterprise
```

### Scenario 3: Quick Switching with Aliases

```bash
# Add to ~/.bashrc
alias ccwork='cc-switch work && cd ~/work'
alias cchome='cc-switch personal && cd ~/personal'

# Now you can:
ccwork   # Switches to work account and changes directory
cchome   # Switches to personal account and changes directory
```

---

## 🐛 Troubleshooting

### Permission Denied

```bash
chmod +x cc-switch.sh
```

### OpenSSL Not Found

```bash
# Ubuntu/Debian
sudo apt-get install openssl

# macOS
brew install openssl
```

### jq Not Found

```bash
# Ubuntu/Debian
sudo apt-get install jq

# macOS
brew install jq
```

### Decryption Fails

```bash
# Reset and reconfigure
./cc-switch.sh reset
./cc-switch.sh setup
```

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**melxiory**

- GitHub: [@melxiory](https://github.com/melxiory)

---

## 🙏 Acknowledgments

- [Claude Code](https://claude.ai/claude-code) - AI-powered CLI tool
- [Bash](https://www.gnu.org/software/bash/) - GNU Bourne-Again SHell

---

## ⚠️ Disclaimer

This tool is not officially affiliated with Anthropic or Claude Code. Use at your own risk. Always follow your organization's security policies when managing API keys.

---

<div align="center">

### 🌟 Star this repo if it helped you!

[![GitHub stars](https://img.shields.io/github/stars/melxiory/cc-account-switcher?style=social)](https://github.com/melxiory/cc-account-switcher/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/melxiory/cc-account-switcher?style=social)](https://github.com/melxiory/cc-account-switcher/network/members)

</div>
