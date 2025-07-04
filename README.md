Faculty Research Database System

https://img.shields.io/badge/MySQL-8.0-blue
https://img.shields.io/badge/Python-3.8%252B-yellow
https://img.shields.io/badge/AWS_RDS-Compatible-orange
https://colab.research.google.com/assets/colab-badge.svg

Overview
A comprehensive database system for managing faculty research profiles, publications, patents, and academic contributions. This system provides:
Structured organization of faculty research data
Efficient querying capabilities
Secure document handling
Seamless integration with Google Colab for analysis

Database Schema
Core Tables
faculty: Base information about faculty members
journal_publications: Peer-reviewed journal articles
conference_publications: Conference papers and proceedings
book_publications: Books and book chapters
patents: Patent applications and grants
research_funding: Grants and sponsored projects

Supporting Tables
faculty_development_programs: FDP/STTP participation
consultancy: Industry consultancy projects
achievements: Awards and recognitions
documents: Storage for supporting documents

Setup Instructions
1. Database Deployment
sql
-- Create database (run first)
CREATE DATABASE faculty_research_db;

-- Then run all table creation scripts from schema.sql
2. Google Colab Setup
python
# Install required packages
!pip install pymysql sqlalchemy pandas

# Configure database connection
DB_CONFIG = {
    'host': 'your-rds-endpoint.rds.amazonaws.com',
    'user': 'admin',
    'password': 'yourpassword',
    'database': 'faculty_research_db',
    'port': 3306
}
3. Data Import
python
from google.colab import files
uploaded = files.upload()
file_path = list(uploaded.keys())[0]

# Load Excel data to MySQL
load_faculty_data_from_excel(file_path)
Key Features
Comprehensive Tracking: All academic activities in one system

Powerful Querying: Find faculty by research area, publication type, etc.

Document Management: Store proofs, certificates, and supporting documents

Analysis Ready: Direct integration with Python data tools

Example Queries
python
# Get all SCOPUS publications by a faculty member
def get_scopus_publications(faculty_name):
    query = """
    SELECT j.paper_title, j.journal_name, j.publication_date 
    FROM journal_publications j
    JOIN faculty f ON j.faculty_id = f.faculty_id
    WHERE f.name = %s AND j.publication_type = 'SCOPUS'
    """
    return pd.read_sql(query, conn, params=[faculty_name])
Usage Guide
For Administrators:
Use the provided Python functions for data management
Schedule regular backups of the database
Manage user access through MySQL privileges

For Faculty:
Submit research updates via standardized Excel templates
Access personal research profiles through query interfaces
Upload supporting documents through the document system

Maintenance
Backup Strategy: Daily automated backups recommended

Performance: Index frequently queried columns

Security: Regular credential rotation advised
