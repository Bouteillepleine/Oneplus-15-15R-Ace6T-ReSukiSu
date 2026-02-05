# Build OnePlus 15 — ReSukiSU Kernel Builder

A GitHub Actions workflow that builds an **Android GKI kernel**, integrates **ReSukiSU**, optionally applies **SUSFS**, and packages the result as a flashable **AnyKernel3 ZIP**.

This repo is meant for reproducible, configurable CI builds with useful build metadata (hashes, sizes, timings) and optional features like NETFILTER, BBR+ECN, and Baseband Guard (BBG).

---

## ✨ Highlights

- **ReSukiSU integration** (KernelSU fork) via upstream `setup.sh`
- Optional **SUSFS** patching (with metadata capture: branch, commit, version)
- Optional **KPM** image patching (`patch_linux`)
- Network toggles: **NETFILTER** + **BBR/ECN**
- Security toggle: **LSM / Baseband Guard (BBG)**
- Repro-friendly:
  - Optional **custom build timestamp**
  - Optional **custom kernel suffix** (or random suffix)
  - Optional **ccache**
- Produces:
  - **AnyKernel3 flashable ZIP**
  - Build summary with **SHA256**, sizes, warnings count, and commit links

---

## 📦 Output

After a successful run, the workflow uploads an artifact:

- **AnyKernel3 ZIP** containing the built `Image`
- Artifact name format :
  - `AnyKernel3_ReSuki_<KSUVER>_OnePlus15_<KERNELVER>_KPM_LSM_ReSuki.zip`

The build summary also reports:

- ZIP + Image size
- ZIP + Image SHA256
- Build duration
- KernelSU (ReSukiSU) commit link
- SUSFS commit link (if enabled)

---

## 🚀 How to Use

1. **Fork** this repo (or copy the workflow into your repo).
2. Go to **Actions** → **Build Oneplus**.
3. Click **Run workflow**.
4. Choose your options (FILE / SUSFS / KPM / NETFILTER / etc.).
5. Download the generated artifact from the workflow run page.

---
## ⚠️ Notes / Disclaimers

- This repo builds a kernel that may include features intended for advanced use-cases (root/module frameworks, filesystem hiding layers, etc.).  
**Use responsibly and only on devices you own and are willing to recover.**
- Always keep a known-good boot image and recovery path available.
- This project is not affiliated with OnePlus, Google, or the upstream projects referenced.

## 🙏 Credits

This workflow references and/or uses components from:
- Kernel manifests
- **ReSukiSU** (KernelSU fork)
- **SUSFS** patch set
- **AnyKernel3** packaging template
- Patch collections used in CI steps

All credit belongs to their respective maintainers.
