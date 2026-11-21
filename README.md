# Dr. Baysinger – F-Droid хранилище

Собствено F-Droid хранилище за **Real BC**, **Sound BC** и **SlugSpeed**.
Всеки ден GitHub Actions взема последния APK от релийзите на трите репота, подписва индекса и го публикува на GitHub Pages.

**Адрес за F-Droid:** `https://smouky577.github.io/fdroid/repo`

Няма `.bat` файл. Хранилището се пуска от GitHub: Actions → **Update F-Droid repo** → Run workflow.

## Еднократна настройка

### 1. Ключ за хранилището (отделен от main-release.jks)
PowerShell (`keytool` е в `jbr\bin` на Android Studio):

```powershell
& "D:\Android Studio\jbr\bin\keytool.exe" -genkeypair -v -keystore fdroid-repo.p12 -storetype PKCS12 -alias repokey -keyalg RSA -keysize 4096 -validity 10000 -dname "CN=Dr. Baysinger F-Droid repo"
[Convert]::ToBase64String([IO.File]::ReadAllBytes("fdroid-repo.p12")) | Set-Clipboard
```

Пазете `fdroid-repo.p12` както `main-release.jks`. Ако се загуби, потребителите трябва да добавят хранилището наново.

### 2. Secrets
GitHub → репо `fdroid` → Settings → Secrets and variables → Actions → New repository secret:

- `FDROID_KEYSTORE` – base64 текстът от клипборда
- `FDROID_KEYSTORE_PASS` – паролата от стъпка 1

### 3. Pages
Settings → Pages → Source: **GitHub Actions**

### 4. Пускане
Actions → **Update F-Droid repo** → Run workflow.

## Нова версия на апп
Качете нов релийз с APK (по-висок `versionCode`, подписан с `main-release.jks`) в репото на аппа. Хранилището го хваща до 24 часа, или веднага с Run workflow.

Последни версии: Sound BC **1.1**, Real BC **1.1**, SlugSpeed **1.2**, с новите иконки без кръг. SlugSpeed включва и поправката „празно = дуло → мишена“.

## Нов апп
Добавете името на GitHub репото в `apps.txt` и файл `metadata/<applicationId>.yml`.

---

# Dr. Baysinger – F-Droid repository

A private F-Droid repository for **Real BC**, **Sound BC** and **SlugSpeed**.
Once a day GitHub Actions takes the latest APK from each app’s releases, signs the index and publishes it on GitHub Pages.

**F-Droid address:** `https://smouky577.github.io/fdroid/repo`

There is no `.bat` file. The repository is started from GitHub: Actions → **Update F-Droid repo** → Run workflow.

## One-time setup

### 1. Repository key (separate from main-release.jks)
PowerShell (`keytool` is in Android Studio’s `jbr\bin`):

```powershell
& "D:\Android Studio\jbr\bin\keytool.exe" -genkeypair -v -keystore fdroid-repo.p12 -storetype PKCS12 -alias repokey -keyalg RSA -keysize 4096 -validity 10000 -dname "CN=Dr. Baysinger F-Droid repo"
[Convert]::ToBase64String([IO.File]::ReadAllBytes("fdroid-repo.p12")) | Set-Clipboard
```

Keep `fdroid-repo.p12` the same way you keep `main-release.jks`. If it is lost, users must add the repository again.

### 2. Secrets
GitHub → repo `fdroid` → Settings → Secrets and variables → Actions → New repository secret:

- `FDROID_KEYSTORE` – the base64 text from the clipboard
- `FDROID_KEYSTORE_PASS` – the password from step 1

### 3. Pages
Settings → Pages → Source: **GitHub Actions**

### 4. Run
Actions → **Update F-Droid repo** → Run workflow.

## A new app version
Publish a new release with an APK (higher `versionCode`, signed with `main-release.jks`) in that app’s repo. The repository picks it up within 24 hours, or immediately with Run workflow.

Latest versions: Sound BC **1.1**, Real BC **1.1**, SlugSpeed **1.2**, with the new icons and no circle. SlugSpeed also includes the “empty = muzzle → target” hint fix.

## A new app
Add the GitHub repo name to `apps.txt` and a `metadata/<applicationId>.yml` file.