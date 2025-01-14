
Below is a sample **Salesforce project** designed for a beginner-level Trailhead Playground, with optional advanced requirements for those who’d like to push their skills further. The project scenario is centered on a **major grocer** that wants to track inventory across several categories (e.g. Food, Beverage, Household). The project includes data modeling, process automation, and reporting/dashboard requirements.

---

## Project Overview

### Scenario

You’ve been hired as a Salesforce Administrator for **Galaxy Grocers**, a major grocery chain. Their leadership wants a CRM system to track **inventory across various product categories**—such as Food, Beverage, and Household Items—and manage re-order processes, all within Salesforce. You’ll build out a solution in your Trailhead Playground that shows how managers and staff can keep track of stock levels, get notified when items run low, and see dashboards showing daily performance metrics.

### Learning Objectives

1. **Familiarize yourself with Custom Objects** and Custom Fields.
2. **Practice setting up process automation** (Flows or Workflow Rules) for low inventory alerts.
3. **Create a Dashboard** to display key metrics such as total inventory by category and items approaching reorder thresholds.
4. **(Optional Advanced)** Add complexity with additional flows, custom approval processes, or integration-like scenarios.

---

## Step-by-Step Project Requirements

Below are the main (beginner-level) requirements, followed by **Optional Advanced** expansions you can implement if you want to challenge yourself.

### 1. Set Up the Data Model

1. **Create a Custom Object** named **Inventory** (or **Product Inventory**).
    
    - Plural Label: **Inventories**
    - Record Name: **Inventory Number** (Auto Number or Text)
2. **Add Custom Fields** on the **Inventory** object:
    
    - **Name** (Text) – The name of the product (e.g., “Organic Apples”).
    - **Category** (Picklist) – Possible values: Food, Beverage, Household, Other.
    - **Current Stock Level** (Number) – The quantity on hand.
    - **Reorder Threshold** (Number) – Minimum quantity before triggering a reorder or alert.
    - **Supplier** (Lookup to Account)** – So you can associate your inventory to the supplier (if you want to use the standard Account object for suppliers).
3. (Optional but recommended) **Create a Custom Object Tab** for **Inventory** so it’s easy to navigate in the Salesforce app.
    
4. **Relate Inventory to Your Grocery Locations** (optional design choice):
    
    - If you want to track multiple store locations, create a **Store** custom object.
    - **Add a Lookup** or **Master-Detail** relationship from **Inventory** to **Store** so each inventory record is tied to a specific store location.

**Data Model - Beginner Summary**:

- **Objects**: Inventory (custom), plus optional Store (custom).
- **Fields**: Name, Category, Current Stock Level, Reorder Threshold, Supplier.

**Optional Advanced**:

- Create a **Price** field to track cost or sale price.
- Create a **Date/Time** field to track expiration dates or next reorder date.
- Implement **Validation Rules** to ensure the Reorder Threshold is not greater than Current Stock Level, or that Expiry Dates can’t be in the past, etc.

---

### 2. Build Automation for Reorder Alerts

Once the data model is set, leadership wants managers to get notified whenever an item’s **Current Stock Level** goes below the **Reorder Threshold**.

#### A) Choice #1: Workflow Rule (Beginner)

1. **Create a Workflow Rule** on the Inventory object:
    
    - Criteria: When **Current Stock Level** < **Reorder Threshold**.
    - **Email Alert**: Notify the Inventory Manager or designated user.
2. **Activate** the workflow rule.
    

#### B) Choice #2: Flow (Beginner-Intermediate)

1. **Create a Record-Triggered Flow** on the Inventory object.
    - **Trigger**: When a record is created or updated.
    - **Condition**: `Current Stock Level < Reorder Threshold`.
    - **Action**: Send an Email Alert or Post to Chatter to notify the Inventory Manager.

**Optional Advanced**:

- Instead of just sending an email, **update a related object**. For example, automatically create a **Case** or **Task** for the Purchasing team to restock.
- **Add an Approval Process** if certain items require manager approval before placing a reorder.
- **Use Scheduled Paths in Flow** to check items nearing expiry date (e.g., 7 days before expiry) to alert staff to discount or remove soon-to-expire products.

---

### 3. Create Reports & Dashboards

Dashboards help management see overall performance and stock levels at a glance.

1. **Create Custom Report Types**
    
    - Base the Report Type on the **Inventory** object.
    - (Optional) Include **Store** if you created that object.
2. **Build Reports** in the **Inventory** folder:
    
    - **Low Stock Report**: Filter where `Current Stock Level < Reorder Threshold`.
    - **Inventory by Category**: Group by **Category** (Food, Beverage, etc.) to see total stock levels.
    - **Inventory by Supplier** (if you’re using the standard Account object for suppliers).
3. **Create a Dashboard**
    
    - Add components referencing the above reports.
    - Consider:
        - **Gauge** or **Metric** for total stock count.
        - **Donut Chart** showing category breakdown.
        - **Table** listing top low-stock items.
4. **Set Dashboard Filters** (optional):
    
    - E.g., Filter by **Store** location or by **Supplier**.

**Optional Advanced**:

- **Dynamic Dashboards**: Show data relevant to the user who’s logged in (e.g., store manager only sees their location).
- **Lightning App Page**: Embed a dashboard or charts on a custom Lightning page for the Inventory object.
- **Schedule Dashboard Refresh**: Have the dashboard email out a snapshot daily/weekly to managers.
- **Importing pre-existing data to use in your app**: Grab relevant information from an existing dataset and import it into your Salesforce app. Example: [Download the Grocery Store Dataset from here](https://www.kaggle.com/datasets/bhavikjikadara/grocery-store-dataset). Then, modify the data to only include fields that map to your Salesforce object fields. Then, use the Data Import wizard or Data Loader to import the records. 

---

### 4. Testing and Deployment

In your **Trailhead Playground**:

1. **Add Sample Data**:
    
    - Create ~5 Inventory records covering different categories, e.g., Food items like apples, Beverage items like soda, Household items like cleaning supplies, etc.
    - Enter realistic `Current Stock Level` and `Reorder Threshold` values depending on the product. Example: a reorder threshold of 100 would make sense for apples, but not for an [outdoor Weber grill](https://www.kingsoopers.com/p/weber-genesis-s-335-outdoor-stainless-steel-3-burner-natural-gas-grill-silver/0007792417465?fulfillment=PICKUP).
2. **Trigger the Automation**:
    
    - Manually lower an item’s `Current Stock Level` below the threshold.
    - Verify an email or Flow notification is sent to the designated user.
3. **Check Your Reports and Dashboards**:
    
    - Ensure that items display accurately (e.g., the Low Stock Report shows the correct items).
4. **Documentation**:
    
    - Write a short description or doc explaining how your **Inventory** object is set up, how the automation works, and the purpose of each dashboard component.

---

## Putting It All Together

When completed, you should have:

1. A **Custom Inventory** object (and optionally a **Store** object).
2. **Custom Fields** for Category, Stock Level, Threshold, and more.
3. **Automation** (Workflow Rule or Flow) that triggers reorder alerts or tasks.
4. **Reports** that summarize inventory status by category and identify low stock.
5. A **Dashboard** that provides a real-time overview of grocery inventory.

If you choose to do the **Optional Advanced** pieces, you’ll gain additional experience with Flows, approval processes, and advanced reporting or dashboard scenarios.

---

## Next Steps & Extensions

- **Integration**: If you want a more complex project, pretend to integrate with a shipping or warehouse management system by simulating updates via inbound changes in a Flow or using an external data source (in a real-life scenario).
- **Enhance Security**: Configure permission sets or sharing rules so only certain roles can see or update certain fields (e.g., cost data is hidden from employees).
- **Trailhead Modules**: Look for modules on **Process Automation**, **Reports & Dashboards**, and **Data Modeling** to further cement your knowledge.

---

### Project Recap

- **Difficulty**: Beginner-friendly with straightforward data modeling, but can be made more challenging with advanced automation and reporting features.
- **Scenario**: Major grocer needing to track inventory, alert staff to low or expiring items, and visualize data in dashboards.
- **Key Deliverables**:
    1. Custom Inventory object + fields
    2. Automation (Workflow/Flow) for low inventory
    3. Dashboard & Reports for real-time insights

With this **Inventory Management**-focused project, you’ll practice critical Salesforce Admin skills—designing a data model, building automations, and surfacing analytics. Enjoy exploring these features in your Trailhead Playground!