# Quran Database (MySQL) – Structured Quran Text Dataset for Developers

![License](https://img.shields.io/badge/License-MIT-green)
![Database](https://img.shields.io/badge/Database-MySQL-orange)
![Encoding](https://img.shields.io/badge/Encoding-UTF8MB4-blue)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

This repository provides a **ready-to-import MySQL database containing the text of the Holy Quran** for developers who need a reliable, structured Quran dataset.

The database includes:

- Arabic Quran text **with Tashkeel (diacritics)**  
- Arabic Quran text **without Tashkeel (plain)**  
- Optional English translations of meaning (separate SQL files)

This project allows teams to integrate Quran data into websites, mobile apps, research tools, and educational platforms **without building the database layer from scratch**.

---

## 🔹 Official Project

Repository: https://github.com/webuccinoco/quran_mysql_database  

⚠️ This is the official repository of this dataset.

---

## 📑 Table of Contents

- [Project Overview](#project-overview)
- [Recognition](#recognition)
- [What’s Included](#whats-included)
  - [chapters Table](#chapters-table)
  - [verses Table](#verses-table)
  - [Translation SQL Files](#translation-sql-files-translations)
- [Database Encoding](#database-encoding)
- [Prerequisites](#prerequisites)
- [How to Use](#how-to-use)
- [Optional Translations](#optional-translations)
- [Roadmap](#roadmap)
- [License](#license)
- [Ownership](#ownership)

---

## Project Overview

The aim of this project is to help teams integrate the Holy Quran text into their infrastructure quickly and consistently.

The project is released under the **MIT License**, allowing usage in both commercial and non-commercial applications.

---

## Recognition

Resource files used to generate this database are based on the **quran-layers** project by BigProf:

https://github.com/bigprof-software/quran-layers

Credit is given to the original authors for their work.

---

## What’s Included

The main file:

```
quranDB.sql
```

Contains two core tables:

---

### chapters Table

Stores Surah metadata:

- `id` – Surah number (1–114)  
- `arabic_name` – Arabic Surah name (Unicode)  
- `english_transliteration` – English transliteration of the Surah name  
- `english_translation` – English meaning of the Surah name  

> Expected rows: **114**

---

### verses Table

Stores each Ayah linked to its Surah:

- `id` – Auto-increment row ID  
- `chapter_id` – Surah number (FK → chapters.id)  
- `verse_number` – Ayah number within the Surah  
- `arabic_text_tashkeel` – Arabic text with diacritics  
- `arabic_text_plain` – Arabic text without diacritics  

---

### Translation SQL Files (`translations/`)

Each translation is provided as a separate SQL file.

Naming pattern:

```
translations/{translation_name}.sql
```

Each translation table contains:

- `id` – Auto-increment row ID  
- `chapter_id` – Surah number  
- `verse_number` – Ayah number  
- `english_text` – Translation of meaning  

Translations are optional and can be imported independently.

---

## Database Encoding

All Arabic text is stored using:

```
utf8mb4
```

This ensures correct preservation of Arabic characters and diacritics.

---

## Prerequisites

- MySQL Server  
  https://www.mysql.com/

- MySQL Client  
  - https://www.phpmyadmin.net/  
  - https://www.heidisql.com/  
  - https://www.mysql.com/products/workbench/

> Tip: Local stacks such as **XAMPP**, **WAMP**, or **MAMP** include MySQL and phpMyAdmin.

---

## How to Use

1. Clone or download the repository:

```
git clone https://github.com/webuccinoco/quran_mysql_database.git
```

or

Download ZIP → Extract

2. Create a database (optional)

The file `quranDB.sql` is designed to **create the database automatically** during import (in the next step) using the name:

```
QuranDB
```

If you are fine with this default behavior, you can **skip this step** and move directly to **Step 3 (Import)**.

---

### If you prefer to create the database manually

Create a database named:

```
QuranDB
```

Using the following charset and collation (recommended for Arabic Quran text):

```sql
CREATE DATABASE QuranDB
CHARACTER SET utf8mb4
COLLATE utf8mb4_0900_as_cs;
```

> **Why this matters**  
> - `utf8mb4` fully supports Arabic characters and Quranic diacritics (Tashkeel).  
> - `utf8mb4_0900_as_cs` is accent-sensitive and case-sensitive, ensuring exact storage and matching of Quran text.

If your MySQL version is **older than 8.0**, you may use:

```sql
CREATE DATABASE QuranDB
CHARACTER SET utf8mb4
COLLATE utf8mb4_unicode_cs;
```

---

### Using a different database name

If you want to use a different database name than `QuranDB`, open the file:

```
quranDB.sql
```

and replace all occurrences of:

```
QuranDB
```

with your preferred database name **before importing**.

3. Import:

```
quranDB.sql
```

This file will only create the DB if it dose not exist then creates tables and inserts all data in it.

---

## Optional Translations

After importing the main database, you may import any translation file from:

```
translations/
```

> ⚠️ Important  
> Some translations permit commercial use while others are limited to non-commercial usage.  
> Always verify the license of each translation before using it in commercial projects.

---

### Included Translation Metadata

| ID | Title | Translator | Year | Description |
|----|------|------------|------|-------------|
| 1 | The Clear Quran | Dr. Mustafa Khattab | 2015 | Contemporary English translation focused on clarity and accessibility. |
| 2 | The Koran Interpreted | Arthur John Arberry | 1955 | Literary English translation aiming to reflect rhythm and style of Arabic. |

---

## Roadmap

- Add more translations  
- Add verse transliteration (Arabic → Latin)  
- Add Juz', Hizb, Sajdah, and other traditional Quran structure tables  
- Add topics, tags, and thematic linking  
- Add cross-verse references  

---

## License

MIT License

