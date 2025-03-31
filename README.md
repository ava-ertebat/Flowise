<!-- markdownlint-disable MD030 -->

<img width="100%" src="https://github.com/FlowiseAI/Flowise/blob/main/images/flowise.png?raw=true"></a>

# Flowise - Build LLM Apps Easily

[![Release Notes](https://img.shields.io/github/release/FlowiseAI/Flowise)](https://github.com/FlowiseAI/Flowise/releases)
[![Discord](https://img.shields.io/discord/1087698854775881778?label=Discord&logo=discord)](https://discord.gg/jbaHfsRVBW)
[![Twitter Follow](https://img.shields.io/twitter/follow/FlowiseAI?style=social)](https://twitter.com/FlowiseAI)
[![GitHub star chart](https://img.shields.io/github/stars/FlowiseAI/Flowise?style=social)](https://star-history.com/#FlowiseAI/Flowise)
[![GitHub fork](https://img.shields.io/github/forks/FlowiseAI/Flowise?style=social)](https://github.com/FlowiseAI/Flowise/fork)

English | [繁體中文](./i18n/README-TW.md) | [簡體中文](./i18n/README-ZH.md) | [日本語](./i18n/README-JA.md) | [한국어](./i18n/README-KR.md)

<h3>Drag & drop UI to build your customized LLM flow</h3>
<a href="https://github.com/FlowiseAI/Flowise">
<img width="100%" src="https://github.com/FlowiseAI/Flowise/blob/main/images/flowise.gif?raw=true"></a>

## ⚡Quick Start

Download and Install [NodeJS](https://nodejs.org/en/download) >= 18.15.0

1. Install Flowise
    ```bash
    npm install -g flowise
    ```
2. Start Flowise

    ```bash
    npx flowise start
    ```

    With username & password

    ```bash
    npx flowise start --FLOWISE_USERNAME=user --FLOWISE_PASSWORD=1234
    ```

3. Open [http://localhost:3000](http://localhost:3000)

## 🐳 Docker

### Docker Compose

1. Clone the Flowise project
2. Go to `docker` folder at the root of the project
3. Copy `.env.example` file, paste it into the same location, and rename to `.env` file
4. `docker compose up -d`
5. Open [http://localhost:3000](http://localhost:3000)
6. You can bring the containers down by `docker compose stop`

### Docker Image

1. Build the image locally:
    ```bash
    docker build --no-cache -t flowise .
    ```
2. Run image:

    ```bash
    docker run -d --name flowise -p 3000:3000 flowise
    ```

3. Stop image:
    ```bash
    docker stop flowise
    ```

## 👨‍💻 Developers

Flowise has 3 different modules in a single mono repository.

-   `server`: Node backend to serve API logics
-   `ui`: React frontend
-   `components`: Third-party nodes integrations
-   `api-documentation`: Auto-generated swagger-ui API docs from express

### Prerequisite

-   Install [PNPM](https://pnpm.io/installation)
    ```bash
    npm i -g pnpm
    ```

### Setup

1.  Clone the repository

    ```bash
    git clone https://github.com/FlowiseAI/Flowise.git
    ```

2.  Go into repository folder

    ```bash
    cd Flowise
    ```

3.  Install all dependencies of all modules:

    ```bash
    pnpm install
    ```

4.  Build all the code:

    ```bash
    pnpm build
    ```

    <details>
    <summary>Exit code 134 (JavaScript heap out of memory)</summary>  
      If you get this error when running the above `build` script, try increasing the Node.js heap size and run the script again:

        export NODE_OPTIONS="--max-old-space-size=4096"
        pnpm build

    </details>

5.  Start the app:

    ```bash
    pnpm start
    ```

    You can now access the app on [http://localhost:3000](http://localhost:3000)

6.  For development build:

    -   Create `.env` file and specify the `VITE_PORT` (refer to `.env.example`) in `packages/ui`
    -   Create `.env` file and specify the `PORT` (refer to `.env.example`) in `packages/server`
    -   Run

        ```bash
        pnpm dev
        ```

    Any code changes will reload the app automatically on [http://localhost:8080](http://localhost:8080)

## 🔒 Authentication

To enable app level authentication, add `FLOWISE_USERNAME` and `FLOWISE_PASSWORD` to the `.env` file in `packages/server`:

```
FLOWISE_USERNAME=user
FLOWISE_PASSWORD=1234
```

## 🌱 Env Variables

Flowise support different environment variables to configure your instance. You can specify the following variables in the `.env` file inside `packages/server` folder. Read [more](https://github.com/FlowiseAI/Flowise/blob/main/CONTRIBUTING.md#-env-variables)

## 📖 Documentation

[Flowise Docs](https://docs.flowiseai.com/)


# 🧠 Flowise Installing Guide with Docker & Portainer

Welcome to this **ultimate guide** for installing **Flowise** — an open-source **UI for LLM-based workflows** — on **Ubuntu 24.04** using **Docker** and **Portainer**.  
This **comprehensive step-by-step tutorial** walks you through installing Flowise with **SSL (HTTPS)** for secure access, managed beautifully via Portainer.

---

## 🚀 Prerequisites

### 💾 Software Requirements
- ✅ **Ubuntu 24.04 LTS** (fresh installation is best)  
- ✅ **Docker** (v28+)  
- ✅ **Docker Compose Plugin**  
- ✅ **Portainer (CE)** for container management  
- ✅ **acme.sh** for free Let's Encrypt SSL certificates  
- ✅ **A domain name** (e.g., `flowise.yourdomain.com`) pointing to your server  

### 🖥️ Hardware Requirements (Minimum)
- 💾 2GB RAM (4GB+ recommended)  
- 💿 10GB Disk space  
- 🌐 A public IP (for SSL validation)  

---

## 🏗️ Step-by-Step Installation

---

### 1️⃣ Update & Upgrade System
```bash
sudo apt update -y && sudo apt upgrade -y
```

---

### 2️⃣ Install Docker & Docker Compose Plugin
```bash
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

✅ **Check Docker:**
```bash
docker --version
```

---

### 3️⃣ Install Portainer (UI for Docker)
```bash
docker volume create portainer_data

docker run -d -p 8000:8000 -p 9443:9443 --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce:latest
```

🔗 Access Portainer at:  
```
https://[YOUR_SERVER_IP]:9443
```

🔑 Set a secure admin password & connect to **local** Docker.

---

### 4️⃣ Install acme.sh (For SSL Certificate)
```bash
sudo apt install curl socat -y
curl https://get.acme.sh | sh
source ~/.bashrc

~/.acme.sh/acme.sh --set-default-ca --server letsencrypt
~/.acme.sh/acme.sh --register-account -m your-email@example.com
```

---

### 5️⃣ Generate SSL Certificates for Flowise Domain
```bash
~/.acme.sh/acme.sh --issue -d flowise.yourdomain.com --standalone

sudo mkdir -p /etc/ssl/private /etc/ssl/certs

~/.acme.sh/acme.sh --installcert -d flowise.yourdomain.com \
--key-file /etc/ssl/private/flowise_private.key \
--fullchain-file /etc/ssl/certs/flowise_certificate.crt

sudo chown 1000:1000 /etc/ssl/private/flowise_private.key
sudo chown 1000:1000 /etc/ssl/certs/flowise_certificate.crt

sudo chmod 600 /etc/ssl/private/flowise_private.key
sudo chmod 644 /etc/ssl/certs/flowise_certificate.crt
```

---

### 6️⃣ Deploy Flowise via Portainer with SSL

#### 🛠 Steps in Portainer:

1. Go to **Volumes** → **+ Add volume**  
```
Name: flowise_data
```

2. Go to **Containers** → **+ Add container**

#### 🔧 Basic Config:
```
Name: flowise
Image: flowiseai/flowise:latest
```

#### 🔌 Port Mapping:
```
Host: 3443
Container: 3000
```

#### 📂 Volumes:
- container:`/etc/ssl/private/flowise_private.key` → volume:`/ssl/flowise_private.key` → (Writable) and (Bind Mode)
- container:`/etc/ssl/certs/flowise_certificate.crt` → volume:`/ssl/flowise_certificate.crt` → (Writable) and (Bind Mode)
- container:`flowise_data` → volume:`/root/.flowise` → (Writable) and (volume Mode)

#### ⚙️ Environment Variables:
```
- Name:`FLOWISE_USERNAME` → `value:admin`

- Name:`FLOWISE_PASSWOR` → value:`your_secure_password`

- Name:`PORT` → value:`3000`

- Name:`SSL_KEY_PATH` → value:`/ssl/flowise_private.key`

- Name:`SSL_CERT_PATH` → value:`/ssl/flowise_certificate.crt`

- Name:FLOWISE_SECURE → value:true
```

✅ **Click "Deploy the container"**

---

### 7️⃣ Access Flowise Dashboard
Open in browser:  
```
https://flowise.yourdomain.com:3443
```

Use your `admin` credentials to login.

---

## 🔧 Maintenance & Tips

### 🔄 Auto-renew SSL:
```bash
~/.acme.sh/acme.sh --renew -d flowise.yourdomain.com --force
docker restart flowise
```

---

### 📜 View Logs:
```bash
docker logs flowise
```

---

### ♻️ Restart / Stop Container:
```bash
docker restart flowise
docker stop flowise
```

---

### ⚠️ Optional - Reverse Proxy with Nginx:
For production-ready routing on port 443, consider Nginx with a proxy to `localhost:3443`.

---

## 🎉 All Done!

You’ve now installed and secured **Flowise** on Ubuntu 24.04 using **Docker**, **Portainer**, and **HTTPS**.  
Start building your AI workflows with peace of mind and full control! 🚀

---

## 📬 Contact & Support

💬 **Need help or consulting? Let’s talk!**  
🌐 **Website:** [https://ava-ertebat.ir](https://ava-ertebat.ir)  
📧 **Email (Support):** support@ava-ertebat.ir  
📧 **Email (Personal):** omidswordfish@gmail.com  
📱 **WhatsApp:** [Chat on WhatsApp](https://wa.me/989163422797?text=Hi%20there!%20Need%20help%20with%20Flowise%20installation%20guide.)




## 🌐 Self Host

Deploy Flowise self-hosted in your existing infrastructure, we support various [deployments](https://docs.flowiseai.com/configuration/deployment)

-   [AWS](https://docs.flowiseai.com/configuration/deployment/aws)
-   [Azure](https://docs.flowiseai.com/configuration/deployment/azure)
-   [Digital Ocean](https://docs.flowiseai.com/configuration/deployment/digital-ocean)
-   [GCP](https://docs.flowiseai.com/configuration/deployment/gcp)
-   [Alibaba Cloud](https://computenest.console.aliyun.com/service/instance/create/default?type=user&ServiceName=Flowise社区版)
-   <details>
      <summary>Others</summary>

    -   [Railway](https://docs.flowiseai.com/configuration/deployment/railway)

        [![Deploy on Railway](https://railway.app/button.svg)](https://railway.app/template/pn4G8S?referralCode=WVNPD9)

    -   [Render](https://docs.flowiseai.com/configuration/deployment/render)

        [![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://docs.flowiseai.com/configuration/deployment/render)

    -   [HuggingFace Spaces](https://docs.flowiseai.com/deployment/hugging-face)

        <a href="https://huggingface.co/spaces/FlowiseAI/Flowise"><img src="https://huggingface.co/datasets/huggingface/badges/raw/main/open-in-hf-spaces-sm.svg" alt="HuggingFace Spaces"></a>

    -   [Elestio](https://elest.io/open-source/flowiseai)

        [![Deploy on Elestio](https://elest.io/images/logos/deploy-to-elestio-btn.png)](https://elest.io/open-source/flowiseai)

    -   [Sealos](https://cloud.sealos.io/?openapp=system-template%3FtemplateName%3Dflowise)

        [![](https://raw.githubusercontent.com/labring-actions/templates/main/Deploy-on-Sealos.svg)](https://cloud.sealos.io/?openapp=system-template%3FtemplateName%3Dflowise)

    -   [RepoCloud](https://repocloud.io/details/?app_id=29)

        [![Deploy on RepoCloud](https://d16t0pc4846x52.cloudfront.net/deploy.png)](https://repocloud.io/details/?app_id=29)

      </details>

## ☁️ Flowise Cloud

[Get Started with Flowise Cloud](https://flowiseai.com/)

## 🙋 Support

Feel free to ask any questions, raise problems, and request new features in [discussion](https://github.com/FlowiseAI/Flowise/discussions)

## 🙌 Contributing

Thanks go to these awesome contributors

<a href="https://github.com/FlowiseAI/Flowise/graphs/contributors">
<img src="https://contrib.rocks/image?repo=FlowiseAI/Flowise" />
</a>

See [contributing guide](CONTRIBUTING.md). Reach out to us at [Discord](https://discord.gg/jbaHfsRVBW) if you have any questions or issues.
[![Star History Chart](https://api.star-history.com/svg?repos=FlowiseAI/Flowise&type=Timeline)](https://star-history.com/#FlowiseAI/Flowise&Date)

## 📄 License

Source code in this repository is made available under the [Apache License Version 2.0](LICENSE.md).
