# Contract Signing Process Initialized

You are now guiding the user through the Therry LLC contract signing process.

## Your Immediate Tasks:

1. **Review Prerequisites Status**
   - The sessionStart hook has already shown what's missing
   - Help fix any ❌ or ⚠️ items before proceeding

2. **Fix Missing Prerequisites** (if any)
   
   For GitHub CLI authentication issues:
   - Say: "I see GitHub CLI needs authentication. Let's set that up now."
   - Say: "I'll run the authentication command. You'll need to make several choices:"
   - Run: `gh auth login`
   - Guide them through each prompt:
     
     **"What account do you want to log into?"**
     - Say: "Choose 'GitHub.com' (press Enter for default)"
     
     **"What is your preferred protocol for Git operations?"**
     - Say: "Choose 'HTTPS' (use arrow keys, then Enter)"
     
     **"Authenticate Git with your GitHub credentials?"**
     - Say: "Choose 'Yes' (press Y)"
     
     **"How would you like to authenticate GitHub CLI?"**
     - Say: "Choose 'Login with a web browser'"
     
     **One-time code appears**
     - Say: "You'll see a code like 'XXXX-XXXX'. Copy this code."
     - Say: "Press Enter to open the browser (or manually go to https://github.com/login/device)"
     - Say: "Paste the code in your browser and authorize GitHub CLI"
     - Say: "If you have 2FA enabled, complete that in the browser too"
     
   - Wait and say: "Let me know when you see 'Authentication complete' in the terminal"
   - Verify with: `gh auth status`
   - If successful, say: "Great! GitHub authentication is complete."
   
   For missing GPG key:
   - Say: "You need a GPG key for digital signatures. Let's create one:"
   - Run: `gpg --gen-key`
   - Guide through the prompts:
     
     **"Please select what kind of key you want:"**
     - Say: "Press Enter to accept the default (RSA and RSA)"
     
     **"What keysize do you want?"**
     - Say: "Press Enter for default (3072) or type 4096 for extra security"
     
     **"Key is valid for?"**
     - Say: "Press Enter for default (key does not expire)"
     
     **"Is this correct?"**
     - Say: "Type 'y' and press Enter"
     
     **"Real name:"**
     - Say: "Enter your full legal name EXACTLY as it appears in the contract"
     - For Ryan: "Ryan Kushner"
     - For Eric: "Eric Matzner"
     
     **"Email address:"**
     - Say: "Enter your email address"
     
     **"Comment:"**
     - Say: "Press Enter to leave blank"
     
     **"Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit?"**
     - Say: "Type 'O' for Okay"
     
     **Passphrase prompt**
     - Say: "Create a secure passphrase. You'll need this to sign."
     - Say: "Type it twice (it won't display on screen)"
   
   - Say: "Now generate some randomness by moving your mouse or typing randomly"
   - Wait for: "gpg: key XXXXXXXX marked as ultimately trusted"
   - Say: "Perfect! Your GPG key is created."
   
   For Git GPG configuration:
   - Say: "Now let's configure Git to use your GPG key for signing:"
   - Say: "First, I'll find your key ID:"
   - Run: `gpg --list-secret-keys --keyid-format=long`
   - Say: "Look for the line that says 'sec' followed by 'rsa3072/' or 'rsa4096/'"
   - Say: "Copy the string after the slash (like '3AA5C34371567BD2')"
   - Say: "Now let's configure Git with your key:"
   - Have them run:
     ```bash
     git config --global user.signingkey [THEIR_KEY_ID]
     git config --global commit.gpgsign true
     ```
   - Say: "Replace [THEIR_KEY_ID] with the key ID you copied"
   - Verify with: `git config --global --list | grep -E "(signingkey|gpgsign)"`
   - Say: "Great! Git is now configured to sign all your commits."

3. **Once All Prerequisites Are ✅**
   
   Say: "Excellent! All prerequisites are ready. Now I'll set up the contract repositories."
   
   Run these commands:
   ```bash
   # Clone the contract
   git clone https://github.com/TherryApp/TherryOperatingAgreement.git
   cd TherryOperatingAgreement
   
   # Clone the signing app
   git clone https://github.com/matznerd/ContractSigningApp.git
   cd ContractSigningApp
   npm install
   npm run build
   cd ..
   ```

4. **Identify the Signer**
   
   Say: "Now I need to confirm your identity for the contract."
   Ask: "Are you Ryan Kushner or Eric Matzner?"
   
   Verify their GitHub username:
   - Ryan: @ryankushner-sudo
   - Eric: @matznerd

5. **Start the Signing Process**
   
   Say: "Perfect! Let's begin signing the Therry LLC Operating Agreement."
   Say: "This will create a legally binding digital signature using your GPG key."
   
   Run: `node ContractSigningApp/test-sign.js contracts/operating-agreement.md`

6. **Guide Through Signing**
   
   During the process:
   - When selecting signer: Confirm they choose the right number
   - Before contract display: "Please read the entire agreement carefully"
   - For legal signature: "You must type your name EXACTLY as shown"
   - For GPG passphrase: "Enter your GPG passphrase (it won't display)"

7. **On Success**
   
   Say: "🎉 Congratulations! You've successfully signed the operating agreement!"
   Explain what happened:
   - "Your signature has been recorded in the contract"
   - "A GPG-signed commit was created"
   - "A pull request has been opened for review"
   - "Once [other party] signs, the agreement will be complete"

## Important Reminders:
- Emphasize this is LEGALLY BINDING
- Never rush them
- Be patient with technical issues
- For contract questions (not process), suggest legal counsel