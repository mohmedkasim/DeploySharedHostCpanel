## Deploy Github private/public shared host cpanel using FTP account
note: I assuming you have already github repo ready to deploy
1. create FTP account in cpanel
2. create FTP account in github with same data as in cpanel FTP account and same domain you created (data existed in cpanel FTP account):
 - FTP_USERNAME: admin@domain.com
 - FTP_SERVER: domain-name.com
 - FTP_PASSWORD
3. create workflow in github of repository

with name example: main.yaml, contains:
```yaml
name: Deploy to cPanel
on:
  push:
    branches:
      - master
jobs:
  FTP-Deploy-Action:
    name: FTP-Deploy-Action
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2.1.0
        with:
          fetch-depth: 2
      # Deploy to cPanel
      - name: FTP-Deploy-Action
        uses: SamKirkland/FTP-Deploy-Action@3.1.1
        with:
          ftp-server: ${{ secrets.FTP_SERVER }}
          ftp-username: ${{ secrets.FTP_USERNAME }}
          ftp-password: ${{ secrets.FTP_PASSWORD }}

```
4. make sure ftp accounts created in cpanel folder manager (public_html)
5. follow deploy in repo actions in github
# You Done.
