# DeKUT Campus Location Picker

A full-stack DeKUT Campus Location Picker application built with Laravel (API Backend) and Kotlin Android (`osmdroid` OpenStreetMap Engine).

---

## 1. Backend Setup & Local Server (Laravel)

### Step 1: Install Dependencies & Run Database Migrations
Navigating to the Laravel directory:
```bash
cd laravel
composer install
php artisan migrate --seed
```

### Step 2: Start the Laravel Development Server
To serve requests to physical devices and Android emulators on your Wi-Fi network:
```bash
php artisan serve --host=0.0.0.0 --port=8000
```

### Step 3: Verify GeoJSON Location API
Run `curl` or open in browser:
```bash
curl http://localhost:8000/api/locations
```
Or check system health:
```bash
curl http://localhost:8000/api/health
```

---

## 2. Android App Setup (Kotlin & osmdroid)

### Step 1: Configure `API_BASE_URL`
In `local.properties` (or `app/build.gradle.kts` / `SessionManager`):
- For Android Emulator: `http://10.0.2.2:8000/` (maps to host `localhost`).
- For Physical Android Phone: `http://<YOUR_COMPUTER_IP>:8000/` (e.g. `http://172.16.121.195:8000/`).

### Step 2: Build the Android Application
```bash
cd C:/Users/ReyR/AndroidStudioProjects/Attendee3
./gradlew assembleDebug
```

### Step 3: Run Unit Tests
```bash
./gradlew testDebugUnitTest
```

---

## 3. Architecture & Key Features
- **osmdroid OpenStreetMap Engine**: Free tile rendering centered on DeKUT Main Campus (zoom 16) with fixed center pin and live GPS readout.
- **GeoJSON `FeatureCollection`**: Standardized `[longitude, latitude]` Point coordinates served dynamically by Laravel.
- **Offline Caching**: Automatically caches fetched locations in `SharedPreferences` if the network is disconnected or server is unreachable.
- **Clean Architecture**: Organized into `ui/locationpicker/`, `data/remote/`, `data/repository/`, and `domain/`.
