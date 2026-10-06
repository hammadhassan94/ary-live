# Short publish checklist

Full guide: **[DEPLOY.md](DEPLOY.md)**

1. Identity is `hammadhassan94` / repo `ary-live`
2. `%USERPROFILE%\.gradle\gradle.properties` → `gpr.user` + `gpr.key` (PAT with `read:packages`) for local Gradle only
3. `.\gradlew.bat buildAndroid` → get `.mpp`
4. `gh repo create ary-live --public --source=. --remote=origin --push`
5. Share: `https://morphe.software/add-source?github=hammadhassan94/ary-live`
