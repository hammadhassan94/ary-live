# How to list ARY PLUS patches on Morphe (community)

Official Morphe patches (YouTube, Reddit) live in  
[MorpheApp/morphe-patches](https://github.com/MorpheApp/morphe-patches).

**You do not PR into that repo.**  
You publish a **community patch source** from  
[MorpheApp/morphe-patches-template](https://github.com/MorpheApp/morphe-patches-template).

Your source is already that template:

`C:\Users\hammad\Desktop\APK\ARY-mobile\arylive-patches`

In Morphe Manager the **app name stays ARY PLUS** (`com.release.arylive`).  
Do **not** brand the GitHub project “Morphe Patches” (see `NOTICE`). The public repo is **ARY Live** (`hammadhassan94/ary-live`).

---

## What users will see

| Place | Name |
|-------|------|
| Play Store / patched app icon | **ARY PLUS** |
| Package | `com.release.arylive` |
| Version to pick | **3.8.0** |
| Your GitHub source | `hammadhassan94/ary-live` |
| Patch to enable | **Hide ads**, **Bypass PairIP license check**, **Custom branding** |

Morphe **resigns** the APK (same as YouTube/Reddit). It is not Play-signed. That is expected. Users uninstall the Play copy **or** also enable **Change package name** (from official/community patches) for side-by-side.

---

## A. One-time PC setup

1. Install **JDK 21**.
2. GitHub account. Create a **Personal Access Token**:
   - Scopes: `read:packages`, `repo`, `workflow`
3. File `%USERPROFILE%\.gradle\gradle.properties`:

```properties
gpr.user=YOUR_GITHUB_USERNAME
gpr.key=ghp_YOUR_TOKEN
```

4. Optional: `gh auth login`

---

## B. Put your identity in the project

Edit `patches/build.gradle.kts`:

```kotlin
group = "app.arylive"

patches {
    about {
        name = "ARY Live Patches"
        description = "Hide ads for ARY PLUS (com.release.arylive) 3.8.0"
        source = "git@github.com:hammadhassan94/ary-live.git"
        author = "YOUR_NAME"
        contact = "na"
        website = "na"
        license = "GPLv3"
    }
}
```

In `README.md` replace every `hammadhassan94`.

Optional: add `patches-bundle.png` (square icon) in the repo root for Manager.

---

## C. Create the public GitHub repo

On GitHub: **New repository** → name `ary-live` → **Public**.  
Do not add a README (folder already has one).

```powershell
cd C:\Users\hammad\Desktop\APK\ARY-mobile\arylive-patches

git remote remove origin   # if it still points at the template
git remote add origin https://github.com/hammadhassan94/ary-live.git
git add -A
git commit -m "feat: Hide ads for ARY PLUS 3.8.0"
git branch -M main
git push -u origin main
```

Also create a `dev` branch (template workflow):

```powershell
git checkout -b dev
git push -u origin dev
```

Repo **Settings → Actions → General**:

- Allow GitHub Actions
- **Read and write** permissions
- Enable **Allow GitHub Actions to create and approve pull requests**

---

## D. Make a release (this is what “lists” it)

Morphe Manager does **not** load raw Kotlin. It loads a **`.mpp`** from a GitHub **Release**.

Template rule: **semantic commits** on `dev` / `main`.  
`release.yml` builds and uploads `patches-*.mpp`.

| Commit | Effect |
|--------|--------|
| `feat: Hide ads for ARY PLUS 3.8.0` | new version |
| `fix: CdnPlayer IMA skip` | patch version |
| `chore: docs` | no release |

Typical flow:

1. Push `feat:` commits to **`dev`** → pre-release `.mpp` (users enable “pre-release” in Manager).
2. Merge **`dev` → `main`** (merge, do not squash) → **stable** release.

Local test without waiting for CI:

```powershell
cd C:\Users\hammad\Desktop\APK\ARY-mobile\arylive-patches
.\gradlew.bat buildAndroid
```

File: `patches\build\libs\patches-*.mpp`

Do **not** hand-edit `patches-list.json`, `patches-bundle.json`, or `CHANGELOG.md` after CI is live.

---

## E. Community add link (share this)

```text
https://morphe.software/add-source?github=hammadhassan94/ary-live
```

Anyone with Morphe Manager taps that → source appears in **Patch sources**.

Manual: Manager → Patch sources → add `hammadhassan94/ary-live`.

---

## F. What testers / users do in Morphe Manager

1. Install [Morphe Manager](https://morphe.software/).
2. Add your source (link above).
3. Download stock **ARY PLUS 3.8.0** APK (`com.release.arylive`) — single APK, not Reddit-style split.
4. Manager asks for the **correct version: 3.8.0**.
5. Enable:
   - **Hide ads**
   - **Bypass PairIP license check** (needed for resigned sideload)
   - **Custom branding** → **App icon**: `Original` (real logo) or `Custom` (Morphe-style blue plus)
     App name stays **ARY PLUS** unless you change it.
6. Optional: **Change package name** if they want to keep the Play Store app.
7. Patch → Install.

If they **do not** change the package name: uninstall Play Store ARY PLUS first (signature mismatch).

---

## G. Local `.mpp` (you only, before GitHub)

1. Manager → Patch sources → import `patches\build\libs\patches-*.mpp`
2. Same as F from step 3.

---

## Folder to upload

Upload **only**:

`C:\Users\hammad\Desktop\APK\ARY-mobile\arylive-patches`

Not `ARY-mobile`, not `ARY-src`, not keystores, not Lab APKs.
