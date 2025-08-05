# Power-BI-Report-Asset-Delivery-Warranty-Insights

🚀 Power BI Report – Asset Delivery & Warranty Insights 📊
Excited to share my latest Power BI project focused on delivery performance tracking and IT asset management!

Using a combination of procurement and inventory data, I built an interactive report to monitor order fulfillment timelines, delivery status KPIs, and warranty tracking of IT devices.

📦 Dataset Overview:
The dataset was split across two key pages:

1. Order & Delivery Page
Contains fields like:

Order date, Delivery Estimated date, Delivered Date

Model, Model Category, Quantity, Country, Delivery Status

Purchase/Lease, POS HP Order, HP Portal, Bucket TO BE

2. In-Stock & Warranty Page
Includes:

Model Category, Asset Tag, Serial Number, Warranty Expiration

State, Substate, Stockroom, Vendor, Legal Owner

Acquisition method, Support Group, PO Number, Scheduled retirement

🔧 Key Calculated Columns & Measures:
✅ Order Delivery Page
Calculated Columns:

TimeTaken To Deliver

DAX
Copy
Edit
DATEDIFF('All Orders'[Estimated delivery date HP Portal], 'All Orders'[Delivered Date], DAY)
Tracks how many days it took to deliver from the estimated to the actual delivery date.

Delivery Month

DAX
Copy
Edit
FORMAT('All Orders'[Delivered Date], "MMM")
Helps aggregate deliveries by month for trend analysis.

Measures:

Average Delivery Time

DAX
Copy
Edit
AVERAGE('All Orders'[TimeTaken To Deliver])
Gives the mean delivery duration, useful for setting benchmarks.
Delayed Delivery %

DAX
Copy
Edit
VAR TotalOrders = COUNTROWS('All Orders')
VAR DelayedOrders = COUNTROWS(
    FILTER('All Orders',
    'All Orders'[Delivered Date] > 'All Orders'[Estimated delivery date HP Portal])
)
RETURN DIVIDE(DelayedOrders, TotalOrders, 0)
Calculates the percentage of late deliveries.

Is KPI Met

DAX
Copy
Edit
IF([Delayed Delivery %] <= 0.3, "Target Met", "Target Not Met")
Evaluates delivery performance against a 30% delay threshold.

🔐 In-Stock & Warranty Page
Calculated Columns:

Days war Expiry

DAX
Copy
Edit
DATEDIFF(TODAY(), 'Raw Data'[Warranty expiration], DAY)
Calculates days until or since warranty expires.

Is war expired (6m)

DAX
Copy
Edit
IF('Raw Data'[Days war Expiry] > 180, "No", "YES")
Flags assets with warranty expiring in < 6 months.
Insights Enabled:
📌 Identify devices delayed beyond expectations

📌 Track delivery performance by country, vendor, or category

📌 Forecast and manage warranty expiration risk

📌 Segment devices that need retirement or warranty extension
