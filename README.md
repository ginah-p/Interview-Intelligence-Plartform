# Interview Intelligence Platform 📊

A **data engineering and analytics project** that transforms interview preparation data into actionable insights through a well-designed data warehouse and ETL pipeline.

> **Built during placement season to solve a real problem: analyzing interview patterns, identifying weak topics, and making data-driven preparation decisions.**

## 🎯 Project Overview

This isn't just another CRUD app - it's a complete **data warehouse solution** that demonstrates:
- ✅ Star schema design and dimensional modeling
- ✅ ETL pipeline development
- ✅ Complex analytical queries
- ✅ Performance optimization techniques
- ✅ Data quality management

**Perfect for Data Engineering / Analytics roles!**

## 🏗️ Architecture

```
Data Sources → ETL Pipeline → Data Warehouse (Star Schema) → Analytics Layer → Dashboard
```

### Star Schema Design
```
          dim_companies
                ↓
dim_time → fact_interview_events ← dim_round_types
                ↓
          dim_questions
                ↓
          dim_topics (hierarchical)
```

## 🌟 Key Features

### Phase 1: Data Warehouse (COMPLETED ✅)
- [x] Star schema with 5 dimension tables + 1 fact table
- [x] Hierarchical topic structure (3-level taxonomy)
- [x] Date dimension for time intelligence
- [x] SCD Type 2 implementation for questions
- [x] Comprehensive indexing strategy
- [x] Pre-built analytical views

### Phase 2: ETL Pipeline (IN PROGRESS 🚧)
- [ ] Python-based data extraction
- [ ] Data validation and quality checks
- [ ] Transformation logic for data cleansing
- [ ] Incremental load implementation
- [ ] Error handling and logging

### Phase 3: Analytics & Insights (PLANNED 📋)
- [ ] 12+ analytical queries showcasing different patterns
- [ ] Performance optimization (materialized views)
- [ ] Query execution plan analysis
- [ ] Dashboard for visualization

### Phase 4: Advanced Features (PLANNED 📋)
- [ ] Data lineage tracking
- [ ] Automated pipeline orchestration
- [ ] Data quality monitoring
- [ ] Predictive analytics

## 🗄️ Database Schema Details

### Fact Table: `fact_interview_events`
**Grain**: One row per question asked in an interview round

**Key Measures**:
- Duration, difficulty rating, answer quality
- Result (passed/failed/pending)
- Preparation indicators (was_prepared, needed_hint)

### Dimension Tables

**dim_companies**: Company profiles with industry classification
**dim_time**: Date dimension (2024-2025) for time-based analysis
**dim_topics**: 3-level hierarchy (Category → Subcategory → Concept)
**dim_questions**: Question bank with SCD Type 2 for history tracking
**dim_round_types**: Interview round categorization

## 🛠️ Tech Stack

**Database & Modeling:**
- PostgreSQL (Relational database)
- Star schema dimensional modeling
- Indexing and query optimization

**Backend & ETL:**
- Python 3.x
- psycopg2 (PostgreSQL adapter)
- Pandas (Data transformation)
- SQLAlchemy (ORM - planned)

**Analytics:**
- SQL (Complex joins, window functions, CTEs)
- Analytical views and materialized views
- Aggregations and time-series analysis

**Future Additions:**
- dbt (Data Build Tool) for transformations
- Apache Airflow for orchestration
- Plotly Dash / Streamlit for dashboards
- Great Expectations for data quality

## 🚀 Getting Started

### Prerequisites
```bash
Python 3.8+
PostgreSQL 12+
pip
```

### Installation

1. **Clone the repository**
```bash
git clone  (https://github.com/ginah-p/Interview-Intelligence-Platform)
cd interview-analytics-platform
```

2. **Set up PostgreSQL database**
```bash
createdb interview_analytics
```

3. **Create virtual environment**
```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```

4. **Install dependencies**
```bash
pip install -r requirements.txt
```

5. **Initialize data warehouse**
```bash
psql -d interview_analytics -f schema/star_schema.sql
```

6. **Populate with seed data**
```bash
python scripts/seed_data.py
```

7. **Test with sample queries**
```bash
psql -d interview_analytics -f queries/sample_analytics.sql
```

## 📊 Sample Analytics Queries

This project includes 12+ analytical queries demonstrating:

1. **Aggregations**: Most frequently asked topics
2. **Joins**: Multi-table analysis across dimensions
3. **Window Functions**: Rolling 7-day performance trends
4. **Hierarchical Queries**: Topic hierarchy analysis
5. **Time-Series**: Monthly performance trends
6. **Correlation Analysis**: Preparation impact on success
7. **Ranking & Filtering**: Top weak topics needing focus
8. **Complex CTEs**: Multi-step analytical computations

**Example Query** (Topic Frequency Analysis):
```sql
SELECT 
    t.topic_name,
    COUNT(f.event_key) as times_asked,
    ROUND(100.0 * SUM(CASE WHEN f.result = 'passed' THEN 1 ELSE 0 END) / COUNT(*), 2) as success_rate
FROM fact_interview_events f
JOIN dim_questions q ON f.question_key = q.question_key
JOIN dim_topics t ON q.topic_key = t.topic_key
GROUP BY t.topic_name
ORDER BY times_asked DESC;
```

## 🎯 Data Engineering Concepts Demonstrated

### Database Design
- ✅ Dimensional modeling (star schema)
- ✅ Normalization and denormalization trade-offs
- ✅ Surrogate vs natural keys
- ✅ Slowly Changing Dimensions (SCD Type 2)
- ✅ Hierarchical data structures

### Query Optimization
- ✅ Strategic indexing on foreign keys
- ✅ Composite indexes for common query patterns
- ✅ Query execution plan analysis
- ✅ Materialized views for expensive queries

### Data Quality
- ✅ Referential integrity constraints
- ✅ Check constraints for data validation
- ✅ Default values and NOT NULL constraints
- ✅ Unique constraints for business keys

### Analytics Patterns
- ✅ Time-based analysis with date dimensions
- ✅ Cohort analysis
- ✅ Funnel analysis (interview stages)
- ✅ Trend analysis and moving averages

## 💡 Interview Discussion Points

**"Walk me through your data warehouse design"**
- Explain star schema choice over snowflake
- Discuss grain of fact table
- Justify dimension table structure

**"How did you optimize query performance?"**
- Indexing strategy (show specific indexes)
- Materialized views for expensive aggregations
- Query execution plans and bottlenecks

**"How do you handle data quality?"**
- Constraints and validation
- Data cleansing in ETL
- Monitoring and alerting (planned)

**"What would you do differently with more time?"**
- Add orchestration (Airflow)
- Implement dbt for transformations
- Build real-time ingestion pipeline
- Add data lineage tracking

## 📁 Project Structure

```
interview-analytics-platform/
├── schema/
│   ├── star_schema.sql          # Complete DDL
│   └── views.sql                # Analytical views
├── scripts/
│   ├── seed_data.py            # Sample data population
│   └── etl_pipeline.py         # ETL logic (WIP)
├── queries/
│   └── sample_analytics.sql    # 12+ analytical queries
├── docs/
│   ├── schema_diagram.png      # ER diagram
│   └── architecture.md         # Design decisions
└── requirements.txt
```

## 📸 Screenshots

_Coming soon - schema diagrams and query results_

## 📈 Project Roadmap

**Week 1**: ✅ Schema design and implementation
**Week 2**: 🚧 ETL pipeline development
**Week 3**: 📋 Analytics queries and optimization
**Week 4**: 📋 Dashboard and documentation

## 👤 Author: Chantel Pindula

- GitHub: [@ginah-p](https://github.com/ginah-p)
- LinkedIn: [Chantel Pindula](https://www.linkedin.com/in/chantel-gina-pindula-a21739238)

---

**Project Status**: ✅ Phase 1 & 2 Complete - Data Warehouse Built & Analytics Queries Implemented

**Last Updated**: November 2024

## 🎯 Current Capabilities

- ✅ 6 tables with 800+ rows of data
- ✅ 15+ strategic indexes
- ✅ 3 analytical views
- ✅ 15 complex SQL queries
- ✅ Working ETL pipeline
- ✅ Star schema fully implemented

## Sample Query Results

**Top Interview Topics:**
```
Arrays:           14 times asked, 85.71% success rate
Linked Lists:     13 times asked, 69.23% success rate
Normalization:     7 times asked, 57.14% success rate
```

**Company Performance:**
```
Google:    12 questions across multiple rounds
Microsoft: 10 questions, multiple technical rounds
Amazon:    10 questions, varied difficulty levels
```

**Keywords**: Data Engineering, Data Warehouse, Star Schema, ETL, PostgreSQL, SQL Analytics, Dimensional Modeling