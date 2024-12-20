# Invisible Influencers – Investigating YouTube’s Bot Phenomenon 

### Link to Datastory
https://amaulap2.github.io/Datastory/

### Abstract

This project, titled *Invisible Influencers – Investigating YouTube’s Bot Phenomenon*, aims to explore the growing issue of bots on YouTube, specifically those spreading spam through repetitive comments across multiple videos. With over 136,000 channels and 73 million videos in the dataset, we analyze how bots influence engagement metrics such as views, likes, and comments. Our primary goal is to identify bots based on their commenting patterns, specifically targeting videos uploaded within similar timeframes. We aim to assess the impact of these bots on both the videos and channels they target, revealing trends in content type, and the engagement. 

### Research question
1. Do Bots Target Specific Categories of Videos?
2. Do Bots Target Specific Channels?
3. How do bots engagement metrics evolve?
4. Can we reliably detect bots ?
5. Is there a correlation between the number of days of suspicious activity and the lifetime of an account?

### Feasability

The main challenge with the YouNiverse dataset is managing its large size. To efficiently preprocess the data, the best approach we've found is using Polars, which processes the data in chunks and offers built-in functions that make the preprocessing faster and easier, compared to writing custom functions. Additionally, storing the preprocessed data in .parquet files helps reduce the dataset's size, making it more manageable for analysis. This not only speeds up data processing but also saves time when reading, writing, and transferring the data.
The second challenge in this project is detecting bots. It’s important to note that it's impossible to be absolutely certain that an account is a bot based on the available data. Instead, we can only identify behaviors that strongly suggest bot-like activity. As a result, we use the terms 'suspicious accounts' and 'bots' interchangeably throughout the analysis.

### Method
#### Preprocessing
To detect suspicious users, we use histograms to analyze the distributions of comments made per day and the number of different videos targeted by each user. Bots typically exhibit abnormal behavior, such as significantly higher activity compared to the average user. Using these histograms, we establish an initial threshold to filter out suspicious users.
We further analyze the distribution of comments made per video to identify anomalies. The average number of comments per video is approximately 1, with a standard deviation of about 3. However, some users post over a thousand comments on a single video. To account for such outliers, we define a threshold as the mean plus twice the standard deviation. This allows us to flag accounts with unusually high commenting activity as suspicious.
#### Results
The analysis focused on identifying suspicious user behavior on YouTube, particularly bot activity, by applying filters based on commenting patterns. Various techniques, such as SVM-based classification, were employed to differentiate between normal users and bots. A notable overlap was observed between Type-1 and Type-2 bots, with 53.83% of Type-1 and 76.53% of Type-2 users being flagged by both filters. This overlap strengthened the evidence of bot presence. Type-1 bots, characterized by high comment volumes on a limited number of videos, were isolated using the SVM model, while Type-2 bots, which distributed their comments across a broader range of videos in a short period, were identified through their widespread commenting behavior.

To explore the relationship between bot activity and video categories, the analysis revealed that bots were more likely to target specific categories, with a significant concentration in the "Howto & Style" section. Further investigation into channel targeting suggested that bots often focused on individual channels, implying they were deployed to enhance engagement on specific content. The engagement metrics indicated that bot-driven videos exhibited a consistent rise in comments over time, with bots maintaining high levels of activity across years.

Network graph analysis provided additional insights, revealing clusters of interconnected channels targeted by bots. This finding suggested that many bot-driven interactions were concentrated within a few key clusters, indicating the operation of bot services across multiple channels, often linked by common suspicious users. The results underscore the growing impact of bots on YouTube’s engagement metrics and demonstrate the effectiveness of comment-based filtering techniques in detecting and understanding bot behavior.
#### Acknowledgements
We wanted to acknowledge a few websites that helped us create our report. The first one is [python graph gallery](https://python-graph-gallery.com/) that we leveraged to create a few of our plots. The second is [cosmograph](https://cosmograph.app/) that we used to build our graph visualization.

### Organization

- Preprocessing : Muhammad
- Analysis : Aurélien, Matthieu and Samuel
- Website : Amaury
- Code Quality : Samuel
