
# Creating Multiple Spotify Playlists Using Terraform

## 🎯 Project Overview

This project demonstrates how to automate the creation and management of multiple Spotify playlists using Terraform. Whether it's for morning motivation, evening relaxation, or party vibes, this setup leverages the Spotify API and Terraform's automation capabilities to streamline playlist management.

## 🧰 Prerequisites

Before you begin, ensure you have the following:

* **Terraform**: Make sure Terraform is installed on your local machine. You can download it from the [official website](https://www.terraform.io/downloads.html).
* **Docker**: Ensure Docker is installed and running. [Download Docker](https://www.docker.com/products/docker-desktop).
* **Spotify Account**: You need a Spotify account (free tier is sufficient).
* **Spotify Developer Account**: Register and create an application to get your Client ID and Client Secret. Visit the [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/applications) to create an app.
* **Spotify Provider for Terraform**: Install and configure the Spotify provider for Terraform.
* **VS Code**: Recommended for editing Terraform files.

## 🚀 Steps to Complete the Project

### 1. Set Up Terraform Project

1. Create a new directory for your Terraform project and navigate to it in your terminal.

   ```bash
   mkdir spotify-playlist-terraform
   cd spotify-playlist-terraform
   ```

2. Create a file named `main.tf`.

### 2. Define Provider

In `main.tf`, define the Spotify provider:

```hcl
provider "spotify" {
  api_key = "your_spotify_api_key"
}
```

### 3. Obtain API Key

To interact with Spotify's API, you need a Client ID and Client Secret:

1. Go to the [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/applications).
2. Create a new application to obtain your Client ID and Client Secret.
3. Set the Redirect URI as `http://localhost:27228/spotify_callback`.

### 4. Configure Authentication Proxy

To authenticate Terraform with Spotify:

1. Create a `.env` file in your project directory with the following content:

   ```env
   SPOTIFY_CLIENT_ID=your_spotify_client_id
   SPOTIFY_CLIENT_SECRET=your_spotify_client_secret
   ```

2. Run the Spotify authentication proxy:

   ```bash
   docker run --rm -it -p 27228:27228 --env-file .env ghcr.io/conradludgate/spotify-auth-proxy
   ```

3. Follow the instructions in the terminal to authenticate and obtain your API key.

### 5. Create Playlists

Define your playlists in `main.tf`:

```hcl
resource "spotify_playlist" "morning_playlist" {
  name        = "Morning Motivation"
  description = "Start your day with energy!"
  public      = true
  tracks      = ["track_id_1", "track_id_2", "track_id_3"]
}

resource "spotify_playlist" "evening_playlist" {
  name        = "Evening Relaxation"
  description = "Unwind after a long day."
  public      = true
  tracks      = ["track_id_4", "track_id_5", "track_id_6"]
}
```

Replace `"track_id_1"`, `"track_id_2"`, etc., with actual Spotify track IDs.

### 6. Initialize and Apply Terraform Configuration

1. Initialize the Terraform configuration:

   ```bash
   terraform init
   ```

2. Apply the Terraform configuration:

   ```bash
   terraform apply
   ```

3. Confirm the action when prompted.

### 7. Verify Playlists on Spotify

After applying the Terraform configuration, log in to your Spotify account and verify that the playlists have been created and populated with the specified tracks.

