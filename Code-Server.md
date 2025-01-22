---
title: Visual Studio Code - Open Source ("Code - OSS") - Lynx
intro: Data Architecture -  DSs, Analytics, & ML Stack
versions:
  fpt: '*'
  ghes: '*'
  ghec: '*'
shortTitle: DSS Stack
---
Visual Studio Code - Open Source ("Code - OSS")
# Run Visual Studio Code Server- Open Source ("Code - OSS") on any machine anywhere and access it in the browser, choice ofd two different architectures 

Reference the Websites
[Code-Server] https://github.com/coder/code-server)
[MS VS Code] https://github.com/Microsoft/vscode


> [!NOTE]
> Highlights
Code on any device with a consistent development environment
Use cloud servers to speed up tests, compilations, downloads, and more
Preserve battery life when you're on the go; all intensive tasks run on your servers 


## Stand Alone Server

Login in Screenshot 

![image](https://github.com/user-attachments/assets/8faf75fb-bcbb-434d-ac74-6e7fc6f034b7)


```markdown
admins@studio-svr:~$ curl -fsSL https://code-server.dev/install.sh | sh
Ubuntu 22.04.5 LTS
Installing v4.96.2 of the amd64 deb package from GitHub.

+ mkdir -p ~/.cache/code-server
+ curl -#fL -o ~/.cache/code-server/code-server_4.96.2_amd64.deb.incomplete -C - https://github.com/coder/code-server/releases/download/v4.96.2/code-server_4.96.2_amd64.deb
######################################################################## 100.0%
+ mv ~/.cache/code-server/code-server_4.96.2_amd64.deb.incomplete ~/.cache/code-server/code-server_4.96.2_amd64.deb
+ sudo dpkg -i ~/.cache/code-server/code-server_4.96.2_amd64.deb
Selecting previously unselected package code-server.
(Reading database ... 115553 files and directories currently installed.)
Preparing to unpack .../code-server_4.96.2_amd64.deb ...
Unpacking code-server (4.96.2) ...
Setting up code-server (4.96.2) ...

deb package has been installed.

To have systemd start code-server now and restart on boot:
  sudo systemctl enable --now code-server@$USER
Or, if you don't want/need a background service you can run:
  code-server

Deploy code-server for your team with Coder: https://github.com/coder/coder
admins@studio-svr:~$  sudo systemctl enable --now code-server@$USER
Created symlink /etc/systemd/system/default.target.wants/code-server@admins.service → /lib/systemd/system/code-server@.service.

# Change ip address & password
admins@studio-svr:~$  sudo nano /home/admins/.config/code-server/config.yaml 
admins@studio-svr:~$  sudo systemctl restart code-server@$USER


```

Code Server Screen Screenshot  


![image](https://github.com/user-attachments/assets/c26a75a8-200a-413e-91a4-a1d7bb880516)


### Add to you ~/.bashrc , ~./zshrc or other bash like startup script

1:Listen on port 80 --> export CODER_HTTP_ADDRESS=0.0.0.0:80 

2:Enable TLS and listen on port 443 --> export CODER_TLS_ENABLE=true : export CODER_TLS_ADDRESS=0.0.0.0:443

3:Redirect from HTTP to HTTPS --> export CODER_REDIRECT_TO_ACCESS_URL=true

### Start the Coder server
coder server

# GitHub Example - Uasing (CODER_EXTERNAL_AUTH_0_ID="primary-github") makes a GitHub authentication token available at data.coder_external_auth.github.access_token

data "coder_external_auth" "<github|gitlab|azure-devops|bitbucket-cloud|bitbucket-server|other>" {
    id = "<USER_DEFINED_ID>"
}

```
data "coder_external_auth" "github" {
   id = "PyramidGithub"
}
# or 
data "coder_external_auth" "github" { id = "PyramidGithub" }
```

## Build Infrustructure to Serve Code Server Teams, Labs & Organizations

Create a Code Server site with Terraform, Kubernetes or  other options

```markdown

admins@studio-svr:~$ curl -L https://coder.com/install.sh | sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
100 21450  100 21450    0     0  39219      0 --:--:-- --:--:-- --:--:-- 39219
Resolved mainline version: v2.18.2
Ubuntu 22.04.5 LTS
The latest mainline version has been promoted to stable, selecting stable.
Installing v2.18.2 of the amd64 deb package from GitHub.

+ mkdir -p ~/.cache/coder
+ curl -#fL -o ~/.cache/coder/coder_2.18.2_amd64.deb.incomplete -C - https://github.com/coder/coder/releases/download/v2.18.2/coder_2.18.2_linux_amd64.deb
######################################################################## 100.0%
+ mv ~/.cache/coder/coder_2.18.2_amd64.deb.incomplete ~/.cache/coder/coder_2.18.2_amd64.deb
+ sudo dpkg --force-confdef --force-confold -i ~/.cache/coder/coder_2.18.2_amd64.deb
[sudo] password for admins:
Selecting previously unselected package coder.
(Reading database ... 125960 files and directories currently installed.)
Preparing to unpack .../coder/coder_2.18.2_amd64.deb ...
Unpacking coder (2.18.2-1) ...
Setting up coder (2.18.2-1) ...

deb package has been installed.

To run a Coder server:

  # Start Coder now and on reboot
  $ sudo systemctl enable --now coder
  $ journalctl -u coder.service -b

  # Or just run the server directly
  $ coder server

  Configuring Coder: https://coder.com/docs/admin/setup

To connect to a Coder deployment:

  $ coder login <deployment url>

admins@studio-svr:~$ coder server
Coder v2.18.2+d15c470 - Your Self-Hosted Remote Development Platform
Started HTTP listener at http://127.0.0.1:3000
Using built-in PostgreSQL (/home/admins/.config/coderv2/postgres)
Opening tunnel so workspaces can connect to your deployment. For production scenarios, specify an external access URL
Using tunnel in US East Pittsburgh with latency  50.903735ms .
╔═══════════════════════════════════════════════╗
║               View the Web UI:                ║
║   https://9gh5nvu9cb7e8.pit-1.try.coder.app   ║
╚═══════════════════════════════════════════════╝
```

Create the TLS secret in your Kubernetes cluster

kubectl create secret tls coder-tls -n <coder-namespace> --key="tls.key" --cert="tls.crt"



```markdown 
coder:
  tls:
      secretName:
      - coder-tls

  # Alternatively, if you use an Ingress controller to terminate TLS,
  # set the following values:
  ingress:
      enable: true
      secretName: coder-tls
      wildcardSecretName: coder-tls
```

$ coder server postgres-builtin-url
psql "postgres://coder@localhost:49627/coder?sslmode=disable&password=feU...yI1"



