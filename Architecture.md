# TravNow Architecture

```mermaid
flowchart TB

  U[User] --> MLP[travnow.com Main Landing Page]
  MLP --> D1[travnow.com/asheville]
  MLP --> D2[travnow.com/st-augustine]
  MLP --> D3[travnow.com/myrtle-beach]

  %% -------------------------
  %% Tahir Front-End + CMS
  %% -------------------------
  subgraph Tahir_FE[Tahir Front-End and CMS]
    direction TB
    CMS[CMS Content]

    D1 --> CMS
    D2 --> CMS
    D3 --> CMS

    D1 --> FE1[Destination Page UI]
    D2 --> FE2[Destination Page UI]
    D3 --> FE3[Destination Page UI]
  end

  %% -------------------------
  %% Travcoding APIs
  %% -------------------------
  subgraph Travcoding_APIs[Travcoding APIs]
    direction TB
    SU[Sign Up]
    SI[Sign In]
    GW[Get Wallet]
  end

  FE1 --> Auth{Authenticated?}
  FE2 --> Auth
  FE3 --> Auth

  Auth -- No --> SU
  Auth -- No --> SI
  SU --> GW
  SI --> GW
  Auth -- Yes --> GW

  %% -------------------------
  %% Travcoding Widget
  %% -------------------------
  subgraph Widget[Travcoding Booking Widget]
    direction TB
    W[Widget Container]
    H[Hotels]
    R[Homes]
    A[Activities]

    W --> H
    W --> R
    W --> A
  end

  GW --> W
  FE1 --> W
  FE2 --> W
  FE3 --> W

  %% -------------------------
  %% Booking Outcome
  %% -------------------------
  W --> Outcome{Booking Completed?}

  %% -------------------------
  %% Funnels
  %% -------------------------
  subgraph Funnels[Email Funnels]
    direction TB
    F1[Booked Funnel]
    F2[Not Booked Funnel]
  end

  Outcome -- Yes --> F1
  Outcome -- No --> F2

  %% -------------------------
  %% Ops and Reporting
  %% -------------------------
  subgraph Ops[Ops and Reporting]
    direction TB
    BO[Travcoding Backoffice]
    GHL[GoHighLevel CRM]
    RT[Reporting Tools]
  end

  Outcome -- Yes --> BO
  Outcome -- Yes --> GHL
  Outcome -- Yes --> RT
  Outcome -- No --> GHL
