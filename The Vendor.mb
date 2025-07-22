graph TD
    subgraph "Vendor Partner Journey: Self-Service Portal"
        %% Login
        Login[Login as Vendor] --> Portal[🤝 Vendor Portal Dashboard];

        %% Core Actions from the Portal
        Portal --> MyDeliveries[View My Deliveries];
        Portal --> MyProducts[Manage My Products];
        Portal --> MyAnalytics[View My Performance];

        %% Detailed Flows
        
        %% Delivery Tracking Flow
        MyDeliveries --> DeliveryStatus{Filter: Pending / Delivered?};
        DeliveryStatus -- Pending --> ViewPending["View My Pending Deliveries"];
        ViewPending --> ActionUpload[Upload Invoice for a Delivery];
        DeliveryStatus -- Delivered --> ViewHistory[View My Delivery History];

        %% Product Management Flow
        MyProducts --> ViewMyList[View My Product List];
        ViewMyList --> SuggestUpdate[Suggest Price/Info Update];
        SuggestUpdate --> NotifyManager["--> Sends notification to Manager for approval"];

        %% Analytics Flow
        MyAnalytics --> ViewStats["View My Analytics<br>(e.g., total volume, on-time rate)"];
        
    end
