graph TD
    subgraph "Manager Journey: Operations & Analytics"
        %% Login
        Login[Login as Manager] --> Dashboard[🏠 Main Dashboard];

        %% Manager's Accessible Actions
        Dashboard --> Log[Log New Delivery];
        Dashboard --> Monitor[Monitor Stock & Prices];
        Dashboard --> Reports[Create Financial Reports];
        Dashboard --> LimitedSettings[Manage Operations];

        %% Detailed Flows for the Manager
        Log --> SaveDelivery[Save Delivery Record];
        Monitor --> ViewInventory[View Stock Levels];
        Monitor --> ComparePrices[Compare Vendor Prices];
        Reports --> DownloadReport[Download PDF/Excel];
        
        %% Manager-Specific Settings (No User Management)
        LimitedSettings --> ManageProducts[Manage Products];
        LimitedSettings --> ManageVendors[Manage Vendors];
    end
