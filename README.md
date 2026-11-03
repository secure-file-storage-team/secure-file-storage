# 🔐 Қауіпсіз файлдарды сақтау және алмасу жүйесі
### Secure File Storage & Sharing System

## 📌 Жоба туралы

Бұл жоба — пайдаланушылардың файлдарын қауіпсіз сақтауға, жүктеуге, жүктеп алуға және басқа пайдаланушылармен бөлісуге арналған ақпараттық жүйе.

Жүйенің басты ерекшелігі — файлдар серверге жіберілмей тұрып, клиент жағында шифрланады. Осылайша, қоймада файлдардың тек шифрланған нұсқасы сақталады.

Жоба Java 17+, Spring Boot, PostgreSQL, MinIO және Java Cryptography Architecture (JCA) технологиялары негізінде әзірленеді.

## 🎯 Жобаның мақсаты

Пайдаланушылардың деректерін рұқсатсыз қол жеткізуден қорғау және файлдармен қауіпсіз алмасу мүмкіндігін қамтамасыз ету.

**Негізгі міндеттері:**
- Файлдарды AES-GCM алгоритмі арқылы шифрлау.
- Құпиясөз негізінде PBKDF2 арқылы криптографиялық кілт алу.
- SHA-256 арқылы файлдың тұтастығын тексеру.
- RSA көмегімен файлдарды қауіпсіз бөлісу.
- Мерзімі шектелген сілтемелер жасау.
- Файлдардың бірнеше нұсқасын сақтау.
- Электрондық цифрлық қолтаңбаны қолдану.
- Пайдаланушылардың құқықтары мен әрекеттерін бақылау.

## ⚙️ Қолданылатын технологиялар

| Технология | Қолданылу мақсаты |
|---|---|
| Java 17+ | Негізгі бағдарламалау тілі |
| Spring Boot | REST API серверін құру |
| JCA | Криптографиялық операциялар |
| AES-256-GCM | Файлдарды шифрлау |
| PBKDF2 | Құпиясөзден кілт алу |
| SHA-256 | Файл тұтастығын тексеру |
| RSA-OAEP | Шифрлау кілтін қауіпсіз бөлісу |
| RSA-PSS | Электрондық қолтаңба |
| PostgreSQL | Деректер базасы |
| MinIO | Шифрланған файлдарды сақтау |
| Maven | Тәуелділіктерді басқару |
| JUnit 5 | Автоматты тестілеу |
| GitHub Actions | CI/CD және тестілеуді автоматтандыру |

## 🏗️ Жүйенің архитектурасы

Жүйе бірнеше негізгі модульден тұрады:

1. **Client Application** — пайдаланушымен өзара әрекеттесетін консольдік немесе JavaFX қосымшасы.
2. **Cryptography Library** — шифрлау, дешифрлау, хэштеу және цифрлық қолтаңба операциялары.
3. **REST Server** — клиент пен сервер арасындағы сұраныстарды өңдеу.
4. **Database** — пайдаланушылар, файлдар және рұқсаттар туралы ақпаратты сақтау.
5. **MinIO Vault** — шифрланған файлдарды сақтау қоймасы.
6. **Security & Audit** — қолжетімділікті басқару және әрекеттерді тіркеу.
7. **Testing & CI** — тестілеу және автоматтандырылған тексеру.

### Архитектура диаграммасы
```mermaid
flowchart TD
    A["Пайдаланушы"] --> B["Client Application"]
    B --> C["Cryptography Library"]
    C --> D["AES-GCM"]
    C --> E["PBKDF2"]
    C --> F["SHA-256"]
    C --> G["RSA"]
    B --> H["REST API Server"]
    H --> I["Authentication and Permissions"]
    H --> J[("PostgreSQL")]
    H --> K[("MinIO Vault")]
    H --> L["Audit Logs"]
    M["GitHub Actions"] --> N["Automated Tests"]

## 📊 UML диаграммалары

### 1. Use Case Diagram — жүйені пайдалану сценарийлері

Бұл диаграмма пайдаланушы мен әкімшінің жүйеде қандай әрекеттер орындай алатынын көрсетеді.
```mermaid
flowchart LR
    U["Пайдаланушы"]
    A["Әкімші"]

    U --> UC1["Жүйеге кіру"]
    U --> UC2["Файл жүктеу"]
    U --> UC3["Файлды жүктеп алу"]
    U --> UC4["Файлды бөлісу"]
    U --> UC5["Сілтеме жасау"]
    U --> UC6["Тұтастықты тексеру"]
    U --> UC7["Файл нұсқаларын басқару"]
    U --> UC8["Цифрлық қолтаңба"]

    UC2 --> UC9["Файлды шифрлау"]
    UC3 --> UC10["Файлды дешифрлау"]

    A --> UC11["Пайдаланушыларды басқару"]
    A --> UC12["Аудит журналын қарау"]

### 2. Component Diagram — жүйе компоненттері
```mermaid
flowchart TB
    C["Client Application"]
    CR["Cryptography Library"]
    API["Spring Boot REST Server"]
    AUTH["Authentication Module"]
    AUDIT["Audit Module"]
    DB[("PostgreSQL")]
    MINIO[("MinIO Vault")]

    C --> CR
    C --> API
    API --> AUTH
    API --> AUDIT
    API --> DB
    API --> MINIO

### 3. Class Diagram — жүйе кластары
```mermaid
classDiagram
    class User {
        UUID id
        String username
        String passwordHash
        login()
        logout()
    }

    class FileMetadata {
        UUID id
        String fileName
        String storageKey
        String sha256Hash
        createFile()
        deleteFile()
    }

    class EncryptionService {
        encryptFile()
        decryptFile()
        deriveKey()
    }

    class SharingService {
        shareFile()
        generateLink()
        revokeLink()
    }

    class SignatureService {
        signFile()
        verifySignature()
    }

    class AuditService {
        recordEvent()
        getAuditLogs()
    }

    class FileVersion {
        UUID versionId
        int versionNumber
        Date createdAt
    }

    User "1" --> "*" FileMetadata
    FileMetadata "1" --> "*" FileVersion
    EncryptionService --> FileMetadata
    SharingService --> FileMetadata
    SignatureService --> FileMetadata
    AuditService --> User

### 4. Sequence Diagram — файлды қауіпсіз жүктеу
```mermaid
sequenceDiagram
    actor User
    participant Client
    participant Crypto
    participant API
    participant DB
    participant MinIO

    User->>Client: Файлды таңдау
    Client->>Crypto: Кілт алу
    Crypto->>Crypto: PBKDF2
    Crypto-->>Client: Дайын кілт
    Client->>Crypto: Файлды шифрлау
    Crypto->>Crypto: AES-GCM
    Crypto->>Crypto: SHA-256
    Crypto-->>Client: Шифрланған файл
    Client->>API: Файлды жіберу
    API->>MinIO: Файлды сақтау
    MinIO-->>API: Сақтау нәтижесі
    API->>DB: Метадеректерді сақтау
    DB-->>API: Сақталды
    API-->>Client: Сәтті орындалды
    Client-->>User: Файл қауіпсіз сақталды

## 🔒 Қауіпсіздік мүмкіндіктері
```mermaid
| Функция | Сипаттамасы |
|---|---|
| AES-GCM | Файлдарды шифрлау және аутентификациялау |
| PBKDF2 | Құпиясөз негізінде криптографиялық кілт алу |
| SHA-256 | Деректердің тұтастығын тексеру |
| RSA-OAEP | Кілттерді қауіпсіз бөлісу |
| RSA-PSS | Электрондық цифрлық қолтаңба |
| Expiring Links | Мерзімі шектелген сілтемелер |
| Access Control | Қолжетімділік құқықтарын басқару |
| Audit Logs | Жүйедегі әрекеттерді тіркеу |

**Қауіпсіздік талаптары:**
- Файлдар серверге жіберілмей тұрып шифрланады.
- MinIO қоймасында тек шифрланған файлдар сақталады.
- Құпиясөздер мен жеке кілттер GitHub-қа жүктелмейді.
- Әр файл үшін бірегей nonce қолданылады.
- Сервермен байланыс HTTPS арқылы қорғалады.

## 📁 Жоба құрылымы
```mermaid
```text
secure-file-storage/
│
├── client/
├── server/
├── crypto-library/
├── database/
├── docs/
│   └── diagrams/
├── tests/
├── .github/
│   └── workflows/
│       └── ci.yml
│
├── README.md
├── LICENSE
├── .gitignore
└── pom.xml
```

## 🧪 Тестілеу және CI/CD

Жоба аясында кемінде 20 JUnit 5 тест жазылады.

Тестілеу бағыттары:
- AES-GCM шифрлау және дешифрлау.
- PBKDF2 кілт алу.
- SHA-256 тұтастықты тексеру.
- RSA кілттерін генерациялау және бөлісу.
- Электрондық қолтаңбаны тексеру.
- Файл нұсқаларын басқару.
- Қол жеткізу құқықтарын тексеру.
- Мерзімі өткен сілтемелерді тексеру.
- Қате құпиясөздер мен бүлінген файлдарды өңдеу.

GitHub Actions арқылы әр Pull Request және Push кезінде автоматты тестілеу жүргізіледі.

## 🌿 Git жұмыс тәртібі

Команда Git Flow негізіндегі жұмыс тәртібін қолданады.

- `main` — жобаның тұрақты нұсқасы.
- `develop` — әзірлеу жұмыстары біріктірілетін тармақ.
- `feature/*` — жеке функцияларды әзірлеуге арналған тармақтар.

Барлық өзгерістер Pull Request арқылы енгізіледі. Код кемінде бір команда мүшесінің Code Review тексеруінен өтуі керек.

## 📅 Жобаның орындалу кезеңдері

| Sprint | Жұмыс мазмұны |
|---|---|
| Sprint 1 | Жоспарлау, архитектура, UML, GitHub және Trello баптау |
| Sprint 2 | Шифрлау, файл сақтау, бөлісу және деректер базасы |
| Sprint 3 | Қауіпсіздікті күшейту, тестілеу, CI/CD және қорғау |

## 👥 Команда құрамы

| Қатысушы | Рөлі |
|---|---|
| Әуелбек Бақытжан | Team Lead |
| Кейін анықталады | Backend Developer |
| Кейін анықталады | Cryptography Developer |
| Кейін анықталады | Database Developer |
| Кейін анықталады | QA / Testing |

## 📌 Жоба мәртебесі

**Ағымдағы кезең:** Жоспарлау және архитектура

**Жоба ұзақтығы:** 1 ай

**Команда:** Secure File Storage Team

## 📜 Лицензия

Бұл жоба MIT License лицензиясы негізінде әзірленеді.
