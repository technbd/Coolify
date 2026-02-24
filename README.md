## Coolify:

**Coolify** is an **open-source, self-hostable platform-as-a-service (PaaS)** that makes it easy to **deploy and manage web applications, databases, and other services** on your own servers (like **VPS**, **bare metal**, **Raspberry Pi**, etc.) without relying on managed cloud platforms. 

It’s often described as a self-hosted alternative to services like **Heroku**, **Vercel**, **Netlify**, and **Railway**, giving you more control, privacy, and potentially much lower costs.


_Benefits of Self-Hosting with Coolify:_
- A **self-hosted PaaS platform** that you install on your own server.
- **Full ownership & control** of data and infrastructure — no vendor lock-in.
- Lower long-term costs compared with managed cloud PaaS offerings.
- Freedom to scale across multiple servers and environments.
- Open-source community and extensibility if you want to customize or contribute.



### Key Features:

1. **Broad Deployment Support**:  
Deploy almost anything: static sites, full-stack apps (**Node.js**, **Python**, **PHP**, **Go**, **Ruby**, etc.), Docker **containers**, and **databases**.

2. **Git Integration & CI/CD**:  
Connect with **GitHub**, GitLab, Bitbucket, or Gitea. Coolify can automatically build and deploy on every push.

3. **Automatic SSL & Reverse Proxy**:  
Coolify includes a built-in reverse proxy (e.g., Traefik/Caddy) that automatically manages HTTPS certificates via Let’s Encrypt.

4. **Services & Databases**:  
One-click deployment of common services and databases like **PostgreSQL**, **MySQL**/MariaDB, **MongoDB**, **Redis**, and more.

5. **Environment & Configuration Management**:  
Manage **environment variables**, **secrets**, **domains**, and networking from a dashboard — no manual server edits needed.

6. **Monitoring & Logs**:  
See deployment logs and basic performance metrics via the UI.

7. **Multi-Server Support**:  
Connect more than one server and deploy to different nodes from a central console.



### Requirements:
- Server: Laptop, VPS, VM, Raspberry Pi
- Supported Operating Systems: 
    - Debian, Ubuntu - all TLS versions supported
    - Redhat-based (CentOS, TencentOS, Fedora, Redhat, AlmaLinux, Rocky)
    - SUSE-based (e.g., SLES, SUSE, openSUSE)
    - Arch Linux (Note: Not all Arch derivatives are supported)
    - Alpine Linux
    - Raspberry Pi OS 64-bit (Raspbian)
- Minimum Hardware Requirements: CPU: 2 cores, Memory (RAM): 2 GB, Storage: 30 GB 




---
---



## Installation Coolify:


_What the Installer Does:_
- Installs essential tools (curl, wget, git, jq, openssl)
- Installs Docker Engine (version 24+)
- Configures Docker settings (logging, daemon)
- Sets up directories at /data/coolify
- Configures SSH keys for server management
- Installs and starts Coolify





```
curl -fsSL https://cdn.coollabs.io/coolify/install.sh | bash
```




This will:

- Pull Coolify Docker image
- Create required volumes
- Start Coolify container
- Expose port 8000


```
docker ps

CONTAINER ID   IMAGE                                        COMMAND                  CREATED         STATUS                   PORTS                                                                                                                                                                NAMES
828d6236e9e9   traefik:v3.6                                 "/entrypoint.sh --pi…"   4 minutes ago   Up 4 minutes (healthy)   0.0.0.0:80->80/tcp, [::]:80->80/tcp, 0.0.0.0:443->443/tcp, [::]:443->443/tcp, 0.0.0.0:8080->8080/tcp, [::]:8080->8080/tcp, 0.0.0.0:443->443/udp, [::]:443->443/udp   coolify-proxy
6fe28b2bf24c   ghcr.io/coollabsio/sentinel:0.0.18           "/app/sentinel"          4 minutes ago   Up 4 minutes (healthy)                                                                                                                                                                        coolify-sentinel
f48434cccb24   ghcr.io/coollabsio/coolify:4.0.0-beta.463    "docker-php-serversi…"   5 minutes ago   Up 5 minutes (healthy)   8000/tcp, 8443/tcp, 9000/tcp, 0.0.0.0:8000->8080/tcp, [::]:8000->8080/tcp                                                                                            coolify
b95a929e9c53   postgres:15-alpine                           "docker-entrypoint.s…"   5 minutes ago   Up 5 minutes (healthy)   5432/tcp                                                                                                                                                             coolify-db
0c3b535f2b85   redis:7-alpine                               "docker-entrypoint.s…"   5 minutes ago   Up 5 minutes (healthy)   6379/tcp                                                                                                                                                             coolify-redis
c06c45f79023   ghcr.io/coollabsio/coolify-realtime:1.0.10   "/bin/sh /soketi-ent…"   5 minutes ago   Up 5 minutes (healthy)   0.0.0.0:6001-6002->6001-6002/tcp, [::]:6001-6002->6001-6002/tcp                                                                                                      coolify-realtime

```





### Access Coolify:

Open browser: `http://SERVER_IP:8000`



### Setup Domain + HTTPS (Recommended):

After login:
1. Add your domain: **Settings** - **Configuration** - **General**:
    - **URL**: `https://coolify.example.com`
    - Name: 
    - Instance's Public IPv4: your_public_IP
2. Point DNS **A record** to your server IP: 
    - Type: A
    - Name (sub-domain): coolify 
    - IPv4: your_public_IP 
3. Enable automatic SSL (Let’s Encrypt)



---
---



## Deploy App:


### Example-1: 

1. Projects - `+ Add`:
    - Name: web-app
    - Description: 

1. Projects - `+ Add`:
    - Name: databases
    - Description: 
    - click `+ Add Resource`  
    - select `PostgreSQL`
        - Name: postgresql-database
        - Image:
        - Username: postgres
        - Password: 
        - Initial Database: postgres
        - Ports: 
        - Postgres URL (internal): 
        - click `Start`

3. Setup Private Repo: Sources - `+ Add`:
    - Name: web-app-repo 
    - click `Continue`
    - click `Register Now`
        - GitHub App name: 

4. For Public Repo: Projects - click `web-app`:
    - click `+ Add Resource`
    - select `Public repository`
    - Repository URL (https://): `https://github.com/coollabsio/coolify-examples/tree/v4.x/nextjs/ssr`
    - click `Check repository`
        - Branch:
        - Build Pack: `Nixpacks`
        - Base Directory:
        - Port: 
        - click `Continue`
            - Name: 
            - Build Pack: 
            - Domains: `https://app1.example.com`
            - Build: 
            - click `Deploy`


5. For Private Repo: Projects - click `web-app`:
    - click `+ Add Resource`
    - select `Private repository (with Github App)`
    - select a Github App: 



### License: 
MIT - LICENSE


### Ref: 
- [coolify Docs](https://coolify.io/docs/get-started/introduction)
- [coolify Installation](https://coolify.io/docs/get-started/installation)
- [github.com | coollabsio](https://github.com/coollabsio/coolify-examples)





