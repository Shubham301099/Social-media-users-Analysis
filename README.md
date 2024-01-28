# Instagram User Analytics

## Project Description

Instagram, a prominent social media platform, served as the inspiration for this project. The database, named "Instagram_ig_clone," comprises seven tables: USER, PHOTOS, COMMENTS, LIKES, FOLLOWS, TAGS, and PHOTO_TAGS. This project utilizes MySQL Workbench 8.0 CE for efficient SQL-based data exploration and extraction.

## Project Approach

The project involved cloning the dataset and executing provided commands to create the Instagram database. Leveraging various sorting and data extraction queries, insights were gathered to address specific tasks.

## Tech Stack Used

MySQL Workbench 8.0 CE was employed for its user-friendly interface, providing a visual console and improved dataset visibility.

## Project Insights

### Marketing Analysis

1. **Loyal User Reward**
   - **Task:** Find the 5 oldest users on Instagram.
   - **Query:**
     ```sql
     SELECT * FROM users
     ORDER BY created_at
     LIMIT 5;
     ```
     Output -
     
     ![image](https://github.com/Shubham301099/Social-media-users-Analysis/assets/154081009/964cdf06-3a4f-4ca8-a449-e53a79d70313)

   - **Conclusion:** Users 80, 67, 63, 95, 38 are the 5 oldest users on the platform.

2. **Inactive User Engagement**
   - **Task:** Identify users who have never posted a photo.
   - **Query:**
     ```sql
     SELECT username FROM users AS u
     LEFT JOIN photos AS p ON u.id = p.user_id
     WHERE p.id IS NULL;
     ```
     Output -
     
     ![image](https://github.com/Shubham301099/Social-media-users-Analysis/assets/154081009/cece759e-9dac-41aa-9b8f-cb144499bcb8)

     
   - **Conclusion:** 26 users have never posted a single photo on Instagram.

3. **Contest Winner Declaration**
   - **Task:** Find the user with the most likes on a single photo.
   - **Query:**
     ```sql
     SELECT username, p.id, p.image_url, COUNT(l.user_id) AS Total_likes
     FROM photos AS p
     JOIN likes AS l ON l.photo_id = p.id
     JOIN users AS u ON p.user_id = u.id
     GROUP BY p.id
     ORDER BY Total_likes DESC
     LIMIT 1;
     ```
     Output -
     
     ![image](https://github.com/Shubham301099/Social-media-users-Analysis/assets/154081009/24b481cd-c998-4462-84a9-49f0cd7494c3)

   - **Conclusion:** Zack_Kemmer93's photo has the most likes (48) on Instagram.

4. **Hashtag Research**
   - **Task:** Identify the top five most commonly used hashtags.
   - **Query:**
     ```sql
     SELECT t.tag_name, COUNT(*) AS Total
     FROM photo_tags AS pt
     JOIN tags AS t ON pt.tag_id = t.id
     GROUP BY t.id
     ORDER BY Total DESC
     LIMIT 5;
     ```
     Output -
     
     ![image](https://github.com/Shubham301099/Social-media-users-Analysis/assets/154081009/cfd581dc-dc97-4894-8e05-561bbc1f6a46)

   - **Conclusion:** Top hashtags: smile (59), beach (42), party (39), fun (38), concert (24).

5. **Ad Campaign Launch**
   - **Task:** Determine the best day to launch ads based on user registrations.
   - **Query:**
     ```sql
     SELECT DAYNAME(created_at) AS day, COUNT(*) AS Total
     FROM users
     GROUP BY day
     ORDER BY total DESC
     LIMIT 1;
     ```
     Output -
     
     ![image](https://github.com/Shubham301099/Social-media-users-Analysis/assets/154081009/4a5af5c2-0d41-435f-bbda-d0364ce79fbd)
   - **Conclusion:** Thursday is the day with the most user registrations.

### Investor Metrics

1. **User Engagement**
   - **Task:** Calculate the average number of posts per user on Instagram.
   - **Query:**
     ```sql
     SELECT (SELECT COUNT(*) FROM photos) / (SELECT COUNT(*) FROM users) AS Phtos_per_users;
     ```
     Output -
     
     ![image](https://github.com/Shubham301099/Social-media-users-Analysis/assets/154081009/d34f7d18-77d3-4bf1-b480-316b20912c71)
   - **Conclusion:** The average photos per user are 2.5700.

2. **Bots & Fake Accounts**
   - **Task:** Identify potential bots by finding users who liked every single photo.
   - **Query:**
     ```sql
     SELECT u.id, u.username, COUNT(*) AS num_likes
     FROM users AS u
     JOIN likes AS l ON u.id = l.user_id
     GROUP BY u.id
     HAVING num_likes = (SELECT COUNT(*) FROM photos);
     ```
     Output -
     
     ![image](https://github.com/Shubham301099/Social-media-users-Analysis/assets/154081009/120b9374-f88b-489b-bbd9-f3e44ea3a08a)
   - **Conclusion:** 13 potential fake accounts identified.

## Results

This project, conducted using MySQL, uncovered essential MySQL concepts for solving complex problems. Data analysis through SQL queries provided insights into user engagement, aiding marketing, product, and development teams in making informed decisions.
