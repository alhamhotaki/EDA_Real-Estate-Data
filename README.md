# EDA_Real-Estate-Data

We provided an in-depth analysis of a dataset containing 5,000 residential properties with 16 features, including key attributes such as MLS, sold_price, bedrooms, bathrooms, lot_acres, taxes, and year_built. The main objectives are to understand the factors influencing property prices and prepare the data for predictive modeling by addressing data quality issues.

# Initial Data Observations:
* The data requires several type conversions, handling of missing values, and outlier detection.
* Categorical features like kitchen_features and floor_covering are complex and may need encoding.
  
# Data Validation
The validation process involved checking for logical consistency across various columns to ensure that the data made sense within its context. For instance:

* Year Built: Verified that there were no future dates or unrealistically old years.
* Bedrooms, Bathrooms, and Square Footage: Ensured that the number of rooms and home size were logically consistent.
* Lot Size: Verified that the lot sizes were realistic for residential properties.
* Taxes: Checked that tax values were reasonable, with special attention to any zero or negative values.
* Fireplaces: Ensured that the number of fireplaces was realistic and did not include negative numbers.
* HOA Fees: Ensured that fees were appropriate, with no negative values.
  
# Data Cleaning
Significant efforts were made to validate and clean data, including converting data types, addressing missing values through various imputation techniques, and ensuring logical consistency.

* Zipcodes: Initially stored as integers, zipcodes were converted to strings to prevent any incorrect numerical operations, ensuring that the geographic identifiers are treated as categorical data rather than numerical values.
* Year Built: Reformatted to date format, with unrealistic entries like zeros replaced with NaN (Not a Number) to allow for meaningful analysis and imputation.
* Fireplaces: The data for fireplaces, initially containing blanks, was cleaned by replacing these blanks with NaN and converting the data from strings to integers.
* HOA Fees: The HOA fees data, which included commas and the string 'None', was cleaned by removing commas, replacing 'None' with NaN, and converting the entries to numeric values for analysis.

# Handling Missing Values
Several techniques were employed to handle missing data:
* Group-Based Imputation:
  * Lot Acres: Missing values were imputed using the mean value within groups defined by similar properties based on Zipcode, Bedrooms, and Sold Price.
  * Year Built: Missing values were replaced using the median from similar properties, grouped by Zipcode and Sold Price.
  * Bathrooms: Missing values were estimated based on the number of Bedrooms and Garage size, using group-based imputation.
* K-Nearest Neighbors (KNN) Imputation:
  * HOA Fees: Missing values for HOA fees were imputed using KNN, which predicts missing values based on the similarity to other data points. Features like Sold Price,
  * Year Built, and Lot Acres were used as predictors.
* Simple Fill:
  * Fireplaces: Missing values were replaced with 0, indicating the absence of fireplaces.
  * Kitchen Features: Missing values were filled with 'No Features Listed' to ensure the completeness of the data for analysis.
* Complex Missing Data Handling:
  * Square Footage: A new composite feature was introduced, combining Bedrooms and Bathrooms to estimate missing square footage values, which were then imputed based on the average square footage of similar properties.

# Outlier Detection and Handling
Outliers were systematically identified and managed using several strategies to prevent them from skewing analysis results and affecting model performance:
* Log Transformation: Applied to variables like Sold Price and Lot Acres to reduce skewness caused by extreme outliers.
* Capping: Extreme outliers were capped at a reasonable maximum, often at the 99th percentile, to bring the values closer to the rest of the data distribution. This was applied to features like Square Footage and HOA Fees.
* Manual Review: In cases like Taxes, where outliers could indicate data entry errors (e.g., misplaced decimal points), a manual review was conducted to correct these errors.

# Correlation Analysis
* The correlation analysis focused on identifying strong predictors for property prices:
  * Square Footage showed a strong correlation (0.56) with Sold Price, indicating that larger homes typically have higher prices.
  * Taxes also had a strong correlation (0.55) with Sold Price, as higher taxes often reflect higher property values.
  * Fireplaces and Bathrooms showed moderate correlations, suggesting that these features also contribute to higher property prices.
* Handling Multicollinearity:
To address multicollinearity (high correlation between predictor variables), the analysis considered either removing one feature from highly correlated pairs or applying techniques like Principal Component Analysis (PCA) or regularization to simplify the model and reduce the risk of inflated variance.


# Geospatial Analysis
* Data Integration: The primary dataset was enriched by merging it with additional geographic data, mapping zip codes to city names, which allowed for more detailed geographic analysis.
* Interactive Map Creation: Using the Folium library, an interactive map was created to visualize property data centered on the average geographic coordinates of the dataset. This map included marker clustering to manage the display of numerous data points effectively.
* Marker Representation: Properties were represented by color-coded markers based on pricing tiers, with interactive popups providing detailed information for each location.
* Key Insights: The analysis identified top cities for luxury homes and observed geographic trends in property values, further visualized through complementary bar plots highlighting the top 10 cities by average sold price.


The document concludes with a presentation of these findings and suggests that the analysis can be used to guide predictive modeling efforts focused on the most influential factors like square footage, taxes, and geographic location.
Attachment 1: Presentation
Attachment 2: EDA.ipynb


