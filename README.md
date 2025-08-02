# Contract Signing Starter

This repository contains the public setup files needed to start the Therry LLC contract signing process.

## Quick Start

### For Claude Code Users (Recommended)

1. Create a new folder for the signing session:
   ```bash
   mkdir ~/Desktop/TherryContractSigning
   cd ~/Desktop/TherryContractSigning
   ```

2. Download the settings file:
   ```bash
   curl -O https://raw.githubusercontent.com/matznerd/contract-signing-starter/main/contract-signing-settings.json
   ```

3. Start Claude Code with the settings:
   ```bash
   claude --settings contract-signing-settings.json
   ```

4. Type `init` to begin the signing process.

Claude will guide you through:
- Installing prerequisites (GitHub CLI, GPG)
- Setting up authentication
- Cloning the private contract repository
- Completing the digital signature

### Manual Setup

If you prefer to set up manually:

1. **Install Prerequisites:**
   ```bash
   # macOS
   brew install gh gnupg
   
   # Ubuntu/Debian
   sudo apt-get install gh gnupg
   ```

2. **Authenticate with GitHub:**
   ```bash
   gh auth login
   ```

3. **Create GPG Key:**
   ```bash
   gpg --gen-key
   # Follow prompts, use your legal name as it appears in contracts
   ```

4. **Configure Git Signing:**
   ```bash
   git config --global commit.gpgsign true
   git config --global user.signingkey YOUR_KEY_ID
   ```

5. **Fetch the Contract:**
   ```bash
   ./fetch-private-contract.sh
   ```

## What's Included

- **contract-signing-settings.json** - Claude Code hooks configuration
- **INIT-CLAUDE.md** - Detailed instructions for Claude
- **README.md** - This file with simple human instructions
- **fetch-private-contract.sh** - Script to get the private contract repo

## Security & Legal

- This creates **legally binding digital signatures**
- Your GPG key acts as your digital identity
- All signatures are cryptographically verifiable
- Complete audit trail via Git commits

## Prerequisites

- **Node.js** (v16+)
- **Git** with your identity configured
- **GitHub CLI** authenticated to access TherryApp repositories
- **GPG** key for digital signatures

## Support

For issues:
- Technical problems: [Contract Signing App Issues](https://github.com/matznerd/ContractSigningApp/issues)
- Legal questions: Consult your legal counsel

## Repository Structure

This starter contains only public setup files. The actual contracts are stored in private repositories:

- **Public Setup**: `contract-signing-starter` (this repo)
- **Private Contracts**: `TherryApp/TherryOperatingAgreement` (accessed after authentication)
- **Signing Engine**: `matznerd/ContractSigningApp` (automatically cloned)

## Process Overview

1. **Setup Phase**: Install tools, create GPG key, authenticate
2. **Access Phase**: Clone private contract repository
3. **Review Phase**: Read the complete contract
4. **Signing Phase**: Apply your digital signature
5. **Submission Phase**: Create pull request for review

## Important Notes

- ⚠️ **This process creates legally binding agreements**
- 🔐 **Your GPG passphrase secures your digital identity**
- 📝 **Type your legal name exactly as it appears in the contract**
- 🧑‍⚖️ **For legal questions about contract terms, consult counsel**