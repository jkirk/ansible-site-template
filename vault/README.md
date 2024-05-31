# README for vault usage

We automatically decrypt the vault secret via gpg and gpg-agent.

To update the `vault_passphrase.gpg` file for keys the specific key IDs (see `-r` option) run:

    %  echo "$your_actual_vault_password" | gpg -e -o vault_passphrase.gpg -r 9BB6983DDD81AFEB -r 96A87872B7EA3737

Also see: [Secrets with Ansible: Ansible Vault and GPG | Vallard's Blog](https://web.archive.org/web/20160827053812/https://benincosa.com/?p=3235)
