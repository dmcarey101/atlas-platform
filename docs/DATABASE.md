# Atlas Database Design

## Objective

Define the core data model required to support Atlas MVP workflows:

- Find representation
- Evaluate representation
- Monitor competitors
- Monitor issues
- Market intelligence
- Vendor discovery

---

## Core Entities

### 1. Company

A company, trade association, nonprofit, public entity, or other organization that hires lobbying representation.

Fields:
- id
- legal_name
- normalized_name
- parent_company_id
- industry
- website
- created_at
- updated_at

---

### 2. Lobbying Firm

A firm or organization that employs or contracts lobbyists.

Fields:
- id
- firm_name
- normalized_name
- website
- headquarters_state
- created_at
- updated_at

---

### 3. Lobbyist

An individual registered to lobby in one or more states.
Fields:
- id
- first_name
- last_name
- full_name
- current_firm_id
- email
- phone
- created_at
- updated_at

---

### 4. State

A U.S. state or jurisdiction.

Fields:
- id
- name
- abbreviation
- lobbying_source_url
- data_access_method
- difficulty_score

---

### 5. Registration

A public lobbying registration connecting a lobbyist, firm, company, and state.

Fields:
- id
- state_id
- company_id
- lobbying_firm_id
- lobbyist_id
- registration_status
- registration_date
- termination_date
- issue_area
- source_url
- source_document_id
- created_at
- updated_at

---

### 6. Compensation

Reported or estimated lobbying spend tied to a registration, company, firm, lobbyist, or reporting period.

Fields:
- id
- registration_id
- company_id
- lobbying_firm_id
- lobbyist_id
- state_id
- amount_exact
- amount_low
- amount_high
- estimate_method
- reporting_period_start
- reporting_period_end
- source_url
- confidence_score
- created_at
- updated_at

---

### 7. Watchlist

A user-created list of companies, firms, lobbyists, states, or issue areas to monitor.

Fields:
- id
- user_id
- name
- description
- created_at
- updated_at

---

### 8. Watchlist Item

An item being monitored inside a watchlist.

Fields:
- id
- watchlist_id
- entity_type
- entity_id
- created_at

---

### 9. Alert

A detected change relevant to a user’s watchlist.

Fields:
- id
- user_id
- watchlist_id
- alert_type
- title
- description
- related_entity_type
- related_entity_id
- state_id
- detected_at
- read_at

---

## Key Relationships

Company has many Registrations.

Lobbying Firm has many Lobbyists.

Lobbying Firm has many Registrations.

Lobbyist has many Registrations.

State has many Registrations.

Registration may have many Compensation records.

Watchlist has many Watchlist Items.

Watchlist generates many Alerts.

---

## MVP Design Principle

The database should preserve raw public records while also creating normalized entities.

This means Atlas should eventually store both:

1. Raw source data exactly as collected.
2. Normalized data used for search, alerts, and analytics.

---

## Future Entities

Not required for MVP, but likely needed later:

- Source Filing
- Source Document
- Issue Area Taxonomy
- Industry Classification
- Legislative Bill
- State Agency
- Committee
- User Organization
- Subscription Plan
- Export History
