# 📊 Power BI ETL Orders – Sales Performance Dashboard

## 🚀 Project Overview

This project demonstrates an **end-to-end ETL and reporting workflow in Power BI**, starting from raw Excel data and ending with an interactive **Sales Performance Dashboard**.

The main goal is to show how transactional order data can be:

* Cleaned and transformed using **Power Query (ETL)**
* Modeled correctly with relationships (including **Persian calendar support**)
* Visualized in a **business-friendly dashboard** suitable for decision-makers

This repository is structured and versioned to reflect **real-world BI project practices**.

---

## 🎯 Business Objective

Enable sales stakeholders to:

* Monitor **Total Sales** and **Total Profit** at a glance
* Analyze sales distribution by **Country**
* Track **Monthly Sales Trends** using Persian (Shamsi) dates
* Identify **positive, break-even, and negative profit orders**
* Drill into order-level details for deeper investigation

---

## 🧩 Dataset Description

**Source:** Excel files (raw data)

**Main tables:**

* `List of Order` – high-level order information (Order ID, Country, Date, Sales, Profit, etc.)
* `OrderBreakdown` – detailed breakdown of each order
* `Persian Calendar` – mapping between Gregorian and Shamsi dates

**Key transformations applied:**

* Data type detection and standardization
* Profit categorization (Negative / Break-even / Positive)
* Country name normalization (United Kingdom → UK)
* Product name normalization using column split
* Merge & Append operations for learning and consolidation

---

## ⚙️ ETL Process (Power Query)

All transformations are implemented inside **Power Query Editor**:

1. Load Excel data via **Get Data → Excel**
2. Clean and standardize columns
3. Create **Conditional Column** for Profit Category
4. Split Product Name into main name and attribute
5. Merge order tables into a consolidated table (`Total`)
6. Append tables (educational purpose)
7. Add Persian calendar table
8. Apply **Detect Data Type** and numeric formatting

📌 No external scripts or Python dependencies are required.

---

## 🧠 Data Model

* Star-like schema
* Persian Calendar table linked to `Order Date`
* Enables Shamsi-based slicing and time analysis

---

## 📈 Dashboard Features

The main dashboard page includes:

* **KPI Cards**

  * Total Sales
  * Total Profit

* **Sales by Country**

  * Donut chart showing geographic distribution

* **Sales Data Table**

  * Order-level details with profit category highlighting

* **Monthly Sales Trend**

  * Line chart using Persian months

The layout is designed with a **clean UI**, sidebar navigation, and business-friendly visuals.

---

## 🗂️ Project Structure

```
Powerbi-ETL-Orders/
│
├── Data/
│   └── Raw Data/            # Excel source files
├── Docs/
│   ├── notes.md             # Execution notes (task-based)
│   ├── troubleshooting.md  # Issues & fixes
│   └── project-report.md   # Formal project report
├── Outputs/                 # Screenshots & exports
├── Pbix/                    # Power BI project (.pbip)
├── Scripts/                 # Optional M / helper scripts
├── README.md
├── requirements.txt
└── .gitignore
```

---

## 🛠️ Tools & Technologies

* **Power BI Desktop** (latest version)
* **Power Query (M language)**
* **Excel** (raw data & Persian calendar)
* **Git & GitHub** for version control

---

## 📌 How to Run the Project

1. Clone the repository
2. Open the `.pbip` project inside the `Pbix/` folder
3. Ensure Excel files exist in `Data/Raw Data/`
4. Click **Refresh** in Power BI
5. Explore the dashboard pages

---

## 🧪 Project Status

* ✅ Core ETL completed
* ✅ Data model created
* ✅ Initial dashboard layout implemented
* 🔄 Advanced DAX & insights (in progress)

---

## 📚 Learning Outcomes

* Practical ETL in Power BI
* Difference between Merge vs Append
* Persian calendar integration
* Git-friendly Power BI workflow
* Business-oriented dashboard design

---

## 👤 Author

**Babak Sharifyalmeh**
Data Analyst | Power BI Enthusiast

🔗 GitHub: [https://github.com/babaksharifyalmeh](https://github.com/babaksharifyalmeh)

---

*This project is part of a structured, task-based learning journey focused on real-world BI scenarios.*
