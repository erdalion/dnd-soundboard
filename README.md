# D&D Soundboard

A browser-based soundboard for tabletop RPG sessions. Hosts and players can organize and manage audio in a browser, then trigger playback through a dedicated audio device.

The project explores a game-audio workflow: managing sound assets, trimming clips, and triggering playback remotely during a session.

<!-- ## Preview

[Soundboard screenshot](docs/images/soundboard-screenshot.png) -->


## Features

- Play sounds with a single click on a soundboard button
- Browse sounds from folders or view all sounds together
- Organize sounds by categories
- Add a sound with a name, emoji, category, and audio file
- Trim an uploaded clip before saving it
- Edit a sound's name, emoji, or category
- Send playback commands to connected audio devices through Socket IO

## How it works

1. A host or player can upload and organize sound clips in the web client.
2. The server processes uploaded audio and stores sound details in MySQL; audio files live on the mounted SMB share.
3. A player clicks a sound in the browser, and the server sends a playback event to the connected audio connector.
4. The connector plays the requested file through the machine's audio device.

<!-- ## Architecture

<!-- ![Architecture diagram](docs/images/architecture.png) -->


## For players

Players do not need to install anything. Open the soundboard in a supported web browser using the address provided by the host to browse, add, and organize sounds, then click a sound to play it.

## Components

- `dnd-soundboard-client` - React, TypeScript, and Vite web interface
- `dnd-soundboard-server` - Express and Socket IO API with MySQL and FFmpeg
- `dnd-soundboard-puszczacz` - Node.js Socket IO audio connector for Linux/ALSA

## Run locally

This setup is tailored to my environment and requires adapting the database, SMB storage, network, and audio-device configuration.

Prerequisites: Node.js, npm, a MySQL database, FFmpeg, and network-attached sound storage using SMB (for example, a NAS such as TrueNAS). Mount the SMB share on the server and set the sound storage path in `dnd-soundboard-server/index.js`.

```bash
# Start the server
cd dnd-soundboard-server
npm install
npm start

# Start the web client
cd dnd-soundboard-client
npm install
npm run dev

# Start the audio connector on the playback machine
cd dnd-soundboard-puszczacz
npm install
npm start
```

The client uses `http://soundboard.local`, and the server listens on port `3000`. Configure the database, sound storage path, server address, permitted IP, and ALSA device in the source files before running on another network.