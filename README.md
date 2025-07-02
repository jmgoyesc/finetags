# finetags

**finetags** is a Kotlin + Spring Boot backend that extracts transactions from PDF bank statements. Users can upload files, view parsed data, and define custom tags to organize expenses—ideal for preparing personal tax reports in Germany.

---

## 🚀 Features

- Upload PDF bank statements (local only)
- Extract structured transaction data (date, reference, value, type)
- Track processing status per file
- Query extracted data by process ID
- Fully in-memory (no persistence)
- Designed for easy expansion to tagging, aggregation, and AWS deployment

---

## 📦 Tech Stack

- **Kotlin** + **Spring Boot** (REST API)
- **Apache PDFBox** (PDF text extraction)
- **In-memory storage** (no database)
- JSON-based REST communication

---

## 🔧 Running the App

### Prerequisites

- Java 17+
- Gradle (or use the Gradle wrapper)

### Run with Gradle

```bash
./gradlew bootRun
```

The app will start at `http://localhost:8080`

---

## 📂 API Endpoints

### `POST /finetags/api/v1/process`
Upload a PDF file and create a processing job.

**Request:** `multipart/form-data`
```bash
curl -F "file=@statement.pdf" http://localhost:8080/finetags/api/v1/process
```

**Response:**
```json
{ "processId": "d5c3d328-fcf0-4b3c-9182-7c34e3c84741" }
```

---

### `GET /finetags/api/v1/process/{id}`
Fetch metadata and extracted transaction data for a process.

**Response:**
```json
{
  "process": {
    "id": "d5c3d328-...",
    "fileName": "bank_march.pdf",
    "uploadedAt": "2025-06-22T16:55:00Z",
    "status": "COMPLETED",
    "messages": []
  },
  "data": {
    "numberOfItems": 45,
    "period": {
      "from": "2024-03",
      "to": "2024-03"
    },
    "transactions": [
      {
        "date": "2024-03-01",
        "reference": "REWE MARKET",
        "amount": 75.32,
        "type": "DEBIT"
      }
    ]
  }
}
```

---

## 🛣 Roadmap

- [x] Local backend processing
- [ ] User-defined tagging and notes
- [ ] Dynamic grouping and totals
- [ ] Simple rule-based label inference
- [ ] React single-page frontend (SPA)
- [ ] AWS deployment (Lambda + S3 + API Gateway)

---

## 💬 Contributing

This project is built for learning and personal tax prep. If you're interested in contributing parsing logic for other banks or enhancing the rule inference engine, feel free to open issues or PRs.
