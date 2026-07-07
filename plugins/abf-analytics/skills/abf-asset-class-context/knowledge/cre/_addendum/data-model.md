---
title: CRE — Addendum Data Model
main: cre
sub: _addendum
entities:
  - name: Project
    field_count: 31
  - name: Milestone
    field_count: 8
  - name: Realized Cash Flow
    field_count: 9
  - name: Expected Cash Flow
    field_count: 7
---

# CRE — Addendum Data Model

> Project lifecycle and cash-flow tracking supplement for CRE transactions.

## Project & Milestones

### `Project`

| Field | Type | Description |
|-------|------|-------------|
| Property Id | string | Unique identifier for the CRE property associated with this project. |
| Project Name | string | Name of the construction or development project. |
| Sponsor | string | Primary sponsor responsible for organising, capitalising, and managing the CR… |
| Contractor Name | string | General contractor or construction manager responsible for overseeing and exe… |
| Project Start Date | date | Official date when construction activities commenced on site, as documented i… |
| Exp Completion Date Original | date | Original expected completion date as specified in the initial construction sc… |
| Exp Completion Date Current | date | Current expected completion date as of the reporting date, reflecting any app… |
| Completion Date | date | Date when final completion was achieved, encompassing all construction activi… |
| Hard Cost Original | amount | Original approved construction budget for hard costs (materials, labour, equi… |
| Hard Cost Current | amount | Current approved construction budget for hard costs as of the reporting date,… |
| Hard Cost Paid | amount | Cumulative hard costs paid as of the reporting date. |
| Hard Costs Requested | amount | Portion of the current draw request specifically for construction hard costs … |
| Hard Costs Recommended | amount | Portion of hard costs in the current draw approved or recommended by the owne… |
| Soft Cost Original | amount | Original approved budget for soft costs (permits, architecture, engineering, … |
| Soft Cost Current | amount | Current approved budget for soft costs as of the reporting date, reflecting a… |
| Soft Cost Paid | amount | Cumulative soft costs paid as of the reporting date. |
| Land Cost Original | amount | Original approved budget for land acquisition costs, including purchase price… |
| Land Cost Current | amount | Current approved budget for land acquisition costs as of the reporting date. |
| Land Cost Paid | amount | Cumulative land acquisition costs paid as of the reporting date. |
| Total Cost Original | amount | Original approved total project budget, including hard costs, soft costs, lan… |
| Total Cost Current | amount | Current approved total project budget as of the reporting date, reflecting al… |
| Total Cost Paid | amount | Cumulative total project costs paid as of the reporting date. |
| Current Period Change Order Value | amount | Value of change orders approved during the current reporting period (extra wo… |
| Pending Change Order Value | amount | Value of change orders submitted but not yet approved as of the reporting date. |
| Potential Change Order Value | amount | Estimated cost of additional scope changes that may be requested in the futur… |
| Cumulative Change Order Value | amount | Total value of all approved change orders from project inception to the repor… |
| Project Pct Complete | percentage | Percentage of construction work physically completed as of the reporting date… |
| Milestones Met | boolean | Flag indicating whether all key milestones scheduled for the current reportin… |
| Total Draw Amount | amount | Total draw amount requested in the current reporting period, including hard c… |
| Construction Contract Pct Funded | percentage | Cumulative percentage of the total construction contract amount that has been… |
| Retention Withheld | amount | Amount temporarily withheld from the contractor (typically 5–10% of each draw… |

### `Milestone`

| Field | Type | Description |
|-------|------|-------------|
| Project Name | string | Name of the construction or development project to which this milestone belongs. |
| Milestone Name | string | Descriptive name of the construction milestone (e.g. Foundation Complete, Roo… |
| Exp Date Original | date | Expected milestone completion date as of project commencement, prior to any s… |
| Exp Date Current | date | Current expected milestone completion date as of the reporting date, reflecti… |
| Days Behind Schedule | integer | Number of calendar days the milestone is behind the planned schedule as of th… |
| Completion Date | date | Date on which the milestone was officially completed and all associated accep… |
| Description | string | Description of the deliverables, acceptance criteria, and requirements that m… |
| Nr Revisions | integer | Number of times this milestone's scheduled date or scope has been revised sin… |

## Cash Flows

### `Realized Cash Flow`

| Field | Type | Description |
|-------|------|-------------|
| Cf Id | string | Unique identifier for the cash flow event within the originator's database. |
| Property Id | string | Unique identifier for the CRE property associated with this cash flow record. |
| Rent Id | string | Unique identifier for the rent or lease agreement associated with this cash f… |
| Cf Reference Date | date | Date on which the cash flow was received from the lessee or tenant. |
| Type | list | Type of cash flow as per the defined list of values. |
| Effective Amount | amount | Actual cash amount received from the lessee or tenant on the reference date. |
| Cf Details | string | Additional notes or description relating to the cash flow event. |
| Recovery Source | string | Source of any recovered amounts (e.g. guarantor call, insurance, lien sale, s… |
| Currency Iso | string | ISO 4217 three-letter currency code for the cash flow (e.g. EUR, USD, GBP). |

### `Expected Cash Flow`

| Field | Type | Description |
|-------|------|-------------|
| Cf Id | string | Unique identifier for the expected cash flow event within the originator's da… |
| Property Id | string | Unique identifier for the CRE property associated with this expected cash flo… |
| Rent Id | string | Unique identifier for the rent or lease agreement associated with this expect… |
| Cf Reference Date | date | Date on which the lessee or tenant is expected to make the payment. |
| Type | list | Type of expected cash flow as per the defined list of values. |
| Expected Amount | amount | Amount expected to be received from the lessee or tenant on the scheduled due… |
| Currency Iso | string | ISO 4217 three-letter currency code for the expected cash flow (e.g. EUR, USD… |
