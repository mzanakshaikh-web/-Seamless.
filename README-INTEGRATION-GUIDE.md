# Android Gradle integration pack

## What this pack does

This pack supplies starter Gradle configuration and a GitHub Actions workflow
for an Android project using Kotlin DSL. The selected versions are a compatible
baseline: Android Gradle Plugin 8.7.3, Gradle 8.9, Kotlin Android plugin 2.0.21,
and JDK 17.

The GitHub workflow installs Gradle 8.9 and runs `gradle assembleDebug`, so it
does not require a committed `gradlew` wrapper to start a CI build.

## Important compatibility limitation

Only these original project files were available for inspection:
- README.md
- ic_widget_prev.xml
- ic_widget_infinity.xml

Those files do not reveal the real application ID/namespace, source package,
Android manifest, app module layout, dependencies, SDK requirements, or whether
the project uses additional Gradle plugins. Therefore, this pack cannot
guarantee a successful build until matched to the complete original project.

## Before using

1. Back up your existing repository.
2. Extract this ZIP into the repository root, preserving existing source files.
3. Do not overwrite existing Gradle files if your project already has working
   Gradle configuration; compare and merge instead.
4. In `app/build.gradle.kts`, replace `com.example.aistudioapp` in BOTH
   `namespace` and `applicationId` with the actual values used by your app.
5. Confirm that the app module is really named `app` and is located at `app/`.
6. Keep your existing `app/src/main/AndroidManifest.xml`, Kotlin/Java source,
   resources, and required dependencies. This pack does not create or replace
   those application files.
7. Add the dependencies required by your actual source code to the
   `dependencies {}` block in `app/build.gradle.kts`.
8. Commit and push. GitHub Actions will run from the Actions tab.

## Included copies of your two supplied vector icons

The original icon XML files are included under:
- `app/src/main/res/drawable/ic_widget_prev.xml`
- `app/src/main/res/drawable/ic_widget_infinity.xml`

If these resources already exist in your project, keep one copy only. These are
resource assets and do not provide the Android app source or manifest.

## Gradle wrapper (recommended for local Android Studio use)

The CI workflow in this pack installs Gradle directly and does not require
`gradlew`. For a conventional Android Studio project, generate and commit the
wrapper using an installed Gradle 8.9:

    gradle wrapper --gradle-version 8.9

Commit the generated `gradlew`, `gradlew.bat`, `gradle/wrapper/gradle-wrapper.jar`,
and `gradle/wrapper/gradle-wrapper.properties`. Then local builds can use:

    ./gradlew assembleDebug

## Gemini API key

The original README mentions a `.env` file containing `GEMINI_API_KEY`.
Creating `.env` does not automatically make the key available to Android/Kotlin
code. The app's existing source/build setup must explicitly consume it.

Do not embed a permanent private Gemini API key in a public APK: client-side
secrets can be extracted. For production, use a protected backend/proxy or an
appropriate server-side design. A GitHub Actions secret is configured under
Repository Settings > Secrets and variables > Actions.

## Expected repository layout

    .github/workflows/main.yml
    app/build.gradle.kts
    app/src/main/AndroidManifest.xml        # keep from original project
    app/src/main/java/...                   # keep from original project
    app/src/main/res/...                    # keep from original project
    build.gradle.kts
    settings.gradle.kts
    gradle.properties

The build will fail if the original manifest, source code, required dependencies,
or correct package configuration are missing.
