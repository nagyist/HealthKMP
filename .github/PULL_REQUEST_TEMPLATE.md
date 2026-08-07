## Summary
<!-- Provide a brief overview of the changes introduced in this PR -->

## Type of Change
- [ ] 🚀 New Feature (non-breaking change introducing new functionality)
- [ ] 🐛 Bug Fix (non-breaking change fixing an issue)
- [ ] 🎨 Refactoring / Code Quality Improvement
- [ ] 📝 Documentation Update
- [ ] 🔧 Build / CI Configuration Update

## Checklist & Conventions
Please verify the following before submitting your PR:

- [ ] **Alphabetical (A-Z) Order**: All new types, extension functions, `when` branches, and sample screens are kept in strict A-Z order.
- [ ] **Naming Alignment**: Function and parameter names follow Health Connect / platform standards (e.g. `read<Type>`, `write<Type>`, `aggregate<Type>`, `aggregate<Type>GroupByDuration`).
- [ ] **Sample App Updated**: `sample/composeApp` has been updated with UI controls/views for testing this feature.
- [ ] **Platform Purity**: No `java.*`, `android.*`, or `UIKit`/`Foundation` imports in `commonMain`.
- [ ] **Tests Added**: Unit tests added in `commonTest`, `androidHostTest` (Health Connect mapping), and `appleTest` (HealthKit mapping).
- [ ] **API Dump Updated**: Ran `./gradlew :health:apiDump` and committed the generated `.api` / `.klib.api` files.
- [ ] **Local Verification**: Passed `./gradlew :health:apiCheck :health:allTests`.

## Screenshots / Video (If UI / Sample App changed)
<!-- Attach screenshots or videos demonstrating sample app updates if applicable -->
