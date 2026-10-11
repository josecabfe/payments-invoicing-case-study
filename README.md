# How I optimized a payment process from 5 minutes to under 1

**Case study: a zero-cost web form that records each course payment once and updates the course sheet, the bank sheet and an invoice queue at the same time, for a non-technical sales and finance team.**

### [▶ Read the case study and try the demo](https://josecabfe.github.io/payments-invoicing-case-study/)

A consulting firm that also sells specialized training courses, mostly for lawyers, tracked every payment by hand: checking the bank, typing a note into each course spreadsheet, and keeping no list of invoices still to issue. Now one form does the matching in under a minute, and nothing gets forgotten.

---

## The problem

The firm has trained 5,000+ professionals in 190+ courses over 11 years. At that volume, tracking payments by hand doesn't scale.

- Each payment took 4–5 minutes of cross-checking the bank statement against several spreadsheets, and ended up as a free-text note in a cell.
- Prices vary: new participants pay full price and returning participants pay another, plus special promotions, personal discounts and group discounts on request. Every payment had to be checked against its own deal. That is a big part of why it was slow.
- Every course has its own spreadsheet, with 1 to 4 installments and slightly different layouts.
- Typos, transfers assigned twice or to the wrong person, and payments never invoiced because there was no pending list.

**Constraints from the owner:** change the routine as little as possible; everything must stay editable by hand; the person who invoices shouldn't see participant details; no new software costs.

## The solution

1. Record the payment: course, participant, installment, and the bank transfer from a list of unassigned ones.
2. The course sheet shows "Paid – invoice pending" (details kept as a cell note).
3. The bank sheet tags the transfer with course and participant, so it can't be reused.
4. A card is added to "Invoices to issue". Who to invoice (name or company, and tax ID) comes straight from the enrollment form, plus amount, 10% VAT and amount in words.
5. The invoice is written by hand in the pre-printed booklet, as before.
6. The invoice number is entered once and written to the course sheet and the bank sheet automatically.

> **Invoicing in Paraguay, in short:** every sale needs a legal invoice. This firm uses pre-printed invoice booklets authorized by the tax authority, and every invoice has its own number (e.g. `001-001-0000123`). Each invoice carries the tax ID (RUC) of whoever pays, the participant or sometimes their law firm, which they later use to file their own taxes.

## A deliberate choice: a simple core, editable edges

The two common prices, **new participant** (full price) and **returning participant**, are built in. Promotions, personal discounts and group deals change all the time, so instead of building a rule for each one, special cases go under an **"Other"** category with a comment the rest of the team can see, and every cell stays editable by hand. The system automates the everyday path (one payment, one transfer, one invoice) and the checks that stop costly mistakes, and keeps manual edits in sync across sheets.

The result is a system that is simple to use, simple to build and maintain, and fits naturally into the work the sales and finance team was already doing.

## Designed to meet people at their level

Pick from lists instead of typing · search by name or ID number, with or without accents · plain-language error messages that say what to do next · works on phone or computer · payments and invoicing each have their own screen.

## Mistakes it prevents

| Mistake | How |
|---|---|
| Same transfer used twice | Assigned transfers leave the list; the server checks again |
| Wrong amount | Can't exceed the bank transfer or the installment price |
| Payment never invoiced | Stays in the queue, sorted by date, until it has a number |
| Invoice to the wrong name or tax ID | Taken from the enrollment form, not retyped |
| Two people saving at once | Lock + warning if the installment changed meanwhile |
| Invoice number mistyped or reused | Format check; rejected if used for another participant |
| Rows inserted, sorted or deleted | Rows found by payment ID and ID number, not position |

## Testing

26/26 automated tests running the real code on temporary copies (never on the real spreadsheets). They found 2 real bugs before launch; two review rounds fixed ~10 more edge cases.

## Results (first 10 days of use)

| | |
|---|---|
| Time to record a payment | **under 1 min** (was 4–5 min) |
| Payments recorded through the form | **150+** |
| Daily users | 3 |
| Extra software cost | $0 (Google Workspace) |

## Tools

Google Apps Script (JavaScript) · Google Sheets · LockService · installable triggers · HTML/CSS/JS · clasp · git

---

*Real project at my current job. Our participants trust us with their personal and financial information, so no real names, ID numbers, amounts or screenshots of the real system are shown. All names, ID numbers and amounts in the demo are fictional, generated with AI. Numbers are rounded.*

*Another project for the same team: [How I rescued storm-damaged records and made them searchable in seconds](https://josecabfe.github.io/storm-proof-records/)*

*Built by José Cabral Ferraro · [LinkedIn](https://www.linkedin.com/in/jose-cabral-ferraro/)*
