# Invisible Influencers – Investigating YouTube’s Bot Phenomenon 

### Flow diagram explaining how the different notebooks are linked together
![Flow diagram explaining how the different notebooks are linked together](images/Flow_diagram_commented.png)

### Abstract

This project, titled *Invisible Influencers – Investigating YouTube’s Bot Phenomenon*, aims to explore the growing issue of bots on YouTube, specifically those spreading spam through repetitive comments across multiple videos. With over 136,000 channels and 73 million videos in the dataset, we analyze how bots influence engagement metrics such as views, likes, and comments. Our primary goal is to identify bots based on their commenting patterns, specifically targeting videos uploaded within similar timeframes. We aim to assess the impact of these bots on both the videos and channels they target, revealing trends in content type, and the engagement. 

### Research question
1. What types of videos are most frequently targeted by bots?
2. How do bots influence the engagement metrics (views, likes, comments) of videos and channels?
3. What patterns or trends emerge in bot activity based on video categories, keywords, or timing?
4. Can we reliably detect bots without accessing the nature of the comments ?
5. What is the threshold for distinguishing bot activity based on comment distribution, and how does this affect the identification process?

### Feasability

The main challenge with the YouNiverse dataset is managing its large size. To efficiently preprocess the data, the best approach we've found is using Polars, which processes the data in chunks and offers built-in functions that make the preprocessing faster and easier, compared to writing custom functions. Additionally, storing the preprocessed data in .parquet files helps reduce the dataset's size, making it more manageable for analysis. This not only speeds up data processing but also saves time when reading, writing, and transferring the data.
The second challenge in this project is detecting bots. It’s important to note that it's impossible to be absolutely certain that an account is a bot based on the available data. Instead, we can only identify behaviors that strongly suggest bot-like activity. As a result, we use the terms 'suspicious accounts' and 'bots' interchangeably throughout the analysis.

### Method
#### Preprocessing
To detect suspicious users, we use histograms to analyze the distributions of comments made per day and the number of different videos targeted by each user. Bots typically exhibit abnormal behavior, such as significantly higher activity compared to the average user. Using these histograms, we establish an initial threshold to filter out suspicious users.
We further analyze the distribution of comments made per video to identify anomalies. The average number of comments per video is approximately 1, with a standard deviation of about 3. However, some users post over a thousand comments on a single video. To account for such outliers, we define a threshold as the mean plus twice the standard deviation. This allows us to flag accounts with unusually high commenting activity as suspicious.
#### Results
The analysis of the suspicious_user_2018metadata.parquet dataset focused on understanding the activity patterns of suspicious users. Pie charts were used to examine the categorical distribution of bot-like activity, revealing the proportion of users engaged in certain types of behavior. To further understand the relationship between the number of videos a user commented on and their activity level, scatter plots were created. These plots helped identify correlations between the number of videos targeted and the average number of comments per video. Additionally, a gamma distribution was fitted to the data to model and assess the behavior of these suspicious users more accurately. Histograms and cumulative histograms were also employed to study the number of channels commented on by each user, providing a detailed distribution of user activity across the platform.

For the analysis of the video_commented_daily.parquet dataset, various techniques were used to examine bot behavior over time and across different metrics. Time series analysis, using line plots, was instrumental in identifying trends in bot activity, allowing us to visualize the fluctuations and peaks in engagement over the course of the data. Histograms helped represent the distribution of key metrics, such as the number of comments made per day, shedding light on typical and atypical comment patterns. Box plots were used to visualize the spread and detect outliers in the data, offering deeper insights into the variability and consistency of bot activity. Categorical analysis was performed to classify data into meaningful categories, unveiling patterns and relationships that might indicate bot-like behavior. Finally, 3D heatmaps were utilized to visualize interactions and correlations between various categories in the dataset, offering a multi-dimensional perspective on the data.

Together, these methods provided a solid groundwork for understanding how to work with the dataset and allowed us to gain confidence in the project, helping us better understand what was possible to achieve.

### Organization and timelines

- Enlarge the data by filtering ou less data (small changes to do after analysis done in P2). Preprocess yearly data for all years: Decide thresholds for initial filtering, clean data, and prepare it for temporal and other analyses.
Responsible: Muhammad, Matthieu (Due around December 3rd) 
- Analysis Pipeline
Set up and extend the data processing pipeline: Create a robust pipeline for handling larger datasets and scaling analyses.
Responsible: Aurelien, Samuel, Amaury (Due around December 5th)
- Code Quality and Usability
Clean and document code: Ensure the pipeline is well-documented and easy to use for both team members and external collaborators.
Responsible: Mathieu, Amaury
- Advanced Analysis and Insights
Explore advanced methods: Investigate approaches to reduce false positives (e.g., normal users being flagged as bots) and derive deeper insights from the data.
Responsible: Aurelien, Samuel, Mhuammad
- Final Presentation
Code the webpage for final milestone delivery: Collaboratively design and implement a webpage to present project outcomes in an interactive and visually appealing manner.
Responsible: All team members
