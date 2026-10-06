# ARY Live

Community patches for **ARY PLUS** (`com.release.arylive`), for use with [Morphe](https://morphe.software).

Not affiliated with ARY Digital or the Morphe project. See [NOTICE](NOTICE).

## About

Hide ads, bypass PairIP on resigned sideload, and optional Original/Custom app icon for ARY PLUS 3.8.0.

### How to use these patches

Click here to add these patches to Morphe: https://morphe.software/add-source?github=hammadhassan94/ary-live

Or add this repository as a patch source in Morphe Manager: `hammadhassan94/ary-live`

## Patches list

A list of patches will automatically be shown here after the first release is created.

## Getting development started

To start using this template, follow these steps:

1. [Setup](https://github.com/MorpheApp/morphe-documentation/blob/main/docs/morphe-development/README.md) your development environment including adding a GitHub PAT as described [here](https://github.com/MorpheApp/morphe-patcher/blob/main/docs/2_1_setup.md#-prepare-the-environment).
2. Enable "Allow GitHub Actions to create and approve pull requests" in repo Settings > Actions > General > Workflow permissions.
3. Update the [build.gradle.kts](patches/build.gradle.kts) file (group and About).
4. Update this README and the links in the [issue templates](.github/ISSUE_TEMPLATE).
5. Keep a name that does not imply authorship by the Morphe project. See [NOTICE](NOTICE).
6. (Optional): Add `patches-bundle.png` for a custom icon in Morphe Manager.

## Dev usage

To develop and release patches using this template:

- **Make all changes to the `dev` branch.**
- For local development build with `./gradlew buildAndroid`. The `.mpp` is in `patches/build/libs/patches-*.mpp`.
- Always use [semantic commits](https://kapeli.com/cheat_sheets/Semantic_Commits.docset/Contents/Resources/Documents/index):
  - `feat: Added a new feature`
  - `fix: Some problem now fixed`
  - `chore: Random change you do not want in the user facing changelog`
- `fix:` and `feat:` create pre-releases on `dev`. `chore:` does not create a release.
- Users can apply `dev` releases by enabling pre-release in Morphe Manager.
- When `dev` is ready for a stable release, merge `dev` into `main` (do not squash).
- **Always use semantic release (`release.yml`)**. Do not create releases by hand.

## Tips

- See the [patcher documentation](https://github.com/MorpheApp/morphe-patcher/blob/main/docs/1_patcher_intro.md).
- Do not rewrite `release.yml` from scratch. Modify the existing files if needed.
- Do not manually edit or commit generated files after CI is live: `patches-list.json`, `patches-bundle.json`, `CHANGELOG.md`.
- Do not force push semantic-release commits.

### Building locally

- Run `./gradlew buildAndroid`
- Output: `patches/build/libs/patches-*.mpp`
- Patch with [Morphe Desktop](https://github.com/MorpheApp/morphe-desktop)

See the [Morphe documentation](https://github.com/MorpheApp/morphe-documentation).

## License

ARY Live is licensed under the [GNU General Public License v3.0](LICENSE)
