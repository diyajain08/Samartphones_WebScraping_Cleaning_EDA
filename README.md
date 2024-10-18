# Smartphone Data Scraping, Cleaning, and EDA

This project was undertaken as part of my learning process to understand web scraping, data cleaning, and exploratory data analysis (EDA) of smartphone data. The data was collected from the website [Smartprix](https://www.smartprix.com/) using **Selenium**, then cleaned and analyzed to gain insights into the smartphone market.
<br>

## Project Structure

```
📂 Smartprix Smartphone Data Analysis
│
├── web_scraping
│                ├── conn.py                # Script to set up the connection with ChromeDriver
│                ├── smartprix.py           # Web scraping script using Selenium to extract smartphone data
│                ├── test.py                # Test script for verifying web scraping and other functionalities
│                ├── smartprix-phones.ipynb
│                ├── smartprix.html
├── data_cleaning_smartphones.ipynb   # Jupyter Notebook for cleaning the scraped data
├── eda_smartphones_data.ipynb        # Jupyter Notebook for Exploratory Data Analysis (EDA)
└── README.md              # Project overview and documentation
```

## Project Overview

### Web Scraping

The goal of this project was to scrape smartphone data from the website [Smartprix](https://www.smartprix.com/) using **Selenium**. I extracted information such as:

- Smartphone names
- Prices
- Ratings
- Specifications like RAM, storage, and battery capacity

This process was automated using a script (`smartprix.py`), which navigates the website and extracts the necessary data. The **ChromeDriver** was used to control the browser through Selenium.

<br>

### Data Cleaning

The scraped smartphone data required several cleaning steps to ensure that it was ready for analysis. The cleaning process was carried out in the `data_cleaning_smartphones.ipynb` notebook using **Pandas** and **Python**. Below is a detailed explanation of the steps I performed:

1. **Handling Missing Values**:
   - Some entries in the scraped dataset were incomplete, particularly for price or specifications. I used different strategies to handle missing data:
     - For critical columns like `Price` and `Name`, rows with missing values were dropped as these columns are essential for the analysis.
     - For other columns (such as `Ratings` or `Specifications`), I either filled the missing values with placeholder text (e.g., "Not Available") or left them as NaN values depending on the context.

2. **Removing Duplicates**:
   - Duplicate entries appeared in the dataset due to repeated scraping or multiple occurrences of the same smartphone model. I removed all duplicate rows using `drop_duplicates()`, ensuring that each smartphone is represented only once.

3. **Price Formatting**:
   - The `Price` column initially contained non-numeric characters like the rupee symbol (`₹`) and commas (e.g., "₹20,999"). I cleaned this column by:
     - Removing the `₹` symbol and any commas using regular expressions.
     - Converting the cleaned price string into numeric format (integers) so that the prices could be used in further analysis.
     - Dealing with smartphones where the price was missing or had erroneous data by either removing them or setting the price as NaN for consistency.

4. **Parsing and Cleaning Specifications**:
   - **RAM**: The RAM column had values like "4 GB RAM" or "8 GB RAM." I extracted the numerical value from the text and converted the RAM into an integer (e.g., 4, 8) for easier analysis.
   - **Storage**: Storage values were similarly formatted (e.g., "128 GB Storage"), and I cleaned them by extracting the numeric part, converting it into integers (e.g., 128, 256), and storing them in a new column for storage capacity.
   - **Battery**: The battery capacity (e.g., "5000 mAh Battery") was extracted from text, parsed as an integer (5000), and stored in a separate column for numeric analysis. This allowed for proper comparison of battery capacities across devices.

5. **Standardizing Column Names**:
   - I renamed several columns for better clarity and consistency:
     - `smartphone_name` became `Name`
     - `phone_price` became `Price`
     - `ram_spec` became `RAM`
     - `battery_spec` became `Battery`
     - `storage_spec` became `Storage`
     This made the dataset more readable and the columns easier to interpret during analysis.

6. **Creating New Columns**:
   - I created new columns based on parsed data from specifications:
     - **RAM (GB)**: Created a new column with the numerical value of RAM in GB for each smartphone.
     - **Storage (GB)**: A new column with the internal storage size in GB.
     - **Battery (mAh)**: Parsed the battery capacity from the text and stored the values in a separate column as numeric values.

7. **Dealing with Inconsistent or Outlier Data**:
   - During the cleaning process, I identified and handled outliers and incorrect data points:
     - Some smartphones had extremely high or low prices or specs that were clearly outliers (e.g., prices that were way too high or too low, battery sizes outside of typical ranges). These entries were either removed or flagged for further investigation.
     - I ensured that values like RAM, storage, and battery were within reasonable ranges for smartphones, and corrected or removed entries that seemed erroneous.

8. **Type Conversion**:
   - After cleaning the data, I ensured all relevant columns were converted into their correct data types:
     - **Price, RAM, Storage, and Battery** columns were converted to integers.
     - **Name** and other text columns were kept as strings for easy manipulation.

9. **Final Dataset Overview**:
   - The cleaned dataset was now ready for analysis. It contained standardized and consistent values for all important smartphone features (Name, Price, RAM, Storage, Battery, etc.). Each row represented one unique smartphone, and all columns were cleaned to ensure data quality.
   - The cleaned dataset was saved as a CSV file for easy access and further analysis in the exploratory data analysis (EDA) phase.
<br>

### Exploratory Data Analysis (EDA)

After cleaning the data, I performed exploratory data analysis (EDA) in the notebook `eda_smartphones_data.ipynb` to uncover insights and trends in the smartphone market. Here’s a breakdown of the major steps and insights from the EDA process:

1. **Price Distribution Analysis**:
   - I started by exploring the **distribution of smartphone prices**. This involved plotting a histogram to visualize the range of prices in the dataset.
   - Key Insights: Most smartphones fall within the mid-range price category, with fewer high-end and budget devices. This was important to identify the target segments of smartphone pricing.
   
2. **Brand-wise Price Comparison**:
   - Next, I compared prices across **different smartphone brands**. Using bar charts, I visualized the average price of smartphones for each brand.
   - Key Insights: Certain brands (e.g., Apple and Samsung) dominated the premium segment, while others (e.g., Xiaomi, Realme) offered more affordable devices. This comparison helped highlight how brands position themselves in the market.

3. **Top Smartphone Brands by Frequency**:
   - I also analyzed which **brands had the most entries** in the dataset. This analysis revealed the most frequently occurring brands, giving insights into which brands dominate the market.
   - Key Insights: Brands like Xiaomi, Realme, and Samsung were the most frequent, showing their strong presence in the competitive smartphone landscape.

4. **Correlation between Price and Specifications**:
   - One of the main focuses of the analysis was to **examine how smartphone specifications affect price**. I explored correlations between various specs (e.g., RAM, internal storage, battery capacity) and the price.
   - Key Insights:
     - **RAM**: Smartphones with higher RAM tend to be priced higher. I used scatter plots to show that there is a positive relationship between RAM and price.
     - **Storage**: Similarly, more internal storage leads to higher prices, as observed through another scatter plot and correlation analysis.
     - **Battery Capacity**: The relationship between battery capacity and price was less clear, indicating that battery size alone doesn’t significantly drive price increases.

5. **Customer Ratings vs Price**:
   - I also investigated whether **higher prices correlate with better customer ratings**. This involved creating scatter plots and boxplots to observe the distribution of ratings across price categories.
   - Key Insights: Higher-priced smartphones tend to receive better ratings, but there were a few exceptions where budget smartphones received excellent ratings as well, likely due to good value for money.

6. **Specifications Analysis**:
   - I conducted a **deep dive into smartphone specifications** like RAM, storage, and battery capacity to understand their distribution in the market.
   - Key Insights:
     - **RAM Distribution**: Most smartphones in the dataset had 4GB to 6GB of RAM, with premium smartphones offering up to 12GB.
     - **Storage Distribution**: The most common internal storage capacities were 64GB and 128GB, with a few high-end devices offering 256GB or more.
     - **Battery Capacity**: The majority of smartphones had battery capacities between 4000mAh and 5000mAh, indicating a focus on long battery life in modern smartphones.

7. **Brand vs Specifications**:
   - Finally, I compared **brands based on their specifications**. For instance, I analyzed which brands offer the most RAM or battery life.
   - Key Insights: Premium brands like Apple and Samsung focused more on high-end specs (e.g., more RAM and storage), while brands like Xiaomi and Realme offered competitive specs in lower price ranges.


### Visualization and Tools Used:

- **Histograms and Bar Charts**: Used to visualize price distributions and brand comparisons.
- **Scatter Plots**: Helpful in visualizing correlations between price and specifications such as RAM, storage, and battery capacity.
- **Box Plots**: Used to compare customer ratings across price categories.
- **Correlation Heatmaps**: Employed to show the strength of relationships between different numerical features like price, RAM, storage, and battery capacity.
<br>

## Learning Outcomes

This project allowed me to:

1. **Master Web Scraping**: I developed a strong understanding of how to use Selenium to scrape data from dynamic websites.
2. **Data Cleaning**: I honed my skills in cleaning and structuring messy, raw data using Python and Pandas.
3. **Perform EDA**: I learned how to visualize and explore a dataset to derive meaningful insights using Python’s data analysis libraries.
<br>

## Future Improvements

- **Additional Features**: Scraping more detailed smartphone information, such as camera specs and display quality, for a richer dataset.
- **Automation**: Automating the scraping process to collect updated smartphone data over time and observe trends in the market.
- **Advanced Visualizations**: Enhancing EDA with more complex visualizations and statistical analyses.
