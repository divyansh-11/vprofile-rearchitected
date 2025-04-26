# vprofile-rearchitected

Re-architecting the vProfile project using AWS services. This project showcases DevOps practices, CI/CD, and AWS infrastructure automation.

---

## Prerequisites

- JDK 17 or 21  
- Maven 3.9  
- MySQL 8  

---

## Technologies Used

- Spring MVC  
- Spring Security  
- Spring Data JPA  
- Maven  
- JSP  
- Tomcat  
- MySQL  
- Memcached  
- RabbitMQ  
- Elasticsearch  

---

## Database Setup

We use MySQL as the database. To import the schema:

**SQL dump file:**
- Located at: `/src/main/resources/db_backup.sql`

**To import:**
```bash
mysql -u <user_name> -p accounts < db_backup.sql
