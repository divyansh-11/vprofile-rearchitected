vprofile-rearchitected
Re-architecting vprofile Java project on AWS services.

🛠 What Was Done
Code was taken from this repository.

Built using Maven on local machine to generate a .war file.

Created the following AWS resources:

RDS MySQL (Database)

Elasticache Memcached (Caching layer)

Amazon MQ (RabbitMQ) (Message broker)

All backend services were kept in a Security Group named backend.

Hosted the Java application on AWS Elastic Beanstalk (using Tomcat platform).

Uploaded the .war file to Beanstalk environment.

Updated security group rules to allow access from Beanstalk to backend services.

Created AWS CloudFront distribution for faster global access.

Bought and used a custom domain *.dhop.xyz.

Created an SSL Certificate using AWS Certificate Manager (ACM).

Attached certificate to CloudFront for HTTPS.

🚀 Elastic Beanstalk Setup Details
Auto Scaling

Setting	Meaning
Minimum EC2 Instances = 2	Always run at least 2 EC2 instances (for High Availability)
Maximum EC2 Instances = 4	Allow up to 4 EC2 instances if load increases
✅ This means:

Always 2 EC2s running to ensure High Availability.

Beanstalk will auto-add more EC2 instances (up to 4) if website traffic increases.

Auto-remove extra EC2s if traffic decreases to save costs.

Beanstalk internally uses Auto Scaling Groups to monitor:

CPU usage

Network traffic

Application load

Scaling triggers new EC2s when needed and terminates them when load is low.

Rolling Updates

Setting	Meaning
Rolling Update	Beanstalk updates EC2 instances in batches
50% Batch Size	Half of the EC2 instances are updated at one time
✅ How it works:

Out of 4 instances, 2 are updated first, while 2 keep serving live traffic.

Once updated instances are healthy, the next 2 are updated.

Zero downtime during deployment.

Quick rollback if something fails during update.

⚡ This is called a Rolling Update at 50%.

🔥 Technologies Used
Java (Spring MVC, Spring Security, Spring Data JPA)

Maven

Tomcat

MySQL (RDS)

Memcached (Elasticache)

RabbitMQ (Amazon MQ)

Elastic Beanstalk

CloudFront

ACM (AWS Certificate Manager)

Route 53 (Domain)

📚 Database
We used MySQL RDS for the database.

MySQL dump file location in code:

/src/main/resources/db_backup.sql

✅ To import the dump:
mysql -u <user_name> -p accounts < db_backup.sql

🎯 Overall Architecture

Users --> CloudFront --> Elastic Beanstalk --> EC2 instances
                                  |
                        -------------------
                        |        |        |
                    RDS (MySQL)  MQ (RabbitMQ)  Elasticache (Memcached)
