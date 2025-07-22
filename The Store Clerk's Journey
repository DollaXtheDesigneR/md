graph TD
    subgraph "Store Clerk Journey: Daily Tasks Only"
        %% Login
        Login[Login as Store Clerk] --> Dashboard[🏠 Main Dashboard (View Alerts)];

        %% Clerk's Limited Actions
        Dashboard --> Log[Log a New Delivery];
        Dashboard --> View[Check Stock Levels];

        %% Detailed Flow for the Clerk
        Log --> EnterDetails["Enter Product, Quantity, etc."];
        EnterDetails --> SaveDelivery[Save Delivery Record];
        
        View --> ShowInventory[Show Current Stock];
    end
