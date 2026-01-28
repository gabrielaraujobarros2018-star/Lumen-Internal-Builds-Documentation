# ComponentNaming.md
## Safe, Generic Android-Style Component Names for New OS Projects

This document lists **generic, legally safe component names** commonly seen in Android and OS design that you can reuse in a new operating system **without trademark or copyright risk**, provided you implement your own code or respect open-source licenses.

Names listed here are **descriptive system terms**, not protected product branding.

---

## 1. Core System & Boot

- init
- SystemServer
- ServiceManager
- BootManager
- PowerManager
- ShutdownController
- Recovery
- Watchdog
- CrashHandler
- PanicHandler

---

## 2. UI / Shell / Interaction

- SystemUI
- WindowManager
- DisplayManager
- InputManager
- GestureManager
- StatusBar
- NotificationManager
- Launcher
- TaskSwitcher
- Recents
- OverlayManager
- ThemeManager
- AnimationController
- SurfaceManager
- Compositor

---

## 3. IPC / Process / Runtime

- Binder
- BinderIPC
- IPCManager
- RPCManager
- MessageQueue
- Parcel
- ParcelBuffer
- ObjectHandle
- ProcessManager
- ThreadManager
- Zygote
- AppSpawner
- Runtime
- VMRuntime

---

## 4. Permissions / Security / Policy

- PermissionController
- PermissionManager
- AccessController
- PolicyManager
- SecurityManager
- SELinuxController
- SandboxManager
- UIDManager
- CapabilityManager
- AuthManager
- KeyStore
- KeyManager
- CryptoService

---

## 5. Application Framework

- PackageManager
- AppManager
- ActivityManager
- TaskManager
- IntentManager
- ResourceManager
- AssetManager
- ContentProvider
- ServiceRegistry
- LifecycleManager

---

## 6. Storage / Filesystem

- StorageManager
- VolumeManager
- MountService
- FileService
- MediaStore
- CacheManager
- BackupManager
- RestoreManager
- Indexer
- FileObserver

---

## 7. Networking / Connectivity

- NetworkManager
- ConnectivityService
- WifiManager
- EthernetManager
- BluetoothManager
- RadioManager
- TelephonyService
- VPNService
- FirewallService
- DNSResolver

---

## 8. Media / Graphics / Audio

- AudioManager
- AudioService
- MediaServer
- MediaCodec
- CameraService
- GraphicsService
- RenderService
- SurfaceComposer
- VideoService

---

## 9. Hardware Abstraction

- HAL
- HardwareService
- DeviceManager
- SensorService
- SensorManager
- PowerHAL
- AudioHAL
- DisplayHAL
- InputHAL
- CameraHAL

---

## 10. Updates / Maintenance / Debug

- UpdateEngine
- OTAService
- PackageInstaller
- RollbackManager
- Logcat
- Logger
- DebugService
- TraceService
- Profiler
- DumpService

---

## 11. System Utilities

- TimeService
- AlarmManager
- JobScheduler
- SyncManager
- ClipboardService
- SearchService
- LocaleManager
- ConfigManager
- SettingsProvider

---

## Naming Rules (Hard Requirements)

- Names are safe; **code origin is what matters**
- Do NOT reuse Android branding (Android™, Google™, Pixel™)
- Use your own namespaces:
  - `org.youros.systemui`
  - `org.youros.ipc.binder`
  - `org.youros.permissioncontroller`
- If using AOSP code, **follow Apache 2.0 license**
- Never claim Android compatibility unless it is real

---

## Bottom Line

These names are:
- Generic
- Industry-standard
- Used across multiple OSes
- Legally safe for independent OS development

Android does **not own system architecture vocabulary**.

Use them confidently.
