# Atlantis
Testing the Atlantis. It's an application for automating Terraform via pull requests.

**First steps**

1. **[Install Terraform](https://developer.hashicorp.com/terraform/install)**

Terraform needs to be in the $PATH for Atlantis.

2. **[Download Atlantis](https://github.com/runatlantis/atlantis/releases)**

Get the [latest release] from GitHub and unzip it.


3. **[Download NGROK](https://download.ngrok.com)**

Atlantis needs to be accessible somewhere that github.com

Start NGROK on port 4141 and take note og the hostname it gives you:

* COMMAND: ngrok http 4141

4. Creates environment variables:
    * URL ="{https://{YOUR_HOSTNAME}.ngrok.io}"
    * SECRET ="{YOUR_RANDOM_STRING}"
    * USERNAME="{the username of your GitHub}"
    * REPO_ALLOWLIST="{your_git_host/your_username/your_repository}"
   

5. For add GitHub WebHook:
   * Go to your repo's settings
   * Select Webhooks or Hooks in the sidebar
   * Click Add webhook
   * Set Payload URL to your ngrok url with /events at the end. 
   * Set Content type to application/json
   * Set Secret to your random string
   * Select Let me select individual events
   * Check the boxes
     * Pull request reviews
     * Pushes
     * Issue comments
     * Pull requests
     * leave Active checked
   * click Add webhook


6. Create an GitHub Access Token 
   * Create a [Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-fine-grained-personal-access-token)
   * Create a token with repo scope
   * Set the token as an environment variable:
     * TOKEN="{YOUR_TOKEN}"


7. Start ATLANTIS
  ` ./atlantis server 
        --atlantis-url="\$URL" 
        --gh-user="\$USERNAME" 
        --gh-token="\$TOKEN" 
        --gh-webhook-secret="\$SECRET" 
        --repo-allowlist="\$REPO_ALLOWLIST"`