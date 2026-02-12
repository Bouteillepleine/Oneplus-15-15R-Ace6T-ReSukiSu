# Build OnePlus 15 — ReSukiSU Kernel Builder

A GitHub Actions workflow that builds an **Android GKI kernel**, integrates **ReSukiSU**, optionally applies **SUSFS**, and packages the result as a flashable **AnyKernel3 ZIP**.

Built for reproducible, configurable CI runs with useful build metadata (hashes, sizes, timings) and optional features like NETFILTER, BBR+ECN, and Baseband Guard (BBG).

---

## ✨ Highlights

- **ReSukiSU integration** (KernelSU fork) via upstream `setup.sh`
- Optional **SUSFS** patching (with metadata capture: branch, commit, version)
- Optional **KPM** image patching (`patch_linux`) when `KPM=KPM`
- Network toggles: **NETFILTER** + **BBR/ECN**
- Security toggle: **LSM / Baseband Guard (BBG)**
- **Manager compatibility**:
  - **Supported Unofficial Manager:** `MKSU`, `RKSU`, `SukiSU-Ultra`, `ReSukiSU`
- Repro-friendly options:
  - Custom **build timestamp**
  - Custom **kernel suffix** (or random)
  - Optional **ccache**
- Outputs:
  - Flashable **AnyKernel3 ZIP**
  - Build summary with **SHA256**, sizes, warnings count, and commit links

---

## 📦 Output

### What you get
- An uploaded artifact: **AnyKernel3 ZIP** containing the built `Image`

### ZIP naming format
The workflow produces a ZIP like:

- `AnyKernel3_<MANAGER_SOURCE>_<KSUVER>_OnePlus15_<TKERNEL_VERSION>[_KPM][_LSM].zip`

Where:
- `<MANAGER_SOURCE>` → `MD3` / `MD3_SPOOF`
- `<KSUVER>` → computed KernelSU/ReSukiSU version
- `<TKERNEL_VERSION>` → `VERSION.PATCHLEVEL.SUBLEVEL` from `common/Makefile`
- `[_KPM]` → appended only when `KPM=KPM`
- `[_LSM]` → appended only when `LSM=true`

### Build summary includes
- ZIP size + SHA256
- Image size + SHA256
- Build duration
- Warnings count (best-effort, if logs exist)
- ReSukiSU commit link
- SUSFS commit link (if enabled)
- Manager compatibility note:
  - **Supported Unofficial Manager:** `MKSU`, `RKSU`, `SukiSU-Ultra`, `ReSukiSU`

---

## 🚀 How to Use

1. **Fork** this repo (or copy the workflow into your repo).
2. Go to **Actions** → **Build Oneplus** (or your workflow name).
3. Click **Run workflow**.
4. Choose your options (`FILE`, `SUSFS_META`, `KPM`, `NETFILTER`, etc.).
5. Download the artifact from the workflow run page.

---

## ⚙️ Workflow Inputs (quick reference)

- `FILE`: kernel manifest branch suffix (used as `common-${FILE}`)
- `KSU_META`: `branch/custom_tag(optional)/commit_hash(optional)`
- `SUSFS_META`: rollback SUSFS to a commit (`-1` disables, empty = latest)
- `KPM`: `KPM` / `KPN` / `NoN`
- `LSM`: enable Baseband Guard (BBG)
- `NETFILTER`: enable NETFILTER extras (incl. IPSET / IPv6 NAT patches where supported)
- `BBR_ECN`: enable BBR + ECN config
- `UNICODE_BYPASS`: apply Unicode bypass fix (if selected)
- `BUILD_TIME`: custom timestamp, or `F` for current UTC
- `SUFFIX`: custom kernel suffix (or random if empty)
- `BUILD_NOCCACHE`: disable ccache
- `SPACE_NOCLEAN`: disable cleanup/max-space steps

---

## ⚠️ Notes / Disclaimers

- This kernel may include advanced features (root/module frameworks, filesystem hiding layers, etc.).  
  **Use responsibly and only on devices you own and are willing to recover.**
- Always keep a known-good boot image and a recovery path available.
- Not affiliated with OnePlus, Google, or any upstream projects referenced here.

---

## 🙏 Credits

This workflow references and/or uses components from:
- Android kernel manifests
- **ReSukiSU** (KernelSU fork)
- **SUSFS** patch set
- **AnyKernel3** packaging template
- Patch collections used by the CI steps

All credit belongs to their respective maintainers.
