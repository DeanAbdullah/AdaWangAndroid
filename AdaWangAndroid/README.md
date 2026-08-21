# AdaWang Android App (WebView)

Aplikasi Android sebenar (APK) yang memuatkan https://adawang.my dalam skrin penuh — seperti app native, **bukan PWA**.

## Ciri
- Skrin penuh (tiada bar alamat pelayar)
- JavaScript, cookie, login kekal
- Tarik turun untuk refresh
- Muat naik fail (KYC / resit)
- Butang Back ikut sejarah laman
- Deep link `https://adawang.my/...`
- Paparan offline + butang Cuba Lagi
- Pautan luar (Telegram, WhatsApp, tel) dibuka di app sistem

## Syarat
1. [Android Studio](https://developer.android.com/studio) (Giraffe atau lebih baharu)
2. JDK 17
3. Telefon Android atau emulator

## Cara bina APK

### Dalam Android Studio
1. File → Open → pilih folder `AdaWangAndroid`
2. Tunggu Gradle sync selesai
3. **Build → Build Bundle(s) / APK(s) → Build APK(s)**
4. APK debug: `app/build/outputs/apk/debug/app-debug.apk`

### APK Release (untuk kongsi / install)
1. Build → Generate Signed Bundle / APK
2. Pilih **APK** → cipta keystore baharu (simpan password!)
3. Build release → `app/build/outputs/apk/release/app-release.apk`

### CLI
```bash
cd AdaWangAndroid
./gradlew assembleDebug
# atau
./gradlew assembleRelease
```

## Pasang pada telefon
1. Aktifkan **Sumber tidak diketahui** / Install unknown apps
2. Pindah `app-debug.apk` ke telefon
3. Ketik fail APK → Install

## Ubah URL (jika perlu)
Edit `MainActivity.kt`:
```kotlin
const val BASE_URL = "https://adawang.my/"
```

## Ikon app
Ganti fail dalam `app/src/main/res/mipmap-*/ic_launcher.png`  
atau gunakan Android Studio: File → New → Image Asset

## Nota
- Ini **bukan** PWA — ia fail APK yang dipasang seperti app biasa.
- Kandungan sentiasa dari website; kemas kini laman = app ikut berubah.


---

## Notifikasi Push (Firebase)

App ini menyokong **Firebase Cloud Messaging (FCM)**.

### Setup Firebase (wajib sekali)

1. Buka [Firebase Console](https://console.firebase.google.com/)
2. **Add project** → nama `AdaWang`
3. **Add app** → Android  
   - Package name: `my.adawang.app`  
   - Download **`google-services.json`**
4. Ganti fail:
   ```
   AdaWangAndroid/app/google-services.json
   ```
   (padam fail placeholder, letak fail dari Firebase)
5. Sync Gradle → Build APK semula

### Uji notifikasi

1. Firebase Console → **Messaging** → **Create your first campaign**
2. Notification title/body → hantar ke topic `all_users`  
   atau ke token peranti (lihat Logcat: `FCM token: ...`)

### Payload data (pilihan)

| Key | Contoh | Fungsi |
|-----|--------|--------|
| `title` | Loan diluluskan | Tajuk |
| `body` | Permohonan AW-xxx diluluskan | Mesej |
| `url` | https://adawang.my/check-loan-status.php | Buka halaman dalam app |

### Topic automatik
App subscribe kepada:
- `all_users` — semua pengguna
- `loan_updates` — kemas kini pinjaman

### Hantar dari server (PHP contoh)

```php
// Perlu Server Key / OAuth dari Firebase
$payload = [
  'message' => [
    'topic' => 'all_users',
    'notification' => [
      'title' => 'AdaWang',
      'body'  => 'Anda ada kemas kini baharu',
    ],
    'data' => [
      'url' => 'https://adawang.my/account.php',
    ],
  ],
];
```

Versi app: **1.1.0** (versionCode 2)
