1. Task 1 :- Data Cleaning Project (Week 2)
2. Dataset :- British Airways Feedback dataset

# Imported Libraries required for data cleaning process.

#  Load the Raw Dataset

1. The original dataset is stored in the raw dataset/ directory. In this section, the CSV file is loaded into a Pandas DataFrame for further analysis.

# Raw Dataset Inspection

Initial exploration of the dataset's dimensions, column names, data types, ,sample records, before performing any cleaning step.

# Missing Value Analysis 

# Missing value summary for further data cleaning process.

# Visualizing missing data using a heatmap (seaborn or missingno)

# Missing Value Handling 

1. Applying a different strategy for each missing value so that no valuable data will get deleted.

# Strategy for Wifi & Connectivity, Aircraft and Inflight Entertainment

1. The "Not Applicable" Strategy (For Wifi, Entertainment, Aircraft)

• Why: These range from 31% to 83% missing. Dropping them loses valuable signals, but filling them with average scores distorts the truth.
• The Fix: Treat the missingness as its own feature. Transform these numerical ratings into categorical bins, or fill the missing values with a designated score (like 0 if the scale is 1–5) and create a binary shadow column (wifi_was_missing = 1).

# Strategy for Route and Type of Traveller

2. The "Unknown" Category (For Route, Type Of Traveller, Date Flown)

• Why: These hover around 20% missing. You cannot predict someone's flight route or travel type based on their seat comfort score.
• The Fix: Fill categorical gaps with a clean string category like 'Unknown'.

# Strategy for  Cabin Staff Service, Seat Comfort, Seat Type

3. Minimal Imputation (For Cabin Staff Service, Seat Comfort, Seat Type)

• Why: These have under 4% missing data. The impact of a minor imputation error here is negligible.
• The Fix: Use a simple statistical fill. Use the mode (most frequent value) for the categorical Seat Type and the median or mode for the rating columns.

# Strategy for Ground Services, Date Flown and Food & Beverages

1. Food & Beverages (10.80% Missing) and Ground Service (22.23% Missing)

Because this column represents a numerical rating scale (e.g., 1 to 5 stars), a median imputation is the safest path.
• Why the Median? Ratings are discrete integers (1, 2, 3, 4, 5). The median preserves this format by picking the middle value of your data.

2. Date Flown (20.39% Missing)

Fill it with a text placeholder string like "Unknown_Date" to preserve the rows.

# Final Interpretation of missing values

1. By Applying suitable startegy for each missing values all missing data became 0 means now data is cleaned there are no missing values which is useful for further analysis.

# Duplicate Value Handling

1. Finding duplicate values in the dataset


# Step 1: Decide What Defines a "Duplicate" in Your Dataset

Before deleting rows, check what makes them duplicates.
• Option A: They are 100% identical across every single column.
• Action: Drop them immediately.

# Final Interpretation of duplicate value

1. Initially dataset has 3815 rows now duplicate values are deleted and it became 3812 rows.

2. By handling duplicate values with care all duplicated data became 0 and there are no duplicate values and data is cleaned.

# Rename columns to snake_case and correct data types.

# Renaming Columns to snake_case

# Detecting outliers using box plots and IQR method

# Final Outcome of outliers

1. When applying the 1.5 × IQR rule to the seat_comfort rating column, zero outliers were detected. Because the ratings are bounded on a strict 1-to-5 scale, the calculated lower fence (-1.0) and upper fence (7.0) extend completely outside the data's natural boundaries. As confirmed by the box plot, the whiskers stretch fully to the minimum rating of 1.0 and the maximum rating of 5.0 with no data points plotted as individual fliers beyond them.


# Encode categorical columns using label or one-hot encoding

# Final Interpretation : Categorical Column Encoding

• Target Feature Digitization: The categorical target column recommended was mapped from text variables ('yes', 'no') into binary structural flags (1, 0).
• One-Hot Encoding Applied: Nominal features (type_of_traveller and seat_type) were expanded into multiple distinct columns using pd.get_dummies().
• Multicollinearity Prevention: The drop_first=True argument was enforced to drop redundant baseline categorical columns, successfully avoiding the Dummy Variable Trap.


#  Export the cleaned dataset to a new CSV file
