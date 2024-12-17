PROJECT1:RETAIL ORDER SALES ANALYSIS
LINK:https:https://retailordersproject1-knpxm86fw8k9rd2ihwxzrj.streamlit.app/

**Retail Order Sales Analysis Dashboard**

  This project is a Streamlit-based web application designed for analyzing and visualizing retail sales data stored in a PostgreSQL database hosted on AWS. The application provides users with insights into sales, profits, discounts, and other key performance metrics through pre-defined and custom SQL queries.

**Key Features:**

**Dynamic Query Execution:**

  Users can choose from a range of GUVI-provided and self-defined SQL queries to extract insights.

**Data Visualization:** 

  Query results are displayed in tabular format with optional charts for better analysis.
  
**
Query Categories:**

**GUVI Provided Queries:** 

  Predefined queries for common retail analysis tasks like revenue generation, profit margins, and total discounts.

**Self-Defined Queries:** 

  Custom queries for deeper insights, such as unique products sold per city or revenue by product category.


**Database Integration:** 

  Seamlessly connects to a PostgreSQL database, ensuring real-time data retrieval and analysis.

**User-Friendly UI:** 

  Intuitive interface for selecting and executing queries, powered by Streamlit.


**Technologies Used:**

**Streamlit:** 

  For building the interactive dashboard.

**PostgreSQL:** 
  
  Database for storing and querying retail data.

**Python:** 
  
  For query execution and data processing (pandas, psycopg2).




1. Libraries Import
python
Copy code
import streamlit as st
import psycopg2
import pandas as pd
streamlit: Used for building the interactive UI.
psycopg2: A library to connect and query PostgreSQL databases.
pandas: Used to process and display query results in a structured DataFrame format.
2. Database Connection Function
python
Copy code
def database_connection():
    conn = psycopg2.connect(
        host="dbproject1.cvwmae0i6nho.ap-south-1.rds.amazonaws.com",
        port="5432",
        database="dbproject1",
        user="postgres",
        password="pocketpocket"
    )
    return conn
Creates a connection to the PostgreSQL database hosted on AWS RDS.
Replace the credentials for security purposes in a production environment.
3. Query Execution Function
python
Copy code
def run_query(query):
    conn = database_connection()
    try:
        df = pd.read_sql_query(query, conn)
        return df
    except Exception as e:
        st.error(f"Error executing query: {e}")
        return None
    finally:
        conn.close()
Accepts a SQL query as input.
Fetches query results as a Pandas DataFrame.
Displays an error message on failure and ensures the connection is closed after execution.

**4. Streamlit User Interface**

st.title("RETAIL ORDER DATA ANALYSIS")
Sets the app's title.

**6. Queries**
GUVI Provided Queries:
Stored as a dictionary, these queries focus on pre-defined use cases such as:

Top revenue products
Profit margins by city
Discounts, sales price averages, etc.

Example:

"Find the top 10 highest revenue-generating products": 
    'select r2.product_id,sum(r2.sale_price * r2.quantity) as total_revenue ...'
SELF Provided Queries:
Custom queries designed to solve additional data insights such as:

Total orders per region
Revenue by product category
Top cities by revenue

**6. Query Navigation**
nav = st.radio("choose a Query", ["GUVI Provided Queries", "SELF Provided Queries"])
A radio button lets users choose between GUVI or custom queries.
Displays query options as a dropdown list based on selection.

**7. Query Execution and Visualization**
if query:
    getting_result = run_query(choose_a_query_section[query])
    if getting_result is not None:
        st.dataframe(getting_result)
Fetches results for the selected query.
Displays the output in a dataframe table using Streamlit.




  


