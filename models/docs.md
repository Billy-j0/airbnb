{% docs dim_listings_cleansed %}
This dimension table contains **cleaned and standardized Airbnb listing data**.

### Purpose
`dim_listings_cleansed` serves as the **primary listing dimension** used across analytics, reporting, and downstream fact tables.  
All records in this table represent **valid, deduplicated Airbnb listings** after applying business rules and data quality checks.

### Grain
- **One row per Airbnb listing**

### Source
- Raw Airbnb listings dataset

### Data Quality Guarantees
- Each listing has a unique `listing_id`
- All listings are associated with a valid host
- Invalid or unsupported room types are excluded
- String fields are cleansed of empty values

### Common Use Cases
- Joining with fact tables such as reviews or bookings
- Analyzing listings by room type
- Host-level listing aggregation
{% enddocs %}

{% docs dim_listing_cleansed__minimum_nights %}
The **minimum number of nights** a guest must stay when booking a listing.

### Business Logic
- Represents host-defined booking constraints
- Values must be **positive integers**
- Zero or negative values are considered invalid

### Analytical Impact
This field is often used for:
- Filtering listings suitable for short-term stays
- Pricing and availability analysis
- Customer segmentation based on stay duration

### Example
- `1` → One-night stays allowed
- `7` → Weekly minimum stay required
{% enddocs %}

{% docs dim_hosts_cleansed %}
This dimension table contains **cleaned and validated Airbnb host information**.

### Purpose
`dim_hosts_cleansed` acts as the **host master table**, ensuring all listings reference a valid and standardized host record.

### Grain
- **One row per host**

### Source
- Raw Airbnb hosts dataset

### Data Quality Guarantees
- No duplicate host records
- Every host has a valid identifier
- Host names are mandatory
- Superhost flag is standardized

### Common Use Cases
- Host performance analysis
- Superhost vs non-superhost comparisons
- Joining with listings for host-level KPIs
{% enddocs %}

{% docs fct_reviews %}
This fact table stores **guest reviews for Airbnb listings**, enriched with sentiment classification.

### Purpose
`fct_reviews` enables analysis of **guest feedback trends**, sentiment distribution, and listing-level review performance.

### Grain
- **One row per review**

### Source
- Raw Airbnb reviews dataset
- Sentiment derived via text analysis

### Data Quality Guarantees
- Every review references a valid listing
- Reviewer names are always present
- Sentiment values are constrained to known categories

### Common Use Cases
- Sentiment analysis by listing or host
- Review volume tracking
- Quality monitoring across room types
{% enddocs %}
