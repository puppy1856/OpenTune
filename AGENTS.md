# OpenTune Agent Guidelines

This document provides essential information for AI agents working on the OpenTune codebase.

## Project Overview
OpenTune is an open-source YouTube Music client for Android.
- **Tech Stack**: Kotlin, Jetpack Compose, Material Design 3, Hilt (DI), Room (DB), Media3 (Playback), Ktor (Networking).
- **Architecture**: MVVM with a multi-module structure.
- **Target SDK**: 35 (Android 15)
- **Java Version**: 21

## Build & Development Commands
Use the Gradle wrapper (`gradlew` or `./gradlew`) for all build tasks.

| Action | Command |
| :--- | :--- |
| **Build Debug APK** | `./gradlew assembleDebug` |
| **Build Release APK** | `./gradlew assembleRelease` |
| **Run All Tests** | `./gradlew test` |
| **Run Single Test** | `./gradlew :app:testDebugUnitTest --tests "package.ClassName.methodName"` |
| **Lint Check** | `./gradlew lint` |
| **Clean Project** | `./gradlew clean` |
| **Install Debug** | `./gradlew installDebug` |

## Code Style & Conventions

### 1. General Kotlin Style
- Follow [Official Kotlin Coding Conventions](https://kotlinlang.org/docs/coding-conventions.html).
- **Indentation**: 4 spaces.
- **Naming**:
    - Classes/Objects: `PascalCase` (e.g., `MusicService`)
    - Functions/Variables: `camelCase` (e.g., `playPause()`, `currentMediaItem`)
    - Constants: `UPPER_SNAKE_CASE` (e.g., `MAX_VOLUME`)
- **Imports**: Avoid wildcards. Organize imports alphabetically (standard IDE behavior).

### 2. Jetpack Compose (UI)
- **UI Delegation**: Visual/styling changes (colors, spacing, layouts) MUST be delegated to the `frontend-ui-ux-engineer` agent.
- **Pure Logic**: Handle state management and event logic in ViewModels.
- **Dynamic Themes**: Use `themeColor` extracted from thumbnails (see `MainActivity.kt`).
- **Icons**: Prefer `painterResource` with local SVGs/drawables or `Icons.Extended`.

### 3. Architecture & Dependency Injection
- **MVVM**: View (Compose) -> ViewModel -> Repository/Database.
- **Hilt**: Use `@AndroidEntryPoint` for Activities/Services and `@HiltViewModel` for ViewModels.
- **Room**: Maintain database migrations. Current version is 19. DAOs should use `Flow` or `suspend` functions.

### 4. Concurrency & Networking
- **Coroutines**: Use `viewModelScope` for UI-related tasks and `Dispatchers.IO` for background/DB work.
- **Flow**: Use `StateFlow` for UI state and `SharedFlow` for one-time events.
- **Networking**: Use `Ktor` for API calls.

### 5. Error Handling & Logging
- **Logging**: Use `Timber`. Avoid `Log.d` or `println`.
- **Exceptions**: Use `reportException(e)` (defined in `utils/Utils.kt`) to report issues.
- **Media3**: Handle unstable API warnings with `@OptIn(UnstableApi::class)` when necessary, but prefer stable alternatives.

### 6. Git Workflow
- Use **Conventional Commits**: `feat:`, `fix:`, `docs:`, `refactor:`, `chore:`, etc.
- Always run `./gradlew lint` before finalizing changes.

## File Structure
- `app/`: Main application logic.
- `innertube/`: YouTube API implementation.
- `lrclib/`, `kugou/`: Lyrics providers.
- `material-color-utilities/`: Color extraction and theme generation.
- `gradle/libs.versions.toml`: Centralized dependency versions.
