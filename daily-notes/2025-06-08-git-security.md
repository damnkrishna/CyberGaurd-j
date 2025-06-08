# Security essential while using GITHUB

In the past, one common way of hacking into web applications was by finding admin passwords directly embedded in the source code. As a developer myself, I know that modern practices have evolved—developers now typically create `.env` files to store their passwords and fetch them when required. When uploading or pushing their code to Git or any platform, they exclude the `.env` file, making their programs safer, right?

Unfortunately, this isn't always true. Even now, when posting projects on Git, people often forget to remove their `.env` files in their rush to publish. Sometimes when a website crashes, it exposes passwords, making it easier for hackers to gain access.

Additionally, if you initially post your `.env` file on Git but later remember to remove it, Git has already stored your password in its history, making it unsafe. You need to change those credentials immediately. Even after removal, you may have inadvertently left paths to the file in other files, and there are always remnants that aren't completely deleted, which hackers can exploit.

## How Hackers Exploit These Leaks

- Using GitHub dorks to hunt for secrets
- Employing tools like Gitleaks to scan entire repository histories
- Scanning archived or nested files that contain credentials

## What They Can Do with These Passwords

With access to your credentials, hackers can compromise:
- Database passwords (MySQL, MongoDB)
- Cloud provider keys (AWS, Azure)
- Payment provider keys (Stripe, Razorpay)
- Email API keys (Mailgun, SendGrid)
- JWT/authentication secrets

Basically, if they own your backend, they own you.

## What You Can Do NOW

- Always include `.env` in `.gitignore` before making any commits
- Run scanners like Gitleaks or TruffleHog on your repository before pushing
- For CI/CD, store secrets using GitHub Secrets, Vault, or Key Management Services

## Importance of Enabling Secret Scanning Alerts

Secret scanning alerts will:
- Alert you if secrets are found in your commits by anyone scanning for them

If not enabled:
- Anyone can scan your repository and gain access to your environment files
- Your passwords might be misused
- Your application could be completely compromised
