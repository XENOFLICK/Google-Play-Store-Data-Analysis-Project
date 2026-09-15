# Google Play Store App Data & Sentiment Analysis

An end-to-end data analytics and natural language processing (NLP) project designed to clean, process, and analyze Google Play Store application data alongside raw user reviews. This case study uncovers the core drivers of app ratings, installation distributions, update lifecycles, and sentiment mechanics to deliver data-backed recommendations for app development pipelines.

---

##  Project Overview
This project processes a dynamic dataset tracking thousands of mobile applications across various categories. By leveraging exploratory data analysis (EDA), data cleaning, data profiling, and computational sentiment analysis, the project tracks metrics from foundational statistics to advanced multi-dataset relational structures.

---

##  Tools and Technologies
* **Language:** Python 3.13+
* **Libraries:**
  * **Data Manipulation:** `pandas`, `numpy`
  * **Data Visualization:** `matplotlib`, `seaborn`
  * **Natural Language Processing:** `textblob` (for polarity and semantic evaluation)

---

##  Requirements & System Configuration
To execute the processing pipelines step-by-step, make sure you have the following prerequisites installed:
```bash
pip install pandas numpy matplotlib seaborn textblob
```
* **Dataset Dependencies:**
  * `googleplaystore.csv`: Main metadata repository.
  * `googleplaystore_user_reviews.csv`: Raw text translations of user review feedback.

---

##  Project Architecture & Pipeline

### 1. Data Cleaning and Preprocessing
Before running analytical tiers, data structures were standardized:
* **Missing Value Imputation:** Handled missing structural fields by mapping numerical subsets (`Rating`) to medians and categorical attributes (`Type`, `Content Rating`) to mode strings.
* **Type Normalization:** Stripped semantic punctuation (`+`, `,`, `$`) to transform string objects into mathematical integers and floats.
* **Size Standardization:** Structured a generic text-cleaning parser to map string sizes (`M`, `K`) uniformly into Megabyte (MB) float metrics.
* **Deduplication:** Dropped repeating application instances to ensure zero structural skewness across the portfolio.
* **Temporal Formatting:** Standardized date formats to datetime objects for time-series computations.

### 2. Multi-Tier Analysis
* **Basic Level:** Checked general baseline statistics, unique categories, price models (free vs. paid app balances), top-installed apps, and category-binned size structures.
* **Medium Level:** Calculated Pearson correlations between popularity and ratings, generated visual boxplots of category metrics, mapped genre adopter bases, and checked app size vs. installation scale curves.
* **Advanced Level:** Computed binned data partitions, tracked chronological update velocities, and implemented an NLP review pipeline using `TextBlob` to separate review scores based on positive and negative semantic indicators.

---

##  Challenges Faced & Solutions

* **Structural String Noise in Numerical Fields:** Columns like `Installs` and `Price` contained trailing characters (`+`, `$`, `,`) preventing direct mathematical modeling. 
  * *Solution:* Regular expressions and string vector methods (`.str.replace`) were written into the cleaning script to handle data formatting efficiently.
* **Heterogeneous Size Metrics:** App sizes were recorded arbitrarily as combinations of Megabytes (`M`) and Kilobytes (`K`), making data aggregation impossible.
  * *Solution:* Built a custom normalization parser function (`clean_size`) that scaled all metrics to MB units by dividing `K` values by 1024.
* **Deprecation Warnings in Visualizations:** Newer versions of Seaborn threw color palette mapping warnings during boxplot rendering.
  * *Solution:* Refactored visual definitions by linking categorical axes to the `hue` parameter and setting `legend=False` to ensure clean, warning-free rendering outputs.
* **High-Cardinality Categorical Dimensions:** Granular app `Genres` created overly detailed outputs when evaluating installation bases.
  * *Solution:* Grouped parameters into a clean hierarchy by using high-level `Category` targets for broad segment insights and using subset slicing (`.head()`) for detailed genres.

---

##  Key Insights Uncovered

* **Weak Popularity-to-Sentiment Link:** The correlation between download counts and app ratings is exceptionally weak (~0.0324), proving that mass installation velocity does not guarantee user satisfaction.
* **The Installation 'Sweet Spot':** Apps with the highest installations (100M+ to 1B+) are tightly bound within the **10 MB to 40 MB size footprint**. Larger single file packages face significant installation drop-offs.
* **Demographic Stability:** The `Everyone` content rating is the most common archetype. It shows tight rating distributions around 4.1 to 4.5, making it a highly reliable and safe approach for target audiences.
* **Update Frequency Impacts App Longevity:** Successful applications show heavy clustering around recent modification dates. Regular maintenance updates prevent churn and directly keep consumer sentiment high.
* **Clear Semantic Differences in Feedback:** NLP tracking showed that high-rated apps (4.5+) score a strong positive polarity (~0.2024), with reviews highlighting speed and layout convenience. Low-rated apps (3.0 and below) dipped into negative polarity, with reviews focusing heavily on intrusive ads, frozen UI layouts, and broken updates.

---

##  Recommendations for Strategic Improvement

1. **Optimize the Deployment Footprint:** Keep app bundle payloads under **40 MB** for initial downloads. Use dynamic on-demand delivery frameworks for asset loading to lower entry barriers and reduce install friction.
2. **Prioritize the Freemium Model:** Deploy software under a free tier using in-app purchases or subscription upgrades. Free frameworks drive significantly higher review volumes and engagement loops than upfront paid strategies.
3. **Commit to a Quarterly Release Cadence:** Set up automated update schedules at least once a quarter. Addressing compatibility fixes, minor layout changes, and feature updates keeps your app competitive against top industry players.
4. **Build Proactive UI Feedback Loops:** Since reviews show that broken interfaces and intrusive pop-ups quickly ruin app ratings, run automated visual tests and UX reviews before pushing major version changes.
