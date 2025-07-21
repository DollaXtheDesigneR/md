graph TD
    %% --- Styling ---
    classDef coreEngine fill:#cce5ff,stroke:#004085,stroke-width:2px,font-weight:bold
    classDef userAction fill:#e9ecef,stroke:#343a40,stroke-width:1px
    classDef decision fill:#fff3cd,stroke:#856404,stroke-width:1px
    classDef process fill:#d4edda,stroke:#155724,stroke-width:1px
    classDef feature fill:#f8d7da,stroke:#721c24,stroke-width:1px
    classDef admin fill:#d1ecf1,stroke:#0c5460,stroke-width:1px

    %% --- 1. Authentication & Role-Based Access ---
    subgraph "1. User Access & Roles"
        A[Start: User opens PDMMS] --> Login[Login Screen];
        Login --> Auth{Check Credentials & Role};
        Auth -- Success --> Dashboard[Main Dashboard];
        Auth -- Failure --> Login;
    end

    %% --- 2. Central Hub & Core Engines ---
    subgraph "Central Hub & Core Engines"
        Dashboard -- Displays --> D1[Low Stock Alerts];
        Dashboard -- Displays --> D2[Pending/Overdue Deliveries];
        Dashboard -- Displays --> D3[Key Analytics Widgets];
        
        InventoryEngine[📦 Inventory Tracking Engine]:::coreEngine;
        PriceEngine[🏷️ Price Memory Engine]:::coreEngine;
        SmartEngine[🧠 Smart Memory Engine]:::coreEngine;
        NotificationEngine[⏰ Notification Engine]:::coreEngine;
    end

    %% --- 3. Primary User Action: Log New Delivery ---
    subgraph "3. Product Delivery Memory (Logging)"
        style Log2 feature
        style Log3 feature
        Dashboard -- "Log New Delivery" --> Log1[Select Vendor];
        SmartEngine -.->|Suggests Vendor| Log1;
        Log1 --> Log2[Select Product];
        Log2 --> Log3["Enter: Quantity, Unit Price, Delivery Date"];
        PriceEngine -.->|Suggests Last Price| Log3;
        Log3 --> Log4{Attach Invoice?};
        class Log4 decision;
        Log4 -- Yes --> Log5[Upload Invoice/Receipt Image];
        class Log5 userAction;
        Log4 -- No --> Log6;
        Log5 --> Log6;
        Log6["Set Status: Delivered / Pending / Partial"]:::userAction;
        Log6 --> Log7[Save Delivery Record];
        class Log7 process;
        
        Log1 --> AltLog["OR Bulk Import / Scan"]:::feature;
        AltLog --> Log7;

        %% Data Flow from Logging
        Log7 -.->|Updates Stock Levels & Aging| InventoryEngine;
        Log7 -.->|Updates Price History| PriceEngine;
        Log7 -.-> Dashboard;
    end

    %% --- 4. Monitoring & Comparison ---
    subgraph "4. Inventory & Price Monitoring"
        style Inv_List feature
        Dashboard -- "View Inventory" --> View_Inv[Filter by Vendor/Product/Status];
        class View_Inv userAction;
        InventoryEngine -.->|Provides Data| View_Inv;
        View_Inv --> Inv_List["Display: Stock Levels, Stock Aging (FIFO/FEFO)"];
        
        Dashboard -- "Compare Prices" --> View_Price[Select Product];
        class View_Price userAction;
        PriceEngine -.->|Provides Data| View_Price;
        View_Price --> Price_Chart["Display: Price History & Vendor Comparison Chart"];
        Price_Chart -->|Identify Best Value| SmartEngine;
    end

    %% --- 5. Analytics & Reporting ---
    subgraph "5. Analytics & Reporting"
        Dashboard -- "View Reports" --> Reports[Select Report Type];
        class Reports userAction;
        Reports -- "Delivery Frequency" --> Gen_Report[Generate Report];
        Reports -- "Cost Analysis" --> Gen_Report;
        Reports -- "Vendor Performance" --> Gen_Report;
        Gen_Report --> Export{Export as PDF/CSV/Excel?};
        class Export decision;
        Export -- Yes --> Export_File[Download File];
        Export -- No --> Dashboard;
        Export_File --> Dashboard;
    end

    %% --- 6. Background Processes & Notifications ---
    subgraph "6. Background & Notification Engine"
        InventoryEngine -- "Stock < Threshold" --> NotificationEngine;
        Log7 -- "New Pending Delivery Logged" --> NotificationEngine;
        NotificationEngine --> Gen_Alert1[Generate Low Stock Alert];
        NotificationEngine --> Gen_Alert2[Track Pending Delivery Dates];
        Gen_Alert2 -- "Date > Expected" --> Gen_Alert3[Generate Overdue Delivery Alert];
        
        Gen_Alert1 --> D1;
        Gen_Alert3 --> D2;
    end
    
    %% --- 7. System Setup (Admin Only) ---
    subgraph "7. System Settings & Management"
        M_Setup[System Settings]:::admin;
        Dashboard -- "Settings" --> M_Setup;
        M_Setup --> M_Vendors[Manage Vendors];
        M_Setup --> M_Products[Manage Products & Units];
        M_Setup --> M_Users[Manage Users & Roles];
        M_Setup --> M_Alerts[Configure Alert Thresholds];
        M_Setup --> M_Backup["Data Backup & Restore / Offline Sync"];
        
        M_Vendors & M_Products & M_Users & M_Alerts & M_Backup --> Dashboard;
    end
