# Google Drive Folder Creation Automation (Weekly Progress Tracking)

## Overview
This Make.com automation intelligently creates a **monthly folder structure in Google Drive** with **5 pre-organized weekly subfolders**. It auto-calculates week ranges and triggers on a schedule to maintain consistent data organization for progress tracking.

---

## What It Does

### **Trigger**
- **Webhook Trigger** — Listens for HTTP POST requests
- Can be scheduled via third-party cron services (cron-job.org, Zapier, etc.)
- Runs once per month to create fresh folder structure

### **Automation Flow**

1. **Date Calculation Module (ID: 5)**
   - Extracts current Year (e.g., "2025")
   - Extracts Month Name (e.g., "Apr")
   - Calculates Month Start Date (e.g., "2025-04-01")
   - Calculates Month End Date (auto-adjusts for 28/30/31 days)

2. **Week Range Calculation Module (ID: 17)**
   - Automatically splits the month into **5 weeks**
   - Generates readable date ranges:
     - Week 1: "01 Apr - 06 Apr"
     - Week 2: "07 Apr - 13 Apr"
     - Week 3: "14 Apr - 20 Apr"
     - Week 4: "21 Apr - 27 Apr"
     - Week 5: "28 Apr - 30 Apr" (remaining days)

3. **Google Drive Integration**
   - Creates main **YEAR-MONTH folder** (e.g., "2025-Apr")
   - Creates **5 weekly subfolders** with auto-calculated date ranges
   - Stores all folders in your designated **Google Shared Drive**
   - Uses Team Drive access for secure, scalable organization

---

## Tech Stack

| Component | Purpose |
|-----------|---------|
| **Make.com** | Workflow orchestration & scheduling |
| **Google Drive API** | Folder creation in Team Drive |
| **Webhook Trigger** | External trigger (HTTP POST) |
| **Date Formatters** | Auto-calculate week ranges |

---

## Folder Structure Created

```
SOCIAL_CONTENT (Shared Drive)
│
└── 2025-Apr/
    ├── 01 Apr - 06 Apr  (Week 1)
    ├── 07 Apr - 13 Apr  (Week 2)
    ├── 14 Apr - 20 Apr  (Week 3)
    ├── 21 Apr - 27 Apr  (Week 4)
    └── 28 Apr - 30 Apr  (Week 5)
```

---

## Key Features

✅ **Fully Automated** — No manual folder creation needed  
✅ **Month Aware** — Automatically adjusts for 28/30/31 day months  
✅ **Week Aware** — Intelligently splits months into 5 weeks  
✅ **Date Labels** — Every folder shows clear date ranges  
✅ **Scalable** — Works with any Google Team Drive  
✅ **Repeatable** — Same logic every month  

---

## Use Cases

- **Weekly Content Tracking** — Organize social media content by week
- **Project Management** — Track deliverables by week each month
- **Data Segregation** — Keep monthly data isolated and organized
- **Progress Monitoring** — Quick visual overview of week-by-week progress
- **Team Collaboration** — Shared Drive access for team workflows

---

## How to Use This Automation

### **1. Import the Blueprint**
```
1. Go to Make.com
2. Create a new scenario or import existing one
3. Select "Import Blueprint" 
4. Upload: folder_creation_blueprint.json
5. Click "Save"
```

### **2. Configure Google Drive Connection**
```
1. In the Make scenario, locate Module 36 (Google Drive: Create A Folder)
2. Update the connection to your Google account
3. Update the Shared Drive ID:
   - Current: "0AMU9_ttXHQFWUk9PVA" (example)
   - Replace with YOUR Shared Drive ID
4. Update destination folder path if needed
```

### **3. Set Up a Trigger (Schedule)**

**Option A: Using Zapier**
```
Create a Zap → Schedule by Zapier
Trigger: 1st day of each month → POST to your Webhook URL
```

**Option B: Using cron-job.org**
```
1. Get your Webhook URL from Make scenario
2. Create cron job: 0 0 1 * * (1st of every month)
3. POST to webhook URL
```

**Option C: Manual Trigger**
```
Click "Run" in Make.com scenario manually
Or send POST request:
curl -X POST https://your-webhook-url
```

### **4. Verify Folder Creation**
- Check your Google Shared Drive
- You should see: `2025-Apr/` with 5 week subfolders
- Check folder names match the calculated week ranges

---

## Configuration Details

| Setting | Value | Notes |
|---------|-------|-------|
| **Trigger Type** | Webhook (HTTP POST) | Or schedule via external service |
| **Frequency** | Monthly (1st of month) | Configurable |
| **Destination** | Google Shared Drive | "SOCIAL_CONTENT" |
| **Parent Folder** | Root of Shared Drive | Customize as needed |
| **Date Format** | YYYY-MMM (e.g., 2025-Apr) | ISO-friendly |

---

## Results & Impact

- **Time Saved:** 5-10 mins/month per person × team size
- **Error Reduction:** Zero manual folder naming errors
- **Consistency:** Same structure every month automatically
- **Scalability:** Works for unlimited months/years

**Real-world example at Fluencium:**
- 50+ content pieces/week organized by date
- Clear visibility of weekly progress
- Team members know exactly where to upload their work
- Monthly archive is automatically organized

---

## Customization Options

### **Change Weekly Dates**
Modify the calculation in Module 17 if you want different week definitions:
```
Week1Start: addDays(5.Month start date; 0)  → Change 0 for different start
Week1End: addDays(5.Month start date; 6)    → Change 6 for different length
```

### **Change Folder Naming**
In Module 35 (array construction), update the naming convention:
```
Current: "{{17.Week1Start}} - {{17.Week1End}}"
Custom:  "Week 1 ({{17.Week1Start}})"
```

### **Change Shared Drive**
In Module 36, update the `sharedDrive` parameter to your drive ID:
```json
"sharedDrive": "YOUR_DRIVE_ID_HERE"
```

---

## Blueprint Details

| Module | Function |
|--------|----------|
| **5** | Extract Year, Month, Start/End dates |
| **17** | Calculate 5 week date ranges |
| **34** | Get parent folder from Shared Drive |
| **35** | Format week range labels into array |
| **36** | Create subfolders for each week |

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Folders not creating | Check Google connection & Shared Drive ID |
| Wrong dates in folder names | Verify Module 17 date calculations |
| Permission denied | Ensure Google account has access to Shared Drive |
| Webhook not triggering | Confirm HTTP POST is being sent to webhook URL |

---

## Screenshots

**Example: Monthly Folder Structure**
```
📁 2025-Apr
   📁 01 Apr - 06 Apr
   📁 07 Apr - 13 Apr
   📁 14 Apr - 20 Apr
   📁 21 Apr - 27 Apr
   📁 28 Apr - 30 Apr
```

---

## Status

✅ **Production** — Active at Fluencium for organizing weekly social content  
✅ **Tested** — Works across months with different lengths (28/30/31 days)  
✅ **Scalable** — Ready to adapt for multiple teams/Shared Drives  

---

## Time to Build
~2-3 hours (including Google Drive setup & webhook configuration)

---

## Questions?

This automation is reusable for any project that needs **monthly + weekly folder organization**. Customize the parent folder, folder naming, or trigger schedule based on your needs.

