# ig-request-cleaner
Cancel pending Instagram follow requests in bulk with multi-threading, random delays, and resume support.

---

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/a/a5/Instagram_icon.png" alt="Instagram Logo" width="100" />
</p>

<h1 align="center">IG Request Cleaner</h1>

<p align="center">
  IG Request Cleaner is a Python-based automation tool to
  <strong>cancel pending Instagram follow requests</strong> in bulk.<br />
  It uses <a href="https://github.com/adw0rd/instagrapi" target="_blank" rel="noopener noreferrer">instagrapi</a>
  for safe API interaction and supports <strong>multi-threading</strong>,
  <strong>random human-like delays</strong>, and <strong>resume capability</strong> —
  so you can safely manage thousands of requests without getting flagged.
</p>


---

## ✨ Features
- ✅ Cancel pending Instagram follow requests in bulk
- ✅ Multi-threading for faster execution
- ✅ Random human-like delays to avoid detection
- ✅ Resume-safe: continues from where it left off if interrupted
- ✅ Skip specific usernames automatically
- ✅ Detailed CSV logs with statuses and timestamps

---

## 📂 Project Structure
```

ig-request-cleaner/
│── pending\_follow\_requests.html   # Instagram export file
│── cancel\_follow\_requests\_log.csv # Auto-generated logs
│── ig\_request\_cleaner.ipynb       # Main Google Colab notebook
│── README.md                      # Project documentation

````

---

## 🔧 Requirements
- **Python 3.9+** (Google Colab recommended)
- **Libraries:**
  ```bash
  pip install instagrapi beautifulsoup4 pandas

---

## 📥 How to Get `pending_follow_requests.html`

Before using this tool, you need your Instagram **Pending Follow Requests** data:

1. Go to [Instagram Accounts Center](https://accountscenter.instagram.com/info_and_permissions)
2. Navigate to:
   **Settings → Privacy → Download Your Information**
3. Select **Some of Your Information** → choose **Followers and Following**.
4. Select **HTML format** → submit the request.
5. Instagram will email you a **ZIP file** — download and extract it.
6. Inside the extracted folder, locate:

   ```
   followers_and_following/pending_follow_requests.html
   ```
7. Upload this file into **Google Colab** or place it in your working directory.

---

## 🚀 How to Use in Google Colab

### **1. Install dependencies**

```bash
!pip install instagrapi beautifulsoup4 pandas
```

### **2. Login to Instagram**

```python
from instagrapi import Client
cl = Client()
cl.login("your_username", "your_password")
```

> ✅ Supports 2FA — you will be prompted for your verification code.

### **3. Upload your file**

Upload your `pending_follow_requests.html` file to Colab:

```
/content/pending_follow_requests.html
```

### **4. Run the main script**

Paste the **multi-threaded resume-safe script** from this repository into your Colab notebook and run it.

---

## ⚙️ Configuration Options

| Option          | Description                               | Default                                 |
| --------------- | ----------------------------------------- | --------------------------------------- |
| `HTML_PATH`     | Path to your pending follow requests file | `/content/pending_follow_requests.html` |
| `EXCLUDE_USERS` | Set usernames to skip                     | `{"reza.frxond"}`                      |
| `MAX_WORKERS`   | Number of parallel threads                | `3`                                     |
| `DELAY_MIN`     | Minimum delay between actions (seconds)   | `1.8`                                   |
| `DELAY_MAX`     | Maximum delay between actions (seconds)   | `4.6`                                   |
| `LOG_CSV`       | CSV log file path                         | `cancel_follow_requests_log.csv`        |

---

## 📊 Logs & Output

The script automatically creates a CSV log:

```
cancel_follow_requests_log.csv
```

Each entry contains:

* **username**
* **user\_id**
* **status** → `canceled`, `api_false`, `exception`, `resolve_failed`, `dry_run`
* **message**
* **timestamp**

**Example:**

| username    | user\_id | status    | message             | timestamp        |
| ----------- | -------- | --------- | ------------------- | ---------------- |
| john\_doe   | 12345678 | canceled  |                     | 2025-09-09 14:31 |
| jane\_smith | 98765432 | exception | Rate limit exceeded | 2025-09-09 14:35 |

---

## ⚠️ Best Practices

* Use **small thread counts** (`MAX_WORKERS=2-3`) to avoid account restrictions.
* Keep `DELAY_MIN` and `DELAY_MAX` reasonable (e.g., `2–5 sec`).
* Always add important usernames to `EXCLUDE_USERS`.
* If you get **"Please wait a few minutes"**, increase delays and retry later.
* Use a **secondary account** if you plan to cancel thousands of requests.
