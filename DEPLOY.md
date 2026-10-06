# Deploy ARY Live Patches (Morphe community source)

Built from the official template:  
[MorpheApp/morphe-patches-template](https://github.com/MorpheApp/morphe-patches-template)

This repo is **not** a PR into [MorpheApp/morphe-patches](https://github.com/MorpheApp/morphe-patches).  
Official Morphe patches (YouTube, Reddit, …) live there. **Community** patches are separate GitHub repos (created from the template) that users add as a patch source.

ARY PLUS phone is a **single APK** (`ApkFileType.APK`). Reddit in official Morphe is often a **split** bundle (APKM) — Morphe Manager merges splits for you. You do **not** need that merge step for ARY mobile.

**Target app (latest as of 2026-10):**

| Field | Value |
|-------|--------|
| App | ARY PLUS |
| Package | `com.release.arylive` |
| Version | **3.8.0** (versionCode `180`) |
| Stock file | `ARY-mobile/ARY-Plus-mobile.apk` |

---

## 1. One-time setup (your PC)

1. Install **JDK 21**
2. Create a GitHub PAT with scopes: `read:packages`, `repo`, `workflow`
3. Login CLI (optional but useful):

```powershell
gh auth login
```

4. Gradle credentials for Morphe packages — create/edit  
   `%USERPROFILE%\.gradle\gradle.properties`:

```properties
gpr.user=YOUR_GITHUB_USERNAME
gpr.key=YOUR_GITHUB_PAT
```

Or for one session:

```powershell
$env:GITHUB_ACTOR = "YOUR_GITHUB_USERNAME"
$env:GITHUB_TOKEN = "YOUR_GITHUB_PAT"
```

---

## 2. Put your name on the bundle

Edit `patches/build.gradle.kts`:

```kotlin
source = "git@github.com:hammadhassan94/ary-live.git"
author = "YOUR_NAME"
```

Edit `README.md`: replace every `hammadhassan94` with your GitHub username.

---

## 3. Push the source (community listing)

```powershell
cd C:\Users\hammad\Desktop\APK\ARY-mobile\arylive-patches

# create empty public repo on GitHub named ary-live, then:
gh repo create ary-live --public --source=. --remote=origin --push
```

If the repo already exists:

```powershell
git remote add origin https://github.com/hammadhassan94/ary-live.git
git add -A
git commit -m "feat: Hide ads for ARY PLUS 3.8.0"
git branch -M main
git push -u origin main
```

Enable Actions → **Allow GitHub Actions to create and approve pull requests**  
(Settings → Actions → General → Workflow permissions).

---

## 4. Build the `.mpp` (what Morphe loads)

### Option A — local build

```powershell
cd C:\Users\hammad\Desktop\APK\ARY-mobile\arylive-patches
.\gradlew.bat buildAndroid
```

Output:

`patches\build\libs\patches-1.0.0.mpp` (version from `gradle.properties`)

### Option B — GitHub Releases (recommended for community)

1. Work on `dev` branch for WIP; merge to `main` for stable
2. Use **semantic commits**:
   - `feat: ...` → new release
   - `fix: ...` → patch release
   - `chore: ...` → no release
3. Push → template `release.yml` builds + publishes a GitHub Release with the `.mpp`

Users then add:

```text
https://morphe.software/add-source?github=hammadhassan94/ary-live
```

---

## 5. Use in Morphe Manager (phone / desktop)

### Local file (before GitHub is public)

1. Morphe Manager → **Patch sources** → import / add **local** `.mpp`
2. Select stock APK: **ARY PLUS 3.8.0** (`com.release.arylive`)
3. Manager shows compatible version **3.8.0** (from our `Constants.kt`)
4. Enable **Hide ads**, **Bypass PairIP license check**, and **Custom branding**
5. **App icon**: Original (stock lime plus) or Custom (Morphe-style blue plus)
6. Patch → Install

### After GitHub publish

1. Open: `https://morphe.software/add-source?github=hammadhassan94/ary-live`  
   or paste `hammadhassan94/ary-live` in Manager sources
2. Same select APK → Hide ads → Patch → Install

**Signature note:** Morphe resigns the APK. You cannot update over the Play Store install.  
Uninstall stock first, **or** also enable an official/community **Change package name** patch for side-by-side.

---

## 6. What this patch does

Same client-side strip as the Lab APK:

- Interstitials
- Banners / native (`AdLoaderHelper`)
- Revive (`ads.aryzap.com`)
- Home feed injectors
- IMA preroll (`AdsLoader` → null)

Does **not** unlock paid / TVOD / DRM.

---

## 7. When ARY releases a newer version

1. Download new stock APK
2. Confirm package still `com.release.arylive`
3. Add `AppTarget(version = "X.Y.Z")` in  
   `patches/src/main/kotlin/app/arylive/patches/shared/Constants.kt`
4. Re-test fingerprints (class names usually stay clear)
5. Commit `feat: support ARY PLUS X.Y.Z` and push
