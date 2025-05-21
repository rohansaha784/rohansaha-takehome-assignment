# Rohan Saha – Take-Home DAML Assignment

This repository contains my solutions to the three coding questions in the take‑home. Everything compiles on **DAML SDK 2.10.0** and all provided tests pass.

---

## 📁 Project Structure
```
rohansaha-takehome-assignment
│
├─ daml/
│   ├─ Loan/                       # Q1: basic loan approval
│   │   ├─ Approval.daml
│   │   └─ Test.daml
│   │
│   └─ LoanExtended/               # Q2 + Q3
│       ├─ ApprovalWithLimit.daml  # token & loan‑limit logic
│       ├─ Repayment.daml          # repayment‑policy template
│       ├─ TestWithLimit.daml      # Q2 tests
│       └─ TestRepayment.daml      # Q3 tests
│
├─ daml.yaml                       # project config
└─ README.md                       # this file
```

---

## 🛠️ Build & Test
```bash
# build
daml build

# Q1 + Q2 tests
daml test

# Q3 repayment test
daml test --files daml/LoanExtended/TestRepayment.daml
```
Expected (all **ok**):
```
test_LoanWorkflow               ok
test_DoubleApproveFails         ok
test_LoanWithLimitWorkflow      ok
test_RepaymentFlow              ok
```

---

## 🌟 Design Highlights
| Task | Key Points |
|------|------------|
| **Q1 – Loan approval** | `LoanRequest → Approve → Loan`; straightforward archive‑and‑create. |
| **Q2 – Token & LoanLimit** | `LoanLimit` tracks `utilizedAmt`; approval increments, full repayment decrements. `Disburse` gives `Token` and recreates the `Loan` with updated `disbursed`. |
| **Q3 – Repayment** | Bank posts `RepaymentRestriction`; `Repay` (bank‑controlled) checks min amount, handles partial vs. full payoff, and adjusts `LoanLimit` when closed. |
