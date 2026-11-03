# 🔐 Secure File Storage & Sharing System

## 📌 Жоба туралы

**Secure File Storage & Sharing System** — пайдаланушылардың файлдарын қауіпсіз сақтауға, шифрлауға және басқа пайдаланушылармен қауіпсіз бөлісуге арналған жүйе.

Жүйеде файл серверге жіберілмес бұрын Client Application жағында шифрланады. Шифрланған файл MinIO Vault қоймасында сақталады. Файлдың құпиялылығы мен тұтастығын қамтамасыз ету үшін заманауи криптографиялық алгоритмдер қолданылады.

## 🎯 Жобаның мақсаты

Пайдаланушылардың жеке файлдарын рұқсатсыз қол жеткізуден қорғау, файлдарды қауіпсіз сақтау және оларды шифрланған түрде басқа пайдаланушыларға жіберу мүмкіндігін жасау.

## ⚙️ Негізгі мүмкіндіктер

- **AES-GCM** — файлдарды қауіпсіз шифрлау және дешифрлау.
- **PBKDF2** — пайдаланушы құпиясөзінен криптографиялық кілт жасау.
- **SHA-256** — файлдың тұтастығын тексеру.
- **RSA** — файлдарды басқа пайдаланушылармен қауіпсіз бөлісу.
- **Expiring Links** — белгілі бір уақыттан кейін жарамсыз болатын сілтемелер жасау.
- **File Versioning** — файлдардың бірнеше нұсқасын сақтау және басқару.
- **Digital Signature** — файлдың цифрлық қолтаңбасын жасау және тексеру.
- **Audit Logs** — жүйедегі әрекеттер тарихын тіркеу.
- **Access Control** — пайдаланушылардың құқықтарын басқару.

## 🛠️ Қолданылатын технологиялар

| Технология | Қолданылуы |
|---|---|
| Java 17+ | Негізгі бағдарламалау тілі |
| Spring Boot | REST API Server |
| Java Cryptography Architecture (JCA) | Криптографиялық операциялар |
| AES-GCM | Файлдарды шифрлау |
| PBKDF2 | Кілтті құпиясөзден шығару |
| SHA-256 | Файл тұтастығын тексеру |
| RSA | Кілттерді қауіпсіз бөлісу |
| PostgreSQL | Мәліметтер базасы |
| MinIO | Шифрланған файлдарды сақтау |
| Maven | Project Build Management |
| JUnit 5 | Automated Testing |
| GitHub Actions | CI/CD |

## 🏗️ Жүйенің архитектурасы

Жүйе бірнеше негізгі бөліктен тұрады:

1. **Client Application** — пайдаланушы интерфейсі және файлдармен жұмыс істеу.
2. **Cryptography Library** — файлдарды шифрлау, дешифрлау және тексеру.
3. **REST API Server** — клиент пен сервер арасындағы байланысты қамтамасыз ету.
4. **PostgreSQL** — пайдаланушылар мен файлдардың метадеректерін сақтау.
5. **MinIO Vault** — шифрланған файлдарды сақтау.
6. **Audit Module** — жүйедегі әрекеттерді тіркеу.

### Architecture Diagram

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
```

## 👥 Use Case Diagram

Жүйенің негізгі пайдаланушылары мен олардың мүмкіндіктері:

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
```

## 🧩 Component Diagram

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
```

## 📦 Class Diagram

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
```

## 🔄 Sequence Diagram

Файлды қауіпсіз сақтау процесі:

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
```

## 🔒 Қауіпсіздік

Жобада келесі қауіпсіздік механизмдері қарастырылады:

- Файлдарды серверге жібермес бұрын Client-side Encryption арқылы шифрлау.
- AES-GCM алгоритмі арқылы файлдардың құпиялылығы мен тұтастығын қорғау.
- PBKDF2 көмегімен құпиясөзден криптографиялық кілт жасау.
- SHA-256 арқылы файлдың өзгертілгенін анықтау.
- RSA арқылы қауіпсіз кілт алмасуды ұйымдастыру.
- Пайдаланушылардың рұқсаттарын тексеру.
- Құпиясөздер мен кілттерді GitHub Repository ішінде сақтамау.

## 📁 Жобаның құрылымы

```text
secure-file-storage/
│
├── client/
│   └── src/
│
├── server/
│   └── src/
│
├── crypto-library/
│   └── src/
│
├── database/
│
├── docs/
│   └── diagrams/
│
├── tests/
│
├── .github/
│   └── workflows/
│
├── README.md
├── LICENSE
└── .gitignore
```

*Ескерту: Бұл — жоспарланған жоба құрылымы. Нақты папкалар мен файлдар әзірлеу барысында қосылады.*

## 🧪 Testing

Жобада JUnit 5 арқылы автоматтандырылған тестілеу жүргізіледі.

Тексерілетін негізгі функциялар:

- AES-GCM Encryption / Decryption.
- PBKDF2 Key Derivation.
- SHA-256 Integrity Verification.
- RSA Encryption / Decryption.
- Digital Signature Verification.
- File Versioning.
- Access Control.
- Expiring Links.

**Мақсат: кемінде 20 JUnit Test жазу.**

## 🔀 Git Workflow

Команда GitHub арқылы бірлесіп жұмыс істейді.

Қолданылатын Branch құрылымы:

- `main` — тұрақты нұсқа.
- `develop` — негізгі әзірлеу нұсқасы.
- `feature/*` — жеке функцияларды әзірлеу.

Жұмыс тәртібі:

1. Әр қатысушы өз Feature Branch ашады.
2. Өзгерістерін Commit арқылы сақтайды.
3. Pull Request ашады.
4. Команда мүшесі Code Review жасайды.
5. Тексерілген код `develop` Branch-ке біріктіріледі.
6. Дайын нұсқа `main` Branch-ке енгізіледі.

## 📅 Project Development Plan

Жоба үш Sprint бойынша орындалады.

### Sprint 1 — Planning & Architecture

- Жобаның талаптарын талдау.
- GitHub Repository құру.
- Trello Board дайындау.
- UML диаграммаларын әзірлеу.
- Жүйе архитектурасын анықтау.
- Project Structure дайындау.

### Sprint 2 — Core Development

- AES-GCM Encryption / Decryption.
- PBKDF2 Key Derivation.
- SHA-256 Integrity Verification.
- Spring Boot REST API.
- PostgreSQL және MinIO интеграциясы.
- Файлдарды жүктеу және жүктеп алу.

### Sprint 3 — Security & Testing

- RSA File Sharing.
- Expiring Links.
- File Versioning.
- Digital Signature.
- Audit Logs.
- JUnit Tests.
- GitHub Actions CI/CD.
- Final Documentation және Project Defense.

## 👨‍💻 Team Members

| Аты-жөні | Рөлі |
|---|---|
| Әуелбек Бақытжан | Team Lead |
| Team Member 2 | Developer |
| Team Member 3 | Developer |
| Team Member 4 | Developer |
| Team Member 5 | Developer |

*Команда мүшелерінің аты-жөні мен нақты міндеттері кейін толықтырылады.*

## 📊 Project Status

**Current Stage:** Planning & Architecture

Жоба әзірлеу кезеңінде. Функциялар Sprint жоспарына сәйкес кезең-кезеңімен жүзеге асырылады.

## 📜 License

Бұл жоба MIT License негізінде таратылады.
