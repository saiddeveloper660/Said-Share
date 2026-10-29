# SAID SHARE

### Fast, Private & Local File Sharing

Said Share is a modern local-network file sharing application that allows users to transfer files between Android devices and computers without cloud storage or internet-based file servers.

Developed by: **Said Developer**

---

## 🌟 Key Features

- **⚡ Blazing Fast Local Wi-Fi Speed:** Transfer files at full Wi-Fi network throughput directly between devices without internet bottlenecks.
- **📱 Phone ↔ Phone Direct Transfer:** Quick peer-to-peer file sharing between Android phones with automatic device discovery (mDNS / NSD & subnet scanning).
- **💻 Phone ↔ Windows PC Browser Transfer:** No software installation required on PC! The Android app hosts an embedded responsive web interface accessible via browser with drag-and-drop file upload and batch downloading.
- **🔒 Private & Secure:** Offline-first architecture. No accounts, no cloud servers, no third-party tracking. Transfers are protected by temporary 6-digit session PINs and user confirmation prompts.
- **📦 Unlimited File Types & Large File Streaming:** Send photos, videos, APKs, documents, ZIP archives, and gigabyte-sized files safely using buffered 64KB chunked I/O without OutOfMemory errors.
- **📊 Real-Time Progress & Controls:** Live current-file and overall percentage, transfer speed (MB/s), estimated time remaining, plus Pause, Resume, and Cancel capabilities.
- **📜 Local Transfer History:** Built-in Room database maintains history of sent and received files with one-tap opening via Android FileProvider.
- **🌓 Modern Material 3 UI:** Designed with sleek Electric Cyan aesthetics, full edge-to-edge support, dynamic dark mode, and responsive layout.

---

## 🏗️ Architecture

Said Share is built following clean MVVM (Model-View-ViewModel) architecture:

```
com.example/
├── data/              # Persistence layer
│   ├── dao/           # Room Data Access Objects (TransferDao)
│   ├── model/         # Database entities (TransferEntity)
│   ├── repository/    # TransferRepository for local history
│   └── AppDatabase.kt # SQLite database configuration
├── model/             # Domain models (DeviceItem, FileItem, TransferState)
├── network/           # Local networking engine
│   ├── NetworkUtils.kt       # IP detection, Wi-Fi status, PIN generation
│   ├── SaidNsdHelper.kt      # Android Network Service Discovery (mDNS)
│   ├── SubnetScanner.kt      # Concurrent subnet probe on port 8765
│   ├── SaidHttpServer.kt     # Embedded multi-threaded streaming HTTP server
│   ├── SaidTransferClient.kt # OkHttp client with streaming CountingRequestBody
│   └── SaidWebUi.kt          # Embedded responsive HTML5/CSS/JS PC interface
├── qr/                # ZXing QR Code matrix generation
├── service/           # Foreground data-sync service with ongoing notification
├── storage/           # Storage Access Framework & FileProvider manager
├── ui/
│   ├── components/    # Reusable Material 3 cards, badges, dialogs
│   ├── screens/       # Home, Send, Receive, Transfer, Success, History, Settings
│   └── theme/         # Color palette, Typography, SaidShareTheme
└── viewmodel/         # MainViewModel managing state and background transfers
```

---

## 📱 How It Works

### Sending Files from Android to Android
1. Open **Said Share** on both phones.
2. Receiver taps **Receive** to start the local transfer server.
3. Sender taps **Send**, selects one or multiple files, and selects the discovered device from the radar list.
4. Receiver confirms the incoming transfer prompt.
5. The transfer streams with real-time progress and speed indicators.

### Sending Files between Phone & Windows PC
1. On Android, tap **Receive**.
2. Note the local URL displayed (e.g. `http://192.168.1.45:8765`).
3. Open the URL in Google Chrome, Microsoft Edge, or Firefox on any Windows PC connected to the same Wi-Fi.
4. Drag and drop any files directly into the browser to upload them to the phone, or download files shared by the phone.

---

## 🛠️ Build & Installation Instructions

### Prerequisites
- Android Studio Ladybug (2024.2+) or later
- JDK 17 or JDK 21
- Android SDK 35 / 36
- Minimum Android version: Android 7.0 (API Level 24)

### Building from Source
```bash
# Clone the repository
git clone https://github.com/said-developer/said-share.git
cd said-share

# Build Debug APK
./gradlew assembleDebug

# Run Unit & Robolectric Tests
./gradlew testDebugUnitTest
```

---

## 🛡️ Security & Privacy Notice

- Said Share works entirely on your local area network (LAN / WLAN).
- It never contacts external cloud servers, collects analytics, or uploads your files online.
- Keep your device connected to a trusted Wi-Fi network when sharing sensitive files.

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

---

**Developed with ❤️ by Said Developer**
