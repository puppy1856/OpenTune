# OpenTune 專案上下文 (GEMINI.md)

## 專案概述
**OpenTune** 是一款基於 Material Design 3 的高級 Android 版 YouTube Music 客戶端。它旨在提供無廣告、高效能且注重隱私的音樂體驗，功能包括歌詞同步、背景播放、智慧跳過片段及動態主題色彩。

- **核心技術棧**: Kotlin (2.1.0), Jetpack Compose, Material Design 3 (Material You), Hilt, Media3 (ExoPlayer), Room, Ktor, OkHttp, Coil, NewPipe Extractor.
- **目標平台**: Android 6.0 (SDK 24) 及以上版本。
- **開發語言**: Kotlin (主要), Java 21 (工具鏈)。

## 專案架構與模組
專案採用多模組 Gradle 結構：

- **`:app`**: 主 Android 應用程式模組，包含 UI (Compose)、ViewModel 及 Hilt 依賴注入設置。
- **`:innertube`**: YouTube InnerTube API 的封裝庫，使用 Ktor 進行通訊，整合了 NewPipe Extractor。
- **`:kugou` / `:lrclib`**: 歌詞搜尋與下載服務模組。
- **`:kizzy`**: Discord Rich Presence (RPC) 整合，用於在 Discord 上顯示正在播放的音樂。
- **`:material-color-utilities`**: 用於實現 Material You 動態色彩生成的工具庫。
- **`:jossredconnect`**: 連線服務相關模組。

## 建置與執行指令
使用 Gradle 封裝器 (`./gradlew` 或 `gradlew.bat`) 執行以下指令：

- **建置測試版 APK**: `./gradlew :app:assembleDebug`
- **建置發行版 APK**: `./gradlew :app:assembleRelease` (需配置環境變數中的簽名金鑰)
- **執行單元測試**: `./gradlew test`
- **專案清理**: `./gradlew clean`
- **Lint 檢查**: `./gradlew lint`

## 開發規範與慣例
- **UI 框架**: 嚴格使用 Jetpack Compose。
- **依賴注入**: 使用 Hilt 進行依賴管理。
- **資料持久化**: 使用 Room Database 處理本地資料庫，DataStore 處理偏好設置。
- **播放邏輯**: 使用 Media3 MediaSession 和 ExoPlayer 處理音樂播放與後台服務。
- **版本控制**: 使用 `gradle/libs.versions.toml` 統一管理依賴庫版本。
- **程式碼風格**: 遵循 Kotlin 官方慣例，優先使用 Kotlin DSL (`.kts`) 進行 Gradle 配置。

## 關鍵檔案路徑
- **`app/src/main/java/com/arturo254/opentune`**: 主程式邏輯與 UI 實作。
- **`gradle/libs.versions.toml`**: 專案所有庫與外掛程式的版本清單。
- **`app/build.gradle.kts`**: 應用程式主配置與依賴項。
- **`README.md`**: 專案詳細功能說明與編譯指南。

---
*本文件由 Gemini CLI 自動生成，用於為 AI 提供專案開發背景。*
