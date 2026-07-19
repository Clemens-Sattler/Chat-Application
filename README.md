<div align="center">

# 💬 ChatProjekt

**A modern desktop chat platform built with Java & JavaFX**

[![Java](https://img.shields.io/badge/Java-23-orange?logo=openjdk&logoColor=white)](https://www.java.com)
[![JavaFX](https://img.shields.io/badge/JavaFX-17-1f7ac0?logo=java&logoColor=white)](https://openjfx.io)
[![Maven](https://img.shields.io/badge/Maven-3.x-c71a36?logo=apachemaven&logoColor=white)](https://maven.apache.org)

*Real-time rooms, private chats, voice notes, images, emojis and an integrated FAQ assistant.*

</div>

---

## ✨ Overview

ChatProjekt is a full-stack desktop messenger written in Java. A multithreaded socket server powers a JavaFX client to deliver group and private conversations, rich media and a built-in chatbot — all behind a clean, themeable UI.

## 🚀 Features

- 🔐 **Accounts & sessions** — register, login and duplicate-session protection
- 🏠 **Group rooms** — create, join and switch between chat rooms (default *Lobby*)
- ✉️ **Private messages** — direct one-to-one chats via `@username`
- 🎙️ **Voice messages** — record, send and play back audio notes
- 🖼️ **Image sharing** — drag-and-drop picture transfer between clients
- 😀 **Emoji picker** — categorised emojis in the composer
- 🤖 **FAQ chatbot** — local knowledge-base assistant for quick answers
- 📡 **Live presence** — system messages on join, leave and room updates
- 🧩 **Pluggable message types** — strategy-based serializers for text, voice, image and emoji payloads

## 🛠️ Tech Stack

| Layer        | Technology                                          |
| ------------ | --------------------------------------------------- |
| Language     | **Java 23**                                         |
| UI           | **JavaFX 17** · FXML · CSS                          |
| Networking   | Java **Sockets** · object serialization             |
| Audio        | **Java Sound API** (`javax.sound.sampled`)          |
| Build        | **Maven** with `javafx-maven-plugin`                |
| Libraries    | Gson · OkHttp · Apache Commons · JUnit 5            |
| Persistence  | UCanAccess · Jackcess · HSQLDB                      |

## 🏗️ Architecture

```
		┌────────────────────────────┐
		│      JavaFX Client(s)      │
		│   chat · voice · images    │
		│      emojis · chatbot      │
		└─────────────┬──────────────┘
					  │  Message<T> over TCP
					  ▼
		┌────────────────────────────┐
		│       Server Control       │
		│  rooms · users · routing   │
		│  multithreaded, port 8008  │
		└────────────────────────────┘
```

- **Shared model** — abstract `Message<T>` with chat, system and room-event variants.
- **Server** — accepts connections, spawns a proxy per user, and dispatches messages via concurrent collections.
- **Client** — a background reader thread surfaces incoming messages to JavaFX controllers through typed callbacks.
- **Add-ons** — voice, image and emoji modules are isolated, each with its own serializer.

## 🎙️ My Contribution — Voice Messages

I designed and built the **voice-message module** end-to-end as my individual area of ownership:

- Microphone capture and WAV encoding with `TargetDataLine` / `AudioInputStream`
- A reusable `AudioLogic` API (`startRecording`, `stopRecording`, `play`)
- TCP transfer between clients (`AudioSender` / `AudioReceiver`)
- A `VoiceMessage` domain type and serializer that plug into the shared message pipeline
- A small Swing test harness for fast iteration before JavaFX integration

Beyond that I contributed small fixes and integration glue across the rest of the codebase.

## 👥 Team

Built by a team of **13 students** as part of a collaborative course project. Each member owned a feature area while we coordinated on the shared message protocol, server core and UI shell.