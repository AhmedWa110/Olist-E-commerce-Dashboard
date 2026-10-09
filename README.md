# Olist E-Commerce Analytics Dashboard With Power BI

![NEXUS Dashboard – Command Center](/pic1.png)

## Introduction

Olist is a **20-page Power BI analytics suite** built for **E-Commerce Leaders, Operations Managers, Marketing Teams, and Data Analysts** who need one place to understand how a Brazilian online marketplace is performing. Using a star-schema model of orders, payments, reviews, logistics and marketing-funnel data, the report connects revenue, customers, delivery, sellers, products and lead generation in a single, easy-to-navigate interface.

The project is delivered as a **Power BI Project (PBIP)** with a fully documented semantic model of **130+ DAX measures**, so every page, KPI and visual can be traced and rebuilt.

---

## Skills Showcased

This project was a deep dive into building a production-style Power BI solution. Here's what it covers:

-   **🏗️ Data Modeling:** Designed a star schema with **13 tables** (5 facts, 5 dimensions, 1 date table, 1 measures table, 1 marketing channel table) and **13 active + 9 inactive relationships**.
-   **🧮 Advanced DAX:** Built **130+ measures** in a dedicated `MyMeasures` table, including `Total Revenue`, `AOV`, `Revenue CAGR`, `Repeat Rate`, `On-Time Delivery %`, and `MQL Conversion Rate`.
-   **⏱️ Time Intelligence:** Implemented **YoY, QoQ and MoM** trend measures, plus `USERELATIONSHIP` for role-playing dates (delivery, carrier, shipping and won-date analysis).
-   **🎯 Dynamic KPI Cards:** Every KPI uses a **Value → Trend % → Arrow → Color** measure chain for consistent, conditional storytelling.
-   **📊 Core & Advanced Charts:** Line, Area, Clustered Bar/Column, Donut, Pie, Treemap, Waterfall, Scatter, and Matrix (cohort heatmap) visuals.
-   **🗺️ Geospatial Analysis:** **Azure Maps** bubble maps to visualize customer and revenue concentration across Brazil.
-   **🔮 Forecasting Scenarios:** Base, optimistic and pessimistic revenue projections with CAGR context.
-   **🖱️ Interactive Reporting:**
    -   **Slicers:** 6 standard slicers (Date, Customer State, Seller State, Product Category, Order Status, Payment Type).
    -   **Active Filters Indicator:** A live count of how many slicers are currently filtering the report.
    -   **Drilldowns & Tooltips:** Category- and state-level detail with contextual tooltip measures.
-   **✅ Validation & Traceability:** A full Page → KPI → Visual → Measure → DAX → Table → Relationship map for every element.

---

### Page 1: Command Center

![Page 1 – Command Center](/pic1.png)

The executive landing page, It gives a quick pulse check on the whole business with four headline KPIs, each paired with a year-over-year trend, arrow and color indicator.

**KPI Cards**

| KPI | Measure | Trend |
| --- | --- | --- |
| Total Revenue (GMV) | `SUM(line_total)` | Revenue YoY % |
| Total Orders | `DISTINCTCOUNT(order_id_bk)` | Orders YoY % |
| Total Customers | `DISTINCTCOUNT(customer_sk)` | Customers YoY % |
| Avg Review Score | `AVERAGE(review_score)` | Review Score YoY % |

**Supporting Visuals**

-   **Revenue Quarterly Trend** (Line Chart): How revenue moves quarter over quarter.
-   **Orders Quarterly Trend** (Line Chart): Mirrors the revenue chart for order volume.
-   **Geographic Customer Distribution** (Azure Map): Bubble map of customers by Brazilian state, sized by `Total Customers`.


### Page 2: Revenue Intelligence

![Page 2 – Revenue Intelligence](/pic2.png)

A deep dive into where the money comes from and how fast it is growing.

**KPI Cards:** `Total Revenue`, `AOV` (Total Revenue ÷ Total Orders), `Revenue per Customer`, and `Revenue CAGR` (compound annual growth across the full date range).

**Supporting Visuals**

-   **Monthly Revenue** (Area Chart)
-   **Top Revenue Categories** (Clustered Bar, sorted descending)
-   **Revenue by Payment Type** (Donut: credit card, boleto, voucher, debit card)
-   **Revenue by State** (Clustered Bar with `State Revenue %` tooltip)

### Page 3: Customer 360

![Page 3 – Customer 360](/pic3.png)

A complete customer profile covering acquisition, value, geography and loyalty.

**KPI Cards:** `Total Customers`, `Revenue per Customer`, `Top Revenue State` (text KPI using `TOPN`), and `Repeat Rate` (customers with more than one order).

**Supporting Visuals**

-   **Customer Geo Distribution** (Azure Map)
-   **Revenue per Customer by State** (Clustered Column)
-   **New vs Returning Customers** (Pie Chart)
-   **Top Cities by Customer Count** (Clustered Bar)
-   **New Customer Acquisition Trend** (Line Chart)


---

## Pages 6–20 at a Glance

The remaining pages extend the same KPI-card + supporting-visual pattern across the rest of the business.

| Page | Name | Focus |
| --- | --- | --- |
| 06 | **Retention & Cohort** | Repeat rate, avg orders per customer, cohort retention heatmap, new vs repeat revenue |
| 07 | **Logistics Intelligence** | Avg delivery days, on-time %, days to ship, variance vs a **12-day target** |
| 08 | **Geo Intelligence** | Revenue concentration by state, regional delivery challenges, interactive Brazil map |
| 09 | **Order Lifecycle** | Order funnel from placement to delivery, fulfillment and cancellation rates |
| 10 | **Status Intelligence** | Delivered vs cancelled vs unavailable orders, cancellation drivers by category and state |
| 11 | **Seller Hub** | Active sellers, revenue per seller, top performers, seller satisfaction |
| 12 | **Product Intelligence** | Category count, quality scoring, revenue concentration |
| 13 | **Category Mix Analyzer** | Top category, share trends, YoY growth, mix concentration over time |
| 14 | **Payment Intelligence** | Transactions by payment type, credit card and boleto share, avg payment value |
| 15 | **Installment Analysis** | Avg and max installments, adoption by category and state |
| 16 | **Marketing Funnel** | MQL → deal pipeline, conversion rate, days to close, SDR performance |
| 17 | **Channel Attribution** | Channel efficiency, best-performing channel, declared revenue, attribution table |
| 18 | **Temporal Intelligence** | Peak/weak months, day-of-week patterns, holiday lift, seasonality |
| 19 | **Forecasting Engine** | Base, optimistic and pessimistic revenue scenarios, CAGR context, YTD actuals |
| 20 | **Cross-Domain Insights** | Anomaly count, composite risk score, operational health index, scatter analysis |

---

## Data Model Summary

-   **Fact tables:** `fact_order_items`, `fact_order_life_cycle`, `fact_payments`, `fact_reviews`, `fact_marketing_funnel`
-   **Dimension tables:** `dim_date`, `dim_customer`, `dim_seller`, `dim_product`, `dim_order_status`, `dim_payment_type`, `dim_marketing_channel`, plus `review_comments`
-   **Relationships:** 13 active, 9 inactive. Inactive links (shipping, carrier, delivery, estimated delivery, won date, review creation date) are activated through `USERELATIONSHIP` in the relevant measures.

## Measure Catalog

All **130+ measures** live in the `MyMeasures` table and are grouped into 11 families: Core Revenue, Customer, Order & Lifecycle, Delivery & Logistics, Review & Satisfaction, Seller, Product & Category, Payment & Installment, Marketing Funnel & Channel, Temporal & Holiday, and Cross-Domain & Composite. Each one is documented with its full DAX, format string, dependencies, and the pages/KPIs/visuals that use it.

## Validation & Project Status

| Check | Result |
| --- | --- |
| Visual JSON files | 906 ✅ |
| TMDL files | 27 ✅ |
| Page JSON files | 22 ✅ (20 report pages + 2 empty placeholders) |
| Relationships | 13 active + 9 inactive ✅ |
| Power BI Desktop open test | ⏳ Pending |

**Known follow-ups:** 14 trend measures referenced by KPI cards (for example `On-Time Delivery Trend %`, `MQL Trend %`, `Payment Value MoM %`) still need to be added to `MyMeasures.tmdl`, and about 40 unreferenced measures are flagged as safe to remove after review. Full details are in the implementation document.



## Conclusion

Olist Project shows how Power BI can turn raw marketplace data into a complete decision-making system. From a one-glance executive view to deep dives on customers, logistics, sellers, payments, marketing and forecasting, the dashboard lets users slice, filter and drill through the data to make informed, evidence-based business decisions.
