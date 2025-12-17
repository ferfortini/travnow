# TravNow Architecture

```mermaid
flowchart TB
  %% =========================
  %% TravNow Architecture
  %% =========================

  U[User] --> MLP[travnow.com Main Landing Page\n(Any technology)]
  MLP --> D1[travnow.com/asheville]
  MLP --> D2[travnow.com/st-augustine]
  MLP --> D3[travnow.com/myrtle-beach]

  %% -------------------------
  %% Tahir Front-End + CMS
  %% -------------------------
  subgraph Tahir_FE[Tahir Front-End + CMS Ownership]
    direction TB
    CMS[(CMS Content)]
    D1 --> CMS
    D2 --> CMS
    D3 --> CMS

    D1 --> FE1[Destination Page UI\n(Content + Sections + CTA)]
    D2 --> FE2[Destination Page UI\n(Content + Sections + CTA)]
    D3 --> FE3[Destination Page UI\n(Content + Sections + CTA)]
  end

  %% -------------------------
  %% Travcoding APIs
  %% -------------------------
  subgraph Travcoding_APIs[Travcoding APIs]
    direction TB
    SU[Sign Up / Create Account]
    SI[Sign In]
    GW[Get Wallet]
  end

  FE1 --> AuthDecision{Authenticated?}
  FE2 --> AuthDecision
  FE3 --> AuthDecision

  AuthDecision -- No --> SU
  AuthDecision -- No --> SI
  SU --> GW
  SI --> GW
  AuthDecision -- Yes --> GW

  %% -------------------------
  %% Travcoding Widget
  %% -------------------------
  subgraph Travcoding_Widget[Travcoding Booking Widget]
    direction TB
    W[Widget Container]
    H[Hotels\n(Existing suppliers)]
    R[Homes\n(Quintess)]
    A[Activities\n(Hotelbeds → Viator)]
    W --> H
    W --> R
    W --> A
  end

  GW --> W
  FE1 --> W
  FE2 --> W
  FE3 --> W

  W --> WalletUsage[Wallet-enabled booking flow]

  %% -------------------------
  %% Lead Capture + Funnels
  %% -------------------------
  subgraph Funnels[Lead Capture & Email Funnels]
    direction TB
    LC[Lead Capture Funnel]
    F1[Booked Funnel]
    F2[Not Booked Funnel]
  end

  FE1 --> LC
  FE2 --> LC
  FE3 --> LC

  WalletUsage --> BookingOutcome{Booking Completed?}
  BookingOutcome -- Yes --> F1
  BookingOutcome -- No --> F2

  %% -------------------------
  %% Backoffice + CRM + Reporting
  %% -------------------------
  subgraph OpsStack[Ops & Reporting]
    direction TB
    BO[(Travcoding Backoffice)]
    GHL[(GoHighLevel CRM)]
    RT[(Reporting Tools)]
  end

  BookingOutcome -- Yes --> BO
  BookingOutcome -- Yes --> GHL
  BookingOutcome -- Yes --> RT
  BookingOutcome -- No --> GHL

