# REVERSE_ENGINEERING.md
Lumen OS – Samsung Galaxy A05s (Snapdragon 680)

This document defines the **scope, rules, and workflow** for reverse-engineering hardware and firmware
interfaces required to run Lumen OS on the Galaxy A05s.  
Goal: **minimum time, maximum reuse, zero blind work**.

---

## 1. Core Principles

- Reverse **interfaces**, not implementations
- Treat firmware as **immutable black boxes**
- Prefer elimination and observation over static analysis
- Linux kernel is the hardware contract
- Userspace is replaceable; firmware is not

---

## 2. Non-Goals (Explicitly Out of Scope)

Do NOT reverse:
- Modem firmware (modem.mbn, dsp.mbn)
- TrustZone (tz.mbn, keymaster)
- Hypervisor (hyp.mbn)
- PMIC firmware
- Qualcomm secure boot chain

These are interfaced with, not replaced.

---

## 3. Target Partitions

Handled by Lumen:
- boot (kernel, init, userspace)
- recovery (debug / rescue only)
- super (system, vendor interface layer)

Left intact:
- modem
- tz
- hyp
- xbl / xbl_config
- abl (except handoff behavior)

---

## 4. Reverse-Engineering Order (MANDATORY)

1. Boot chain validation
2. Kernel bring-up
3. Display + input
4. USB + fastboot
5. Storage
6. Power management
7. Modem interface
8. GPU acceleration
9. Sensors
10. Audio
11. Camera (last)

Skipping order increases time exponentially.

---

## 5. Boot Chain Analysis

Objectives:
- Confirm bootloader unlock persistence
- Identify kernel entry point
- Extract kernel command line
- Preserve original boot image

Artifacts:
- boot.img (original)
- kernel config
- dtb / dtbo overlays

No binary patching at this stage.

---

## 6. Kernel Strategy

Base:
- Qualcomm downstream Linux kernel
- Vendor device tree

Steps:
1. Build stock kernel
2. Boot without modification
3. Enable verbose logging
4. Disable features incrementally
5. Track breakage

Never write new drivers unless forced.

---

## 7. Device Tree Reverse-Engineering

Focus areas:
- Display panel bindings
- Touch controller
- Power regulators
- GPIO mappings
- Clocks

Method:
- Compare dtb vs dtbo overlays
- Observe runtime behavior changes
- Log probe failures

No guessing.

---

## 8. Display & Input

Goals:
- Framebuffer output
- Touch events
- Rotation and resolution correctness

Fallback allowed:
- Software rendering
- No GPU acceleration initially

GPU comes later.

---

## 9. USB & Fastboot

Requirements:
- USB gadget framework
- Fastboot protocol support
- Recovery escape path

Fastboot must work before UI.

---

## 10. Storage

Targets:
- eMMC access
- Partition mapping
- Read/write validation

Avoid:
- Repartitioning
- Super partition resizing early

---

## 11. Power Management

Interfaces:
- cpuidle
- cpufreq
- RPMh
- Regulators

Validation:
- Suspend / resume
- Thermal throttling
- Battery drain baseline

Battery safety > performance.

---

## 12. Modem Interface

Scope:
- QMI
- QRTR
- IPC Router

Rules:
- Modem firmware untouched
- Userspace communicates only
- No kernel-space modem logic

Success metric:
- Network registration
- Data connection
- Call setup

---

## 13. GPU Acceleration

Subsystem:
- KGSL
- Vendor blobs

Approach:
- Reuse existing driver
- Match userspace expectations

If it breaks:
- Fall back to software rendering
- Continue OS development

GPU is optional for early Lumen.

---

## 14. Instrumentation & Debugging

Always enabled:
- early printk
- persistent dmesg
- ftrace
- dynamic debug

Never debug without logs.

---

## 15. Time-Reduction Rules

- No static binary reversing unless unavoidable
- No clean-room rewrites
- No firmware replacement attempts
- No purity goals

Working > elegant.

---

## 16. Completion Criteria

Reverse-engineering phase is considered complete when:
- Kernel boots reliably
- Display + touch work
- USB fastboot works
- Modem connects
- Power management is stable

UI, polish, and optimization come later.

---

## 17. Failure Conditions

If any of these occur, stop and reassess:
- Repeated hard bricks
- No serial or kernel logs
- Modem instability
- Thermal runaway

Hardware safety overrides progress.

---

## 18. Final Rule

If a task does not directly move the device
from **non-booting → usable**, it is postponed.

Lumen is built by finishing, not perfecting.
