
# 📦 Shared Version Catalog for Android Projects

여러 Android 프로젝트 간에 공통된 라이브러리 버전을 관리하기 위해 사용하는 **공유 `libs.versions.toml` 저장소**입니다.

## ✨ 장점

- ✅ Jetpack Compose, Hilt, Retrofit 등 주요 라이브러리의 버전을 하나의 파일에서 일관성 있게 관리 가능
- ✅ 새로운 프로젝트를 생성할 때 마다 `libs.versions.toml`를 새로 작성할 필요가 없음

---

## 📁 Repository Structure

```[README.md](../AndroidStudioProjects/SBeenVersionCatalog/README.md)
SBeenVersionCatalog/
└── LICENSE
└── README.md
└── libs.versions.toml
```

---

## 🚀 사용 방법

### ✅ 방법 1: Git Submodule로 프로젝트에 추가

프로젝트가 SBeenVersionCatalog Repository의 형상과 동기화 되어야 할 때 적합

#### 1.1. 프로젝트에 Submodule 추가

```bash
git submodule add https://github.com/KimSungBeen/SBeenVersionCatalog.git
```

#### 1.2. `settings.gradle.kts`에 다음을 추가

```kotlin
dependencyResolutionManagement {
    versionCatalogs {
        create("libs") {
            from(files("../SBeenVersionCatalog/libs.versions.toml"))
        }
    }
}
```

> `files()` 안의 경로는 현재 프로젝트 구조에 맞게 조정하세요.

#### 1.3. Gradle에서 사용 예

```kotlin
implementation(libs.androidx.core.ktx)
implementation(libs.retrofit.core)
```

---

### ✅ 방법 2: 저장소를 별도로 Clone

독립적으로 버전 카탈로그를 사용하고 싶을 때 적합

#### 2.1. 프로젝트 외부에 Clone

```bash
git clone https://github.com/KimSungBeen/SBeenVersionCatalog.git
```

#### 2.2. `libs.versions.toml` 파일을 프로젝트에서 참조

`settings.gradle.kts`에서 외부 경로를 직접 지정:

```kotlin
dependencyResolutionManagement {
    versionCatalogs {
        create("libs") {
            from(files("../SBeenVersionCatalog/libs.versions.toml"))
        }
    }
}
```

혹은 필요 시 원하는 위치로 `libs.versions.toml` 파일만 복사해서 사용해도 됨.

---

## 🧩 포함된 라이브러리 예시

- Jetpack Compose
- Kotlin Coroutines
- Retrofit / OkHttp
- Hilt
- Coil
- Test: JUnit / Espresso / Mockk / Turbine 등

---

## 📌 Versioning Rule

- Major: (patch 버전이 아닌) `kotlin` 또는 `androidGradlePlugin`의 버전의 변경이 있을 때
- Minor: 새로운 라이브러리 의존성이 추가될 때
- Patch: 기존에 존재하는 라이브러리의 버전의 변경이 있을 때 
