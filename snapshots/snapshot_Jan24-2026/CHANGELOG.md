# What this 1.0.6 Snapshot added

PalisadeOS snapshot Jan 24 added these:

[Wifi Connection] (Done!)
- Compile files under /wf_con

[Palikey] (Done!)
- Implement Palikey
- Polish Palikey for PalisadeOS
- Better emoji support

[Boot path validation] (Done!)
- Verify cold boot paths: UEFI → kernel and Android bootloader → kernel
- Add early boot log buffer (pre-filesystem)
- Expose /proc/bootinfo (bootloader, mode, device class)

[init Sequencing] (Done!)
- Deterministic init order file (/palisade/init.seq)
- Fail-safe init stage with timeout and fallback shell
- Init service dependency resolution (minimal DAG)

[Memory Management] (Done!)
- Early memory map dump (usable/reserved/IO)
- Page allocator stats endpoint
- Memory pressure notification hook

[Extras - Undocumented] (Done!)
- GUI Extensions (Called "GUI Modules"
