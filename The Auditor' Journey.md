graph TD
    subgraph "Auditor / Finance Journey: View-Only Financial Oversight"
        %% Login
        Login[Login as Auditor/Finance] --> Dashboard[📈 Financial Audit Dashboard];

        %% Core Actions from the Dashboard
        Dashboard --> Verify[Verify Delivery Records];
        Dashboard --> Audit[Audit Vendor Spending];
        Dashboard --> ExportData[Export Data for Accounting];
        
        %% Detailed Flows

        %% Verification Flow
        Verify --> Search["Search by Invoice #, Date, or Vendor"];
        Search --> ViewRecord["View Delivery Record & Attached Invoice (Read-Only)"];
        
        %% Audit Flow
        Audit --> GenReport[Generate Cost & Spending Reports];
        GenReport --> ViewReport["View Detailed Analytics (Read-Only)"];
        
        %% Data Export Flow
        ExportData --> ChooseFormat["Choose Format (e.g., CSV for Excel)"];
        ChooseFormat --> Download[Download Financial Data];
    end
