# KERNEL.md
Lumen OS – Kernel Architecture and Support Policy

This document defines the **design goals, architecture, and platform support**
of the Lumen kernel.

The Lumen kernel is **multi-architecture**, but **mobile-first**.

---

## 1. Kernel Overview

The Lumen kernel is a **Linux-based kernel** designed to:
- Support modern Android hardware
- Remain portable across CPU architectures
- Provide long-term stability for custom OS development

Primary targets:
- Android smartphones and tablets
- Development and testing on PCs (x86-64)

---

## 2. Supported Architectures

### Currently Supported

- **ARM64 (AArch64)**  
  Primary and mandatory architecture  
  Required for Android devices

- **x86-64 (AMD64)**  
  Secondary architecture  
  Used for:
  - Development
  - Emulation
  - CI testing
  - Desktop bring-up

The kernel must build and boot on both architectures.

---

## 3. Android Device Compatibility

The kernel is explicitly designed to support:

- Qualcomm-based Android devices
- Android boot image format
- Android device trees (DT / DTBO)
- Android partition layouts
- Android firmware interfaces

Android compatibility is **not optional**.

---

## 4. Kernel Base

- Linux upstream as the long-term reference
- Qualcomm downstream trees where required
- Vendor kernel sources for device bring-up

Policy:
- Prefer upstream when possible
- Use downstream when required by hardware
- Never sacrifice hardware support for purity

---

## 5. Boot Requirements

The kernel must support:

- Android boot protocol
- Bootloader handoff from ABL
- Kernel command line parsing
- Initramfs / ramdisk
- Fastboot-compatible boot images

Boot reliability has higher priority than feature completeness.

---

## 6. Device Tree Policy

- ARM64 uses DT / DTBO exclusively
- No hardcoded platform assumptions
- Hardware description must remain external to the kernel

x86-64:
- ACPI supported
- Device tree optional

---

## 7. Android-Specific Kernel Features

Mandatory features:
- Binder
- Ashmem or memfd replacement
- Ion or DMA-BUF heaps
- SELinux support
- cgroups
- Namespace isolation
- wakelocks
- lowmemory handling

These features are required even if Lumen userspace differs from Android.

---

## 8. Firmware Interfaces

The kernel must interface with:

- Qualcomm modem via QMI / QRTR
- GPU via vendor driver (KGSL)
- DSP subsystems
- Power management firmware (RPMh / PMIC)
- Secure services via TrustZone interfaces

Firmware remains external and untouched.

---

## 9. Power Management

Required capabilities:
- cpuidle
- cpufreq
- suspend / resume
- thermal framework
- battery and charging interfaces

Power safety is a hard requirement on Android devices.

---

## 10. Graphics & Display

Support:
- Framebuffer console
- DRM/KMS
- Vendor GPU drivers
- Software rendering fallback

GPU acceleration is optional during early bring-up but required for usability.

---

## 11. Fastboot & USB

The kernel must support:
- USB gadget framework
- Fastboot protocol
- Recovery mode operation

Fastboot is the primary recovery and debugging interface.

---

## 12. Security Model

- SELinux enforced by default
- Firmware-enforced secure boot respected
- No attempts to bypass hardware security

Security failures must degrade functionality, not brick devices.

---

## 13. Debugging & Instrumentation

Always available:
- early printk
- persistent logging
- ftrace
- dynamic debug
- crash dumps

A kernel without logs is considered broken.

---

## 14. Portability Rules

- Architecture-specific code must be isolated
- Device-specific logic belongs in:
  - drivers/
  - device tree
- Core kernel remains portable

x86-64 must not regress ARM64 support.

---

## 15. Long-Term Maintenance

- Stable kernel ABI is not guaranteed
- Device kernels may lag upstream
- Security patches are mandatory

Longevity matters more than novelty.

---

## 16. Completion Criteria

Kernel support is considered complete when:
- Boots on ARM64 Android device
- Boots on x86-64 PC or VM
- Supports firmware interfaces
- Enables stable userspace execution

---

## 17. Final Rule

The kernel exists to make hardware usable.

Architecture flexibility is a feature.
Android compatibility is a requirement.
