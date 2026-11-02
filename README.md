# XYLEM — Edge-Powered Explainable AI Crop Recommendation

A Flutter-based smart agriculture application that combines soil and environmental inputs, on-device crop prediction, and human-readable explanations to help users understand crop recommendations.

> **Project provenance:** This repository is an independently maintained portfolio copy prepared from the project snapshot supplied by Harinand P. The supplied snapshot contains collaborative project files and existing contributor references. Do not interpret this repository as a claim that every component was individually authored by one person. Update `CONTRIBUTIONS.md` with the exact work you personally implemented before publishing.

## What is included in this code snapshot

- Flutter application with dashboard, monitoring, crop recommendation, market, weather, government-scheme and history screens.
- ONNX crop prediction model integration using seven input features: nitrogen, phosphorus, potassium, temperature, humidity, pH and rainfall.
- XAI explanation service that compares sensor values with crop-specific agronomic ranges and generates feature-level explanations, favorable factors and limiting factors.
- Local JSON prediction-history storage and statistics.
- ESP32 sensor communication/UI integration code in the Flutter application.
- English and Kannada localization resources.
- Optional weather and agricultural-news API integrations.

## Important note about explainability

The current `XAIExplanationService` in this snapshot uses crop-specific ranges, predefined feature-importance weights and rule-based impact labels to generate human-readable explanations. This is a practical explanation layer; it is **not a SHAP or LIME implementation**, and its feature-importance percentages should not be interpreted as mathematically derived model attributions. If SHAP/LIME is added later, document the exact explainer, background dataset and validation method separately.

## Technology stack

- **Mobile:** Flutter, Dart, Provider
- **ML inference:** ONNX model integration
- **Explainability:** crop-range-based feature analysis and rule-based explanations
- **Local persistence:** JSON file storage
- **Hardware connectivity:** ESP32 / sensor data integration
- **Localization:** English and Kannada

## Application screenshots

The following screenshots show the Flutter application's Kannada interface and key modules.

| Dashboard | Weather |
|---|---|
| ![Application dashboard](screenshots/app-dashboard-kannada.jpg) | ![Weather dashboard](screenshots/weather-dashboard-kannada.jpg) |

| Crop explanation | Sensor monitoring |
|---|---|
| ![Crop recommendation explanation](screenshots/crop-explanation-kannada.jpg) | ![ESP32 sensor monitoring](screenshots/esp32-sensor-monitoring.jpg) |

| Market prices | Government schemes |
|---|---|
| ![Market prices](screenshots/market-prices-kannada.jpg) | ![Government schemes](screenshots/government-schemes-kannada.jpg) |

## Repository layout

```text
.
├── assets/
│   ├── animations/
│   └── models/
├── lib/
│   ├── l10n/
│   ├── models/
│   ├── providers/
│   ├── screens/
│   ├── services/
│   ├── theme/
│   └── widgets/
├── android/
├── ios/
├── web/
├── test/
├── docs/
├── pubspec.yaml
└── README.md
```

## Run locally

### Prerequisites

- Flutter SDK compatible with the constraints in `pubspec.yaml`
- Dart SDK
- Android Studio or VS Code with Flutter extensions
- An Android device/emulator (or another Flutter-supported target)

### Setup

```bash
git clone https://github.com/<YOUR_GITHUB_USERNAME>/Edge-AI-Explainable-Crop-Recommendation.git
cd Edge-AI-Explainable-Crop-Recommendation
flutter pub get
flutter run
```

### Optional API configuration

Weather and news integrations read API keys from Dart compile-time environment values. Do not commit real keys.

```bash
flutter run \
  --dart-define=OPENWEATHER_API_KEY=your_key \
  --dart-define=NEWS_API_KEY=your_key
```

If keys are not supplied, live API features may fall back or return unavailable data. For production mobile applications, remember that compile-time values embedded in a client app can be extracted; use restricted keys or a backend proxy where appropriate.

## Model and input details

The crop model file included in `assets/models/` is `crop_prediction_model_ir9.onnx`. The current ML service constructs an input vector in this order:

1. Nitrogen
2. Phosphorus
3. Potassium
4. Temperature
5. Humidity
6. pH
7. Rainfall

The service uses the crop-label list defined in `lib/services/ml_service.dart`. Ensure that the model's training-time feature order, scaling, output shape and label order match this implementation before relying on predictions.

## Explainability and prediction history

The app generates explanations containing:
- Main reason for the recommended crop
- Feature values and configured importance weights
- Positive, negative or neutral impact labels
- Favorable and limiting conditions
- A detailed human-readable summary

Prediction history is stored locally in the app's documents directory as JSON and is managed by the prediction database service. It is not a cloud database.

## Configuration and safety checklist

Before making this repository public:

- Confirm that you have permission to publish all collaborative source files and model assets.
- Review `CONTRIBUTIONS.md` and accurately describe your own contribution.
- Rotate any API keys that were previously committed in another repository.
- Keep real API keys, passwords, Wi-Fi credentials and Firebase secrets out of source control.
- Check model and dataset licenses before redistribution.
- Validate the ONNX model's feature order, preprocessing and label mapping.
- Test on a physical device before describing hardware integration as fully working.

## Documentation in this repository

Additional implementation notes are available in:
- `XAI_AND_DATABASE_IMPLEMENTATION.md`
- `LOCALIZATION_GUIDE.md`
- `GOVT_SCHEMES_GUIDE.md`
- `NEWS_API_SETUP.md`
- `QUICK_REFERENCE.md`

Some notes may describe the state of the project at the time they were written; verify them against the current source before relying on them.

## Contributions

See [`CONTRIBUTIONS.md`](CONTRIBUTIONS.md). This repository is maintained as a personal portfolio version. Please distinguish personal implementation work from work completed collaboratively.

## License

No license was supplied with the source snapshot. Until the project contributors agree on a license, all rights remain with the respective copyright holders. Do not add an open-source license unless you have permission from the relevant contributors.
