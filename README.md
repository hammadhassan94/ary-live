# ARY Live

Community patches for **ARY PLUS** (`com.release.arylive`) for use with [Morphe](https://morphe.software).

> Not affiliated with ARY Digital or the Morphe project.  
> Do **not** brand this as “Morphe patches” (see [NOTICE](NOTICE)).

This is a **community patch source** (like Adobo / De-ReVanced).  
It is **not** part of [MorpheApp/morphe-patches](https://github.com/MorpheApp/morphe-patches) (YouTube, Reddit, …).

## Patches

| App | Package | File type | Verified version | Patch |
| :--- | :--- | :--- | :--- | :--- |
| ARY PLUS | `com.release.arylive` | **APK** (single) | **3.8.0** | **Hide ads**, **Custom branding** |

Reddit in official Morphe is often a **split** APKM — Manager merges it.  
ARY PLUS phone builds are a normal **single APK**; no merge step.

### Hide ads

Disables interstitial, banner, native, Revive, home-feed injectors, and IMA preroll.  
Shows a short **Ad skipped** toast when an ad would have loaded or played (throttled so the home feed does not spam).  
Does **not** unlock paid / TVOD / DRM.

### Custom branding

Same idea as official Morphe YouTube/Reddit:

| Option | Result |
|--------|--------|
| **App icon → Original** | Real ARY PLUS lime plus |
| **App icon → Custom** | Morphe-style blue plus |

App name defaults to **ARY PLUS**. Change it in Morphe Manager patch options if you want.

## Add in Morphe Manager

After you publish this repo:

```text
https://morphe.software/add-source?github=hammadhassan94/ary-live
```

1. Select stock **ARY PLUS 3.8.0**
2. Enable **Hide ads**, **Bypass PairIP license check**, and **Custom branding**
3. Under **Custom branding** → **App icon**: **Original** (real logo) or **Custom** (Morphe-style)
4. Patch → Install

## Deploy

Full steps (GitHub + build `.mpp` + Manager): see **[LISTING.md](LISTING.md)** (community list) and **[DEPLOY.md](DEPLOY.md)**.

```powershell
# after gpr.user / gpr.key are set:
.\gradlew.bat buildAndroid
# → patches\build\libs\patches-*.mpp
```

## Layout

```text
patches/src/main/kotlin/app/arylive/
  patches/shared/Constants.kt       # package + version for Manager
  patches/arylive/ads/Fingerprints.kt
  patches/arylive/ads/HideAdsPatch.kt
  util/BytecodeUtils.kt
```

## License

[GPLv3](LICENSE) — see [NOTICE](NOTICE) for Morphe naming rules.
