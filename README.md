# Organizational Management System (Data Modeling)

## 🚀 Key Highlights
- Designed normalized relational schema  
- Supported hierarchical organization structure  
- Ensured data consistency across entities

--- 

## 🔗 Entity Relationship Diagram (Simplified)
<img width="1536" height="1024" alt="Entity-relationship diagram of organizational system" src="https://github.com/user-attachments/assets/3e062c24-5aaa-4ecf-a077-1bc5add0be1b" />

---

## 📌 Overview
This project demonstrates the design of a **relational data model** for an organizational management system, focusing on handling **hierarchical structures, roles, and position assignments**.

The system is designed to support complex organizational relationships while ensuring **data integrity, scalability, and efficient querying**.

---

## 🎯 Problem Statement
Organizations require a system to manage:
- Organizational structures (departments, divisions, units)
- Job roles and position types
- Assignment of personnel to positions
- Hierarchical relationships between entities  

Challenges include:
- Representing **hierarchical data** in relational databases  
- Managing **one-to-many and many-to-many relationships**  
- Ensuring **data consistency across multiple entities**

---

## 💡 Solution
Designed a **normalized relational schema** that:
- Separates organizational entities, roles, and personnel  
- Supports hierarchical relationships  
- Enables efficient querying for reporting and management  

---

## 🧩 Data Model

### Core Entities:
- `organisasi` → organizational units  
- `organisasi_jenis_jabatan` → role/position types within organization  
- `pejabat` → individuals assigned to positions  

---

## 🗄️ Table Structure

### organisasi
- id (PK)
- nama_organisasi
- parent_id (self-reference for hierarchy)

### organisasi_jenis_jabatan
- id (PK)
- organisasi_id (FK → organisasi.id)
- nama_jabatan

### pejabat
- id (PK)
- jenis_jabatan_id (FK → organisasi_jenis_jabatan.id)
- nama_pejabat
- periode_mulai
- periode_selesai

---

## 🔑 Key Design Decisions

### 1. Hierarchical Structure (Self-Referencing)
- `organisasi.parent_id` enables tree-like structures  
- Supports multi-level organizational hierarchy  

### 2. Separation of Concerns
- Organization structure separated from roles  
- Roles separated from assigned individuals  

### 3. Relationship Modeling
- One organization → many position types  
- One position type → many assigned individuals over time  

---

## ⚙️ Example Query

### Get all positions in an organization

```sql
SELECT oj.nama_jabatan
FROM organisasi o
JOIN organisasi_jenis_jabatan oj 
    ON oj.organisasi_id = o.id
WHERE o.id = :organisasiId;
```

### Get active officials
```sql
SELECT p.nama_pejabat, oj.nama_jabatan
FROM pejabat p
JOIN organisasi_jenis_jabatan oj 
    ON p.jenis_jabatan_id = oj.id
WHERE CURRENT_DATE BETWEEN p.periode_mulai AND p.periode_selesai;
```

---

## 📈 Scalability Considerations
- Indexing foreign keys for faster joins
- Handling large hierarchies with recursive queries (CTE)
- Partitioning for large historical data (optional)

---

## 🧠 Key Learnings
- Designing normalized relational schemas
- Handling hierarchical data in SQL
- Modeling real-world organizational structures
- Ensuring data consistency and flexibility

---

## 🔍 Future Improvements
- Add audit logs for changes
- Implement soft deletes
- Introduce role-based access control (RBAC)
- Optimize hierarchical queries using recursive CTE

---

## 📬 About Me

Backend Engineer focused on data modeling, distributed systems, and backend architecture using Laravel, Golang, and Kafka.
