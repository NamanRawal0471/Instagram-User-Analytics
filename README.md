### **Instagram User Analytics 📊**

This project focuses on analyzing Instagram user data to extract valuable insights for **marketing strategies**, **user engagement**, and **investor-driven metrics**. Using **SQL** and **MySQL Workbench**, the project aims to provide actionable information to optimize Instagram's business operations and user experience.

---

## **Overview**  
As a data analyst working with the product team at Instagram, your goal is to analyze user interactions and engagement on the platform. The insights derived can help the marketing, product, and development teams make **informed decisions** for the app's growth.  

The project is divided into two key sections:  

1. **Marketing Insights**: Analyze user data to identify loyal users, optimize ad campaigns, and enhance user engagement.  
2. **Investor Metrics**: Calculate engagement metrics and detect anomalies like fake accounts to maintain platform integrity.

---

## **Project Objectives**

### **1. Marketing Insights**  
- **Loyal User Reward**:  
   Identify the **Top 5 oldest users** who have been active on Instagram the longest.  
   ```sql
   SELECT username, created_at 
   FROM users 
   ORDER BY created_at ASC 
   LIMIT 5;
   ```

- **Inactive User Engagement**:  
   Find users who have **never posted a single photo** and target them for re-engagement.  
   ```sql
   SELECT username 
   FROM users 
   LEFT JOIN photos ON users.id = photos.user_id 
   WHERE photos.id IS NULL;
   ```

- **Contest Winner Declaration**:  
   Determine the user with the **most likes on a single photo**.  
   ```sql
   SELECT users.username, photos.id AS photo_id, COUNT(*) AS total_likes
   FROM photos
   JOIN likes ON likes.photo_id = photos.id
   JOIN users ON photos.user_id = users.id
   GROUP BY photos.id
   ORDER BY total_likes DESC
   LIMIT 1;
   ```

- **Hashtag Research**:  
   Identify the **Top 5 most commonly used hashtags** for marketing campaigns.  
   ```sql
   SELECT tags.tag_name, COUNT(*) AS usage_count
   FROM tags
   JOIN photo_tags ON tags.id = photo_tags.tag_id
   GROUP BY tags.tag_name
   ORDER BY usage_count DESC
   LIMIT 5;
   ```

- **Ad Campaign Launch**:  
   Determine the **best day of the week** to launch ad campaigns based on user registrations.  
   ```sql
   SELECT DAYNAME(created_at) AS day_of_week, COUNT(*) AS user_count
   FROM users
   GROUP BY day_of_week
   ORDER BY user_count DESC;
   ```

---

### **2. Investor Metrics**  
- **User Engagement**:  
   Calculate the **average posts per user** and the total number of photos per user.  
   ```sql
   SELECT COUNT(*) / (SELECT COUNT(*) FROM users) AS avg_posts_per_user
   FROM photos;
   ```

- **Bots & Fake Accounts**:  
   Identify users who have **liked every photo** on the platform, as they are likely fake accounts.  
   ```sql
   SELECT user_id, username, COUNT(*) AS total_likes
   FROM users
   JOIN likes ON users.id = likes.user_id
   GROUP BY likes.user_id
   HAVING total_likes = (SELECT COUNT(*) FROM photos);
   ```

---

## **Tools & Technologies Used**  
- **MySQL Workbench 8.0 CE**: Used for executing SQL queries and data analysis.  
- **SQL**: To write queries for extracting and analyzing data.

---

## **Insights Gained**  
1. **Loyal Users**: Oldest active users can be rewarded to enhance brand loyalty.  
2. **Inactive Users**: Identifying users with no posts helps target re-engagement strategies.  
3. **Trending Hashtags**: Helps in optimizing marketing campaigns by leveraging popular hashtags.  
4. **Optimal Ad Timing**: Launching ads on days with high user registrations can maximize reach.  
5. **Fake Accounts Detection**: Ensures platform integrity by flagging suspicious users.  
6. **Engagement Metrics**: Understanding average posts per user helps evaluate overall user activity.

---

## **How to Run the Project**  
1. Import the provided **database** into MySQL Workbench.  
2. Run the SQL queries for each task to analyze the data.  
3. Capture the outputs and document the results for reporting.  

---

## **Results**  
This project provides insights into Instagram's user base, helping stakeholders optimize marketing efforts, enhance user engagement, and maintain platform quality.  

---

## **Tech Stack**  
- **SQL**  
- **MySQL Workbench**  

---

### **Key Learnings**  
This project demonstrates the power of SQL in deriving actionable insights from raw data. It enhances understanding of database querying, data analysis, and reporting for business decision-making.

---  
**By**: Naman Rawal 🚀
