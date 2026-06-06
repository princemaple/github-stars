---
project: Nimbus
stars: 1976
description: The future of file storage
url: https://github.com/nimbusdotstorage/Nimbus
---

Nimbus cloud storage
====================

A better cloud

Quickstart
----------

Prerequisites
-------------

-   Bun (JavaScript runtime)
-   Docker (for running PostgreSQL)
-   Git
-   OpenSSL

### 1\. Clone the Repository

git clone https://github.com/nimbusdotstorage/Nimbus.git
cd Nimbus

### 2\. Install Dependencies

bun i

### 3\. Environment Setup

1.  Copy .env.example to .env

cp .env.example .env

Copy .env to child directories

bun run env:sync

Follow the instructions on the first step of this guide.

How to setup Google keys?  

-   Navigate to Google Cloud console.
    
-   Create a new project and navigate to its dashboard.
    
-   Navigate to **OAuth Consent Screen** and enter the details.
    
    -   Name: _Nimbus_
    -   Audience: _External_
    -   Contact info: _youremail@gmail.com_
-   Navigate to **Clients**.
    
    -   Type: _Web application_
    -   Name: _Nimbus_
    -   Add **Authorised Javascript origin** as `http://localhost:3000`
    -   Add **Authorised redirect uri** as `http://localhost:1284/api/auth/callback/google`
    -   **IMPORTANT**:Get your `client_id` and `client_secret`.
-   Enable Google Drive API
    
    -   Search for **Google Drive API** or Click Here.
    -   Click **Enable**.
-   Now navigate to **Audience** and add **Test users**.
    

How to setup Microsoft keys?  

Official Guide: Microsoft Register App

-   Go to the **Microsoft Azure Portal**.
    
-   Navigate to **Microsoft Entra ID** → Click **Add** → Click **App registrations**.
    
    -   Name: _Nimbus_
    -   Under **Supported account types**, choose: **Accounts in any organizational directory and personal Microsoft accounts** (i.e. all Microsoft account users).
    -   Under **Redirect URI**, select **Web** and enter: `http://localhost:1284/api/auth/callback/microsoft` (Also add `http://localhost:3000` under front-end origins if needed.)
-   After registration, navigate to the app's **Overview** to copy your **Application (client) ID**.
    
-   In the left menu, Click **Manage**. Use this to navigate.
    
-   Navigate to **Certificates & secrets** → Click **New client secret** → Add a _description_ and _expiry_ → Click **Add** → Copy the generated secret value.
    
-   Navigate to **API permissions** and make sure these **delegated Microsoft Graph** permissions are added and granted:
    
    -   `email` – View users' email address
    -   `offline_access` – Maintain access to data you have given it access to
    -   `openid` – Sign users in
    -   `profile` – View users' basic profile
    -   `User.Read` – Sign in and read user profile
    -   `Files.ReadWrite.All` – Have full access to user files (OneDrive access)
-   Click **Grant admin consent** to apply the permissions.
    

How to setup Box keys?  

Official Guide: Box Create OAuth 2.0 App

-   Navigate to Box Developer Console console.
    
-   Click **Create App**. Select **Custom App**.
    
-   Fill in the form.
    
    -   Name: _Nimbus_
    -   Purpose: _Integration_
    -   Categories: _Productivity, Collaboration, Core Enterprise_
    -   External system are you integrating with: _Box files_
    -   Click **Next**
    -   Select **User Authentication (OAuth 2.0)**
    -   Click **Create App**
-   Copy the **Client ID** and **Client Secret** under **OAuth 2.0 Credentials**.
    
-   Add **OAuth 2.0 Redirect URIs** as `http://localhost:1284/api/auth/oauth2/callback/box`.
    

> **Note**: The redirect URI is different because it uses the generic oauth2 plugin from better-auth.

-   Add **Application Scopes**:
    
    -   `Read all files and folders stored in Box`
    -   `Write all files and folders stored in Box`
    -   `Manage Users`
    -   `Enable Integrations`
-   Add **CORS Domains** as `http://localhost:3000`.
    
-   Click **Save Changes**.
    

Details

Official Guide: Dropbox OAuth Guide

How to setup Dropbox keys?  

-   Navigate to Dropbox App Console.
    
-   Click **Create App**.
    
    -   Select: _Scoped Access_
    -   Select: _Full Dropbox Access_
    -   Name: _Nimbus_
-   Copy the **App key** and **App secret**.
    
-   Add _OAuth 2 Redirect URIs_ as `http://localhost:1284/api/auth/callback/dropbox`.
    
-   Navigate to **Permission** and add **Scopes**.
    
    -   `account_info.read`
    -   `files.metadata.read`
    -   `files.content.read`
    -   `files.content.write`
    -   `sharing.read`
-   Click **Submit** in the pop up bar.
    

GOOGLE\_CLIENT\_ID=
GOOGLE\_CLIENT\_SECRET=

MICROSOFT\_CLIENT\_ID=
MICROSOFT\_CLIENT\_SECRET=

BOX\_CLIENT\_ID=
BOX\_CLIENT\_SECRET=

# To generate a secret, just run \`openssl rand -base64 32\`
BETTER\_AUTH\_SECRET=

How to get a Resend API Key?  

1.  Go to Resend.com and sign up or log in to your account.
    
2.  From the dashboard, click on **"API Keys"** in the sidebar.
    
3.  Click the **"Create API Key"** button.
    
4.  Enter a name for your key (e.g., `nimbus-dev`) and confirm.
    
5.  Copy the generated API key.
    
6.  Add it to your `.env` file:
    

RESEND\_API\_KEY=your-api-key-here

### 4\. Set Up Postgres and Valkey with Docker

We use Docker to run a PostgreSQL database and Valkey for local development. Follow these steps to set it up:

1.  **Start the database and valkey**:
    
    bun db:up
    bun cache:up
    
    This will start a Postgres container with default credentials:
    
    -   Host: `localhost`
    -   Port: `5432`
    -   Database: `nimbus`
    -   Username: `postgres`
    -   Password: `postgres`
    
    And a Valkey container with credentials:
    
    -   Host: `localhost`
    -   Port: `6379`
    -   Username: `valkey`
    -   Password: `valkey`
2.  **Verify the database and valkey is running if running a detached container**:
    
    docker ps
    
    You should see the `nimbus-db` and `nimbus-cache` containers in the list with a status of "Up".
    
3.  **Run Database Migrations**
    

After setting up the database, run the migrations:

bun db:push

1.  **Connect to the database** (optional):
    
    # Using psql client inside the container
    docker compose exec postgres psql -U postgres -d nimbus
    
2.  **Connect to the valkey** (optional):
    
    # Using valkey-cli inside the container
    docker compose exec valkey valkey-cli --user valkey --pass valkey
    

### 7\. Start the Development Server

In a new terminal, start the development server:

> NOTE: this starts both the web and server development servers, to run just one, use `bun dev:web` or `bun dev:server`. Both will need the db running to work.

bun dev

The application should now be running at http://localhost:3000

### 8\. Access Authentication

Once the development server is running, you can access the authentication pages:

-   **Sign In**: Navigate to http://localhost:3000/signin
-   **Sign Up**: Navigate to http://localhost:3000/signup

Make sure you have configured the Google OAuth credentials in your `.env` file as described in step 4 for authentication to work properly. Additionally, configure your Resend API key for the forgot password functionality to work.

If you want to contribute, please refer to the contributing guide

Deploying Docker images (ex. Coolify)
-------------------------------------

Follow the DEPLOYMENT.md file for instructions on how to deploy with Coolify.

Our Amazing Contributors
------------------------

Deploying Nimbus to VPS/VDS for Production or Development
---------------------------------------------------------

> Deployment is the same locally or on a server, but OAuth providers (e.g., Google) require a domain for callback URLs.

### Steps to Deploy on a Server:

1.  Point your **domain** to the server.
2.  Use the domain in Google API keys for callback URLs (e.g., `https://example.com:1284/api/auth/callback/google`).
3.  Update the `.env` file with the domain (e.g., `TRUSTED_ORIGINS=https://example.com:3000`).
