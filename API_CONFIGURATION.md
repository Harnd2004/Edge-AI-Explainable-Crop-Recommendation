# API configuration

The app's optional weather and news integrations use compile-time Dart defines.

```bash
flutter run --dart-define=OPENWEATHER_API_KEY=your_key --dart-define=NEWS_API_KEY=your_key
```

Do not commit real keys. Rotate keys that were previously exposed in source control. Client-side keys can be extracted from a compiled mobile application; use provider restrictions or a backend proxy for production.
