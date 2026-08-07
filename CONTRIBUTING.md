# Contributing to HealthKMP

Thank you for your interest in contributing to **HealthKMP**! We welcome contributions, bug fixes, and feature additions to make Kotlin Multiplatform health data integration seamless across Android, iOS, and watchOS.

Please take a moment to review the following guidelines before submitting a Pull Request.

---

## 📐 Coding Standards & Conventions

### 1. Alphabetical (A-Z) Ordering
To keep the codebase predictable and maintainable, all data type declarations, extension functions, mapping logic, and sample screens **must be strictly kept in Alphabetical (A-Z) order**:
- `HealthDataType` enum/object declarations in [HealthDataType.kt](health/src/commonMain/kotlin/com/viktormykhailiv/kmp/health/HealthDataType.kt)
- Extension functions in `commonMain/extensions.kt` and platform-specific `extensions.kt`
- `when (type)` branching blocks in `HealthConnectManager.kt`, `HealthKitManager.kt`, and `Aggregation.kt`
- Sample app screen files in `sample/composeApp/src/commonMain/.../sample/dataType/`

### 2. Naming Conventions
- Align method and parameter names with **Health Connect** and established health platform standards (e.g., `aggregateGroupByDuration` matches Health Connect's `AggregateGroupByDurationRequest`).
- Public extension functions must adhere to the standard prefix pattern:
  - `read<DataType>()` (e.g., `readSteps()`, `readBloodPressure()`)
  - `write<DataType>()` (e.g., `writeWeight()`)
  - `aggregate<DataType>()` (e.g., `aggregateHeartRate()`)
  - `aggregate<DataType>GroupByDuration()` (e.g., `aggregateStepsGroupByDuration()`)

### 3. Platform Purity (`commonMain`)
- Code in `commonMain` **must be pure Kotlin Multiplatform code**.
- **No platform-specific imports** (`java.*`, `android.*`, `Foundation`, `UIKit`) in `commonMain`. Use KMP-native libraries like `kotlinx-datetime` and `kotlinx-coroutines`.
- Public asynchronous functions in `HealthManager` must return `Result<T>` for robust error handling.

### 4. Data Models & Named Arguments
- Record data models (e.g., `StepsRecord`, `WeightRecord`) should include input range validation (`init { require(...) }`).
- **Use named arguments** when instantiating data models (especially in unit tests) to prevent parameter swaps (e.g., systolic vs. diastolic) and improve code readability.

---

## 📱 Sample App Update Requirement

Every PR introducing a new health data type, aggregation metric, or feature **must update the sample app**:
- Update `sample/composeApp` to include UI screens and controls for testing the new data type or feature.
- Ensure empty list states (`records.isEmpty()`) are handled gracefully without causing division by zero or UI crashes.

---

## 🧪 Testing & Verification

Every feature or bug fix must include corresponding tests:
- **`commonTest`**: Unit tests for shared logic and data models.
- **`androidHostTest`**: Validation for Health Connect record mapping (runs on JVM).
- **`appleTest`**: Validation for HealthKit record mapping (shared by iOS and watchOS).

### Commands to Run Before Submitting a PR:
```bash
# 1. Update and check binary API compatibility dump
./gradlew :health:apiDump

# 2. Run API check to verify compatibility
./gradlew :health:apiCheck

# 3. Run all tests across all platforms
./gradlew :health:allTests

# 4. Verify Swift framework linking for Apple targets
./gradlew :health:linkDebugFrameworkIosArm64 :health:linkDebugFrameworkWatchosArm64
```

---

## 📌 Binary Compatibility Validator

The project uses the **Binary Compatibility Validator** to ensure public API stability. When making changes to public interfaces or data classes:
1. Run `./gradlew :health:apiDump` to update the `.api` / `.klib.api` files.
2. Commit the updated API dump files along with your code changes.

---

## 🚀 Pull Request Checklist

Before opening a Pull Request, ensure:
- [ ] Code follows **Alphabetical (A-Z) ordering** everywhere.
- [ ] Method and extension function naming matches Health Connect / platform conventions.
- [ ] `sample/composeApp` is updated with UI for testing your changes.
- [ ] Tests added in `commonTest`, `androidHostTest`, and `appleTest`.
- [ ] `./gradlew :health:apiDump` was run and `.api` files are committed.
- [ ] `./gradlew :health:apiCheck :health:allTests` passes locally.
