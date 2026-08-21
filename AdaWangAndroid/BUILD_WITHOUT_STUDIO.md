# Bina APK tanpa Android Studio

## Cara paling mudah: GitHub Actions (percuma)

1. Cipta akaun di https://github.com (percuma)
2. New repository → nama `AdaWangAndroid` (Public atau Private)
3. Upload semua fail dalam folder `AdaWangAndroid` (atau push zip extract)
4. Pergi tab **Actions** → pilih **Build AdaWang APK** → **Run workflow**
5. Tunggu 3–5 minit
6. Klik run yang selesai → **Artifacts** → muat turun **AdaWang-APK**
7. Extract → dapat `app-debug.apk` → pasang pada telefon

Tiada Android Studio. Tiada SDK. Hanya GitHub.

---

## Cara 2: Telefon (tidak bina APK, guna web)

PWA / “Add to Home screen” — anda kata tidak mahu ini.

---

## Cara 3: PC tanpa Android Studio (command line)

Perlu JDK 17 + Android command-line tools (besar, ~1GB).
Lebih mudah guna GitHub Actions di atas.

---

## Pasang APK pada telefon

1. Settings → Security → benarkan **Install unknown apps**
2. Buka fail `app-debug.apk`
3. Install → buka **AdaWang**

---

## Notifikasi push

Untuk push, anda PERLU:
1. Firebase project + `google-services.json` sebenar
2. Kod FCM (ada dalam README versi penuh)
3. Bina semula APK

APK semasa (tanpa Studio) = app WebView penuh ke https://adawang.my/
