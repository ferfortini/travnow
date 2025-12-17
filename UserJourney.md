# TravNow User Journey & Booking Flow

```mermaid
flowchart TB

  U[User] --> Home[travnow.com]
  Home --> Dest[Destination Landing Page]

  %% -------------------------
  %% Entry & Lead Capture
  %% -------------------------
  Dest --> Explore[Explore Deals CTA]
  Dest --> Lead[Lead Capture Form]

  %% -------------------------
  %% Authentication
  %% -------------------------
  Explore --> Auth{Logged in?}
  Auth -- No --> Signup[Sign Up]
  Auth -- No --> Signin[Sign In]
  Signup --> Wallet[Get Wallet]
  Signin --> Wallet
  Auth -- Yes --> Wallet

  %% -------------------------
  %% Widget & Products
  %% -------------------------
  Wallet --> Widget[Travcoding Booking Widget]

  Widget --> Product{Select Product}
  Product --> Hotels[Hotels]
  Product --> Homes[Homes]
  Product --> Activities[Activities]

  %% -------------------------
  %% Booking Flow
  %% -------------------------
  Hotels --> Checkout[Booking Flow]
  Homes --> Checkout
  Activities --> Checkout

  Checkout --> Outcome{Booking Completed?}

  %% -------------------------
  %% Funnels
  %% -------------------------
  Outcome -- Yes --> Booked[Booked Funnel Emails]
  Outcome -- No --> NotBooked[Not Booked Funnel Emails]

  %% -------------------------
  %% Ops & Reporting
  %% -------------------------
  Outcome -- Yes --> Backoffice[Travcoding Backoffice]
  Outcome -- Yes --> CRM[GoHighLevel CRM]
  Outcome -- Yes --> Reporting[Reporting Tools]
  Outcome -- No --> CRM
