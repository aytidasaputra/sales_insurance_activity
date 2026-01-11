# sales_insurance_activity

# Setup Flutter - Sales Activity Asuransi

## 1. Install Flutter

### Windows:
```bash
# Download Flutter SDK dari https://flutter.dev/docs/get-started/install/windows
# Extract ke C:\src\flutter
# Tambahkan ke PATH: C:\src\flutter\bin

flutter doctor
```

### macOS/Linux:
```bash
# Clone repository
git https://github.com/aytidasaputra/sales_insurance_activity.git 
export PATH="$PATH:`pwd`/flutter/bin"

flutter doctor
```

## 2. Masuk ke Folder

```bash
cd sales_insurance_activity
```

## 3. Struktur Folder Project

```
sales_insurance_activity/
├── lib/
│   ├── main.dart
│   ├── models/
│   │   ├── product.dart
│   │   ├── activity.dart
│   │   ├── customer.dart
│   │   └── sales.dart
│   ├── screens/
│   │   ├── splash_screen.dart
│   │   ├── login_screen.dart
│   │   ├── home_screen.dart
│   │   ├── products/
│   │   │   ├── product_list_screen.dart
│   │   │   └── product_detail_screen.dart
│   │   ├── activities/
│   │   │   ├── activity_list_screen.dart
│   │   │   ├── add_activity_screen.dart
│   │   │   └── activity_detail_screen.dart
│   │   ├── customers/
│   │   │   ├── customer_list_screen.dart
│   │   │   └── customer_detail_screen.dart
│   │   └── profile/
│   │       └── profile_screen.dart
│   ├── widgets/
│   │   ├── custom_app_bar.dart
│   │   ├── product_card.dart
│   │   ├── activity_card.dart
│   │   └── custom_button.dart
│   ├── services/
│   │   ├── api_service.dart
│   │   ├── auth_service.dart
│   │   └── database_service.dart
│   ├── providers/
│   │   ├── auth_provider.dart
│   │   ├── product_provider.dart
│   │   └── activity_provider.dart
│   ├── utils/
│   │   ├── constants.dart
│   │   ├── colors.dart
│   │   └── helpers.dart
│   └── config/
│       ├── routes.dart
│       └── theme.dart
├── assets/
│   ├── images/
│   ├── icons/
│   └── fonts/
├── pubspec.yaml
└── README.md
```

## 4. Update pubspec.yaml

```yaml
name: sales_insurance_activity
description: Aplikasi Sales Activity untuk 16 Produk Asuransi
publish_to: 'none'
version: 1.0.0+1

environment:
  sdk: '>=3.0.0 <4.0.0'

dependencies:
  flutter:
    sdk: flutter
  
  # State Management
  provider: ^6.1.1
  
  # UI Components
  cupertino_icons: ^1.0.2
  google_fonts: ^6.1.0
  flutter_svg: ^2.0.9
  
  # Network
  http: ^1.1.0
  dio: ^5.4.0
  
  # Local Storage
  shared_preferences: ^2.2.2
  sqflite: ^2.3.0
  path_provider: ^2.1.1
  
  # Forms & Validation
  flutter_form_builder: ^9.1.1
  form_builder_validators: ^10.0.1
  
  # Date & Time
  intl: ^0.19.0
  
  # PDF & Documents
  pdf: ^3.10.7
  printing: ^5.11.1
  
  # Image
  image_picker: ^1.0.5
  cached_network_image: ^3.3.0
  
  # Charts
  fl_chart: ^0.65.0
  
  # Utils
  uuid: ^4.2.2
  url_launcher: ^6.2.2

dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^3.0.0

flutter:
  uses-material-design: true
  
  assets:
    - assets/images/
    - assets/icons/
  
  # fonts:
  #   - family: CustomFont
  #     fonts:
  #       - asset: assets/fonts/CustomFont-Regular.ttf
  #       - asset: assets/fonts/CustomFont-Bold.ttf
  #         weight: 700
```

## 5. Install Dependencies

```bash
flutter pub get
```

## 6. Konfigurasi Android (android/app/build.gradle)

```gradle
plugins {
    id "com.android.application"
    id "kotlin-android"
    // The Flutter Gradle Plugin must be applied after the Android and Kotlin Gradle plugins.
    id "dev.flutter.flutter-gradle-plugin"
}

android {
    namespace = "com.salesinsurance.activity"
    compileSdk = 34
    ndkVersion = "25.1.8937393"

    compileOptions {
        sourceCompatibility = JavaVersion.VERSION_1_8
        targetCompatibility = JavaVersion.VERSION_1_8
    }

    kotlinOptions {
        jvmTarget = "1.8"
    }

    defaultConfig {
        applicationId = "com.salesinsurance.activity"
        minSdk = 21
        targetSdk = 34
        versionCode = 1
        versionName = "1.0.0"
        
        // Multidex support untuk aplikasi dengan banyak dependencies
        multiDexEnabled true
        
        // Vector drawable support
        vectorDrawables.useSupportLibrary = true
    }

    buildTypes {
        debug {
            applicationIdSuffix ".debug"
            debuggable true
            minifyEnabled false
            shrinkResources false
        }
        
        release {
            // Untuk production, gunakan signing config Anda sendiri
            // signingConfig = signingConfigs.release
            
            // Sementara gunakan debug signing untuk testing
            signingConfig = signingConfigs.debug
            
            minifyEnabled true
            shrinkResources true
            
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
    
    // Flavor untuk berbagai environment (optional)
    flavorDimensions "environment"
    productFlavors {
        dev {
            dimension "environment"
            applicationIdSuffix ".dev"
            versionNameSuffix "-dev"
        }
        
        staging {
            dimension "environment"
            applicationIdSuffix ".staging"
            versionNameSuffix "-staging"
        }
        
        production {
            dimension "environment"
        }
    }
    
    // Packaging options
    packagingOptions {
        exclude 'META-INF/DEPENDENCIES'
        exclude 'META-INF/LICENSE'
        exclude 'META-INF/LICENSE.txt'
        exclude 'META-INF/license.txt'
        exclude 'META-INF/NOTICE'
        exclude 'META-INF/NOTICE.txt'
        exclude 'META-INF/notice.txt'
        exclude 'META-INF/ASL2.0'
        exclude 'META-INF/*.kotlin_module'
    }
}

flutter {
    source = "../.."
}

dependencies {
    // Multidex support
    implementation 'androidx.multidex:multidex:2.0.1'
}
```

## 7. Permissions (android/app/src/main/AndroidManifest.xml)

```xml
<manifest>
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.CAMERA"/>
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
</manifest>
```

## 8. Data Model - 16 Produk Asuransi

Contoh produk asuransi:
1. Asuransi Jiwa
2. Asuransi Kesehatan
3. Asuransi Pendidikan
4. Asuransi Kendaraan
5. Asuransi Properti
6. Asuransi Perjalanan
7. Asuransi Kecelakaan Diri
8. Asuransi Pensiun
9. Asuransi Investasi
10. Asuransi Kebakaran
11. Asuransi Kredit
12. Asuransi Bisnis
13. Asuransi Syariah
14. Asuransi Unit Link
15. Asuransi Dwiguna
16. Asuransi Mikro

## 9. Run Project

```bash
# Check devices
flutter devices

# Run on connected device
flutter run

# Run on specific device
flutter run -d <device_id>

# Build APK
flutter build apk --release

# Build App Bundle
flutter build appbundle --release
```

## 10. Tips Development

1. **Hot Reload**: Press `r` saat running untuk reload cepat
2. **Hot Restart**: Press `R` untuk restart aplikasi
3. **Debug**: Gunakan `print()` atau `debugPrint()`
4. **Format Code**: `flutter format .`
5. **Analyze Code**: `flutter analyze`

## Next Steps

1. Setup Firebase (optional untuk backend)
2. Implementasi authentication
3. Desain UI/UX untuk setiap screen
4. Integrasi dengan API backend
5. Implementasi local database dengan SQLite
6. Testing dan debugging

---

**Catatan**: Struktur ini dirancang scalable dan mudah di-maintain untuk aplikasi sales activity dengan multiple produk asuransi.