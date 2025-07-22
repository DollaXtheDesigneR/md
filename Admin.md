graph TD
    subgraph "Admin Journey: Full System Control"
        %% Login
        Login[Login as Admin] --> Dashboard[🏠 Main Dashboard];

        %% Core Actions from Dashboard
        Dashboard --> Log[Log New Delivery];
        Dashboard --> Monitor[Monitor Stock & Prices];
        Dashboard --> Reports[Create Reports];
        Dashboard --> Settings[System Settings];

        %% Detailed Flows
        Log --> SaveDelivery[Save Delivery Record];
        Monitor --> ViewInventory[View Stock Levels];
        Monitor --> ComparePrices[Compare Vendor Prices];
        Reports --> DownloadReport[Download PDF/Excel];
        
        %% Admin-Specific Settings
        Settings --> ManageUsers[Manage Users & Roles];
        Settings --> ManageProducts[Manage Products & Vendors];
        Settings --> ConfigureSystem[Configure Alerts & Backups];
    end
