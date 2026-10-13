# Restful Booker - Manual API Testing Project (Postman)

A complete, beginner-friendly **manual API testing project** for the public [Restful Booker](https://restful-booker.herokuapp.com) practice API. It contains a Postman collection of **129 documented test cases in 19 learning chapters**, a ready-to-use environment, a test-scenario inventory and a reusable execution-report template.

Everything is designed to be done **by hand first**: no Postman scripts, no automatic assertions, no automatic variable extraction. The same test cases are the foundation for a later **Python `requests` + `pytest`** automation project.

## Contents

1. [Project overview](#1-project-overview)
2. [Objectives](#2-objectives)
3. [Prerequisites](#3-prerequisites)
4. [API under test](#4-api-under-test)
5. [Repository structure](#5-repository-structure)
6. [Import into Postman](#6-import-into-postman)
7. [Environment setup](#7-environment-setup)
8. [How the collection is organised](#8-how-the-collection-is-organised)
9. [Recommended execution order](#9-recommended-execution-order)
10. [Manual chaining: saving the booking ID and token](#10-manual-chaining-saving-the-booking-id-and-token)
11. [Running the CRUD workflow](#11-running-the-crud-workflow)
12. [Running the end-to-end flow](#12-running-the-end-to-end-flow)
13. [Recording actual results](#13-recording-actual-results)
14. [Troubleshooting](#14-troubleshooting)
15. [Limitations of the public shared API](#15-limitations-of-the-public-shared-api)
16. [Documentation review notes](#16-documentation-review-notes)
17. [How this project was verified](#17-how-this-project-was-verified)
18. [Publishing on GitHub](#18-publishing-on-github)
19. [Future scope: Python requests + pytest](#19-future-scope-python-requests--pytest)
20. [Credits and disclaimer](#20-credits-and-disclaimer)

---

## 1. Project overview

| Item | Details |
|---|---|
| System under test | Restful Booker, a public hotel-booking practice API |
| Test type | Manual functional API testing (positive, negative, boundary, business, contract, workflow) |
| Tool | Postman (collections, environments, Params/Authorization/Headers/Body tabs, Console) |
| Test cases | 129, each a Postman request with a full test-case description |
| Deliverables | Postman collection, Postman environment, test scenarios, execution report template, this README |
| Automation | None by design (manual learning phase). See [Future scope](#19-future-scope-python-requests--pytest) |

**What makes it useful as a portfolio project:** every expected result is traced to the official documentation, or explicitly marked *Investigate* when the documentation is silent. Many tests are designed to surface real documentation-vs-behaviour gaps (the API is deliberately buggy), so your execution report can show genuine findings.

## 2. Objectives

- Understand API fundamentals: client-server communication, base URL, endpoints, resources, request and response anatomy.
- Use HTTP methods correctly and explain the difference between full (PUT) and partial (PATCH) updates.
- Read and reason about status codes, headers, content types, query and path parameters, and JSON bodies.
- Practise authentication (token) and authorization (token vs Basic Auth), including negative cases.
- Validate API contracts and business rules **manually** with a checklist.
- Design test cases with equivalence partitioning, boundary value analysis, decision tables and state transitions.
- Chain requests manually (booking ID and token), and run a CRUD workflow and an end-to-end flow.
- Record actual results, distinguish *documented* from *observed* behaviour, and write defect reports.

## 3. Prerequisites

- **Postman desktop app** (instructions use current Postman terminology, with notes for older versions). The web version also works, but its browser agent may block a manually set `Cookie` header (see [Troubleshooting](#14-troubleshooting)).
- Network access to `https://restful-booker.herokuapp.com`. Some corporate networks block `herokuapp.com`.
- **Git** and a **GitHub** account (only for publishing).
- No programming knowledge is needed. Basic familiarity with JSON helps.

> Install tools only from their official sources. On a work computer, follow your organisation's software-approval and security policies (and raise a request if a tool isn't approved) before installing anything.

## 4. API under test

| Item | Value |
|---|---|
| Base URL | `https://restful-booker.herokuapp.com` |
| Official documentation | https://restful-booker.herokuapp.com/apidoc/index.html |
| Home page | https://restful-booker.herokuapp.com (states that it comes pre-loaded with 10 records, **resets every 10 minutes** and is **deliberately loaded with bugs**). It's public, so other people use it at the same time. |
| Source code | https://github.com/mwinteringham/restful-booker |
| Demo credentials | `admin` / `password123` (published in the official documentation; not a secret) |

### Endpoints (all verified against the official documentation)

| Method | Endpoint | Documented name | Credentials | Documented success |
|---|---|---|---|---|
| GET | `/ping` | HealthCheck | - | `201 Created` |
| POST | `/auth` | CreateToken | body: username and password | `200 OK` + `{"token": "..."}` |
| GET | `/booking` | GetBookingIds | - | `200 OK` + `[{"bookingid": n}]` |
| GET | `/booking/{id}` | GetBooking | - | `200 OK` + booking |
| POST | `/booking` | CreateBooking | - | `200 OK` + `{"bookingid": n, "booking": {...}}` |
| PUT | `/booking/{id}` | UpdateBooking | `Cookie: token=<token>` **or** `Authorization: Basic ...` | `200 OK` + booking |
| PATCH | `/booking/{id}` | PartialUpdateBooking | `Cookie: token=<token>` **or** `Authorization: Basic ...` | `200 OK` + booking |
| DELETE | `/booking/{id}` | DeleteBooking | `Cookie: token=<token>` **or** `Authorization: Basic ...` | `201 Created` |

- **Query parameters** (`GET /booking`, all optional): `firstname`, `lastname`, `checkin`, `checkout`. Dates use CCYY-MM-DD, and the date filters are documented as *greater than or equal to*. `bookingid` is **not** a documented query parameter.
- **Booking fields:** `firstname` (String), `lastname` (String), `totalprice` (Number), `depositpaid` (Boolean), `bookingdates.checkin` / `bookingdates.checkout` (Date), `additionalneeds` (String). All are documented as required for POST and PUT, and optional for PATCH.
- **Headers:** `Content-Type` (application/json or text/xml) and `Accept` (application/json or application/xml).
- **No error responses are documented** for any endpoint.

## 5. Repository structure

```
restful-booker-manual-api-testing/
├── Restful-Booker-Manual-API-Testing.postman_collection.json   # 129 test cases in 19 folders
├── Restful-Booker-Environment.postman_environment.json         # base_url, username, password, booking_id, token
├── README.md                                                  # this guide
├── Test-Scenarios.md                                          # test-case inventory with IDs, data, expected results
└── Test-Execution-Report-Template.md                          # reusable execution log + defect log
```

## 6. Import into Postman

1. Open Postman and select your workspace.
2. Click **Import** (top left), or use **File → Import**.
3. Drag in **both** JSON files, or browse to them, and confirm the import.
4. In the sidebar, open **Collections**: you'll see **Restful Booker - Manual API Testing Practice** with folders `00` to `18`.
5. In the sidebar, open **Environments**: you'll see **Restful Booker Environment**.

## 7. Environment setup

1. Select **Restful Booker Environment** in the **environment selector** at the top right of Postman.
2. Open **Environments → Restful Booker Environment** and check the variables:

| Variable | Initial value | You change it? | Purpose |
|---|---|---|---|
| `base_url` | `https://restful-booker.herokuapp.com` | No | Root of every request URL |
| `username` | `admin` | No | Documented demo username (Basic Auth and `/auth`) |
| `password` | `password123` | No | Documented demo password |
| `booking_id` | _(empty)_ | **Yes, manually** | ID of a booking **you** created |
| `token` | _(empty)_ | **Yes, manually** | Token returned by `POST /auth` |

3. Hover over `{{base_url}}` in any request URL: it should resolve to the base URL. If it's red or unresolved, no environment is selected.
4. Send **00.01** (`GET /ping`). Expect `201 Created`.

**Value columns:** current Postman versions show a **Value / Local value** (stays on your machine) and a **Shared value** (synced to your workspace). Older versions call them **Current value** and **Initial value**. Paste tokens and IDs into the **local/current** value. Recent versions save variable changes automatically; older versions need **Ctrl/Cmd + S**.

**Security:** the demo credentials are public, so this environment keeps them as plain variables you can see while learning. Treat the habit seriously anyway. On real projects, mark sensitive variables as secure/secret, never put real credentials in a collection or environment you share or commit, and **clear `token` and `booking_id` before exporting** an environment.

## 8. How the collection is organised

| Folder | Focus | Requests |
|---|---|---|
| 00 - Introduction and Health Check | Setup, rules, health check | 1 |
| 01 - API Fundamentals and Request Anatomy | Client-server, base URL vs endpoint, request/response anatomy | 3 |
| 02 - HTTP Methods | GET, POST, PUT, PATCH, DELETE; full vs partial update | 7 |
| 03 - Status Codes | Status code classes; 404 vs 405; 401 vs 403; 4xx vs 5xx | 5 |
| 04 - Headers and Content Types | Accept, Content-Type, missing/incorrect headers, side effects | 6 |
| 05 - Query and Path Parameters | Query filters, path parameters, missing/malformed values | 13 |
| 06 - JSON and Request Body | JSON types, nested objects, arrays, null, invalid syntax | 8 |
| 07 - Authentication | Tokens, valid/invalid/missing credentials, saving the token manually | 5 |
| 08 - Authorization | Token vs Basic Auth, missing/invalid/malformed credentials | 7 |
| 09 - API Contracts and Response Validation | Manual contract checklist: fields, types, formats, headers, consistency | 4 |
| 10 - Positive Testing | Valid-input variations for every operation | 7 |
| 11 - Negative Testing | Invalid IDs, credentials, fields, types, JSON, auth, headers, methods | 10 |
| 12 - Boundary Testing | Exploratory boundaries: price, strings, dates, IDs, optional fields | 12 |
| 13 - Business Validation | Data consistency, update semantics, delete effectiveness | 9 |
| 14 - Test Case Design | EP, BVA, decision tables, state transitions, traceability | 4 |
| 15 - API Chaining | Manual chaining of booking ID and token; broken chains | 5 |
| 16 - CRUD Workflow | Create → Read → Update → Partial update → Delete → Verify | 9 |
| 17 - End-to-End Booking Flow | Health → Auth → Create → Validate → Update → Patch → Delete → Verify | 10 |
| 18 - Cleanup and Reusable Requests | Practice booking, fresh token, cleanup | 4 |
| **Total** |  | **129** |

- **Naming:** `NN.MM [RB-AREA-NNN] Title`. For example, `02.03 [RB-PUT-001] PUT - full update of your booking (all fields)`. The number gives the execution order; the ID links to `Test-Scenarios.md` and your execution report.
- **Request instructions:** open a request's **Docs** tab. Each one contains the Test Case ID, priority, type, concept, *What this request does*, test scenario, preconditions, test data, *What you need to enter*, steps, *What to inspect*, expected result (status code, reason, behaviour, source of the expectation, pass/fail criteria), common mistakes, a *Record your result* table and, sometimes, a mentor note.
- **Chapter theory:** open a folder's **Overview** tab.
- **Parameters and headers:** every query parameter, path variable and header has a description explaining its purpose (Params and Headers tabs).
- **Authentication in requests:** concept chapters use the documented **Basic Auth** alternative (Authorization tab, built from `{{username}}`/`{{password}}`), so they work without a token. Token-based requests set the **Authorization tab to No Auth** and send `Cookie: token={{token}}` in Headers, exactly as documented.
- **Manual-only:** there's nothing in any **Scripts** tab and there are no saved example responses. You judge every result yourself.
- **Test data markers:** negative and boundary tests use last names such as `RB-BND-003`, so you can find any booking a test created with `GET /booking?lastname=RB-BND-003`.
- **Why some requests look alike:** a few operations appear in more than one folder on purpose, for example `POST /auth` with valid credentials (07.01, 10.01, 15.03, 17.02, 18.02) and the practice booking (01.02, 18.01). Each copy is a separate test case with its own ID and objective, and the workflow folders (15-17) and utilities (18) are kept self-contained so you never have to jump between folders mid-flow.

## 9. Recommended execution order

Work through the folders in order, sending requests by their number. A suggested plan:

| Session | Folders | Requests | Before you start |
|---|---|---|---|
| 1 | 00, 01, 02 | 11 | Import both files and select the environment. 01.02 creates your practice booking. |
| 2 | 03, 04 | 11 | Run **18.01** first: 02.06 deleted your practice booking. |
| 3 | 05, 06 | 21 | Folder 05 needs **fresh standard data**: run 18.01. |
| 4 | 07, 08, 09 | 16 | 07.01 saves your token. Folder 09 needs fresh standard data (18.01). |
| 5 | 10, 11, 12 | 29 | Run 18.01 and 18.02 first. 10.07 deletes the 10.04 booking, not your practice booking. |
| 6 | 13, 14 | 13 | 13 creates its own booking. 14.01 uses the booking deleted in 13.07; then run 18.01 and 18.02. |
| 7 | 15, 16, 17 | 24 | Self-contained flows. Run each folder in one sitting. |
| Any time | 18 | 4 | Utilities: new practice booking, new token, cleanup. |

**State rules to remember**

- Requests that use `{{booking_id}}` need a booking **you** created that still exists. When in doubt, run **18.01** and paste the new ID.
- Requests that use `{{token}}` need a recent token. When in doubt, run **18.02**.
- Folders 13, 15, 16 and 17 create their own bookings and overwrite `booking_id`. That's expected.
- **Use fresh IDs:** the API resets periodically and restarts its ID counter, so an old `booking_id` can point to someone else's booking. Create a fresh practice booking at the start of each folder and after any break. Before a PUT, PATCH or DELETE on an older booking, GET it and check it still shows the changes you made.

## 10. Manual chaining: saving the booking ID and token

**Method A: copy and paste (primary)**

1. Send the producing request (`POST /booking` → `bookingid`, or `POST /auth` → `token`).
2. In the response body, select **only the value** (no quotes, no comma) and copy it.
3. Open **Environments → Restful Booker Environment**, paste it into the value of `booking_id` or `token`, and save if your version requires it.
4. In the consuming request, hover over `{{booking_id}}` or `{{token}}` to confirm the value.

**Method B: right-click (still manual)**

Select the value in the response → right-click → **Set as variable** → choose `booking_id` or `token` in **Restful Booker Environment**.

**When to copy:** immediately after a request that *produces* a value, before running anything that *consumes* it, and again whenever you create a new booking or token, or after an API reset. Folder **15** explains the full relationship map and how to diagnose broken chains.

## 11. Running the CRUD workflow

Folder **16 - CRUD Workflow** is self-contained and uses **one** booking ID throughout:

| # | Request | Manual action | Expected |
|---|---|---|---|
| 1 | 16.01 Create (POST) | copy `bookingid` → `booking_id` | 200 OK |
| 2 | 16.02 Read (GET) | compare with the 16.01 body | 200 OK |
| 3 | 16.03 Update (PUT) | - | 200 OK |
| 4 | 16.04 Read (GET) | compare with the 16.03 body | 200 OK |
| 5 | 16.05 Partial update (PATCH) | - | 200 OK |
| 6 | 16.06 Read (GET) | check changed and preserved fields | 200 OK |
| 7 | 16.07 Delete (DELETE) | read the warning first | 201 Created |
| 8 | 16.08 Read deleted (GET) | - | not found (404 by convention) |
| 9 | 16.09 Search deleted (GET) | - | ID absent |

It uses Basic Auth, so no token is needed. If you stop early, delete the booking with **18.03**.

## 12. Running the end-to-end flow

Folder **17 - End-to-End Booking Flow** follows a realistic guest journey with the **token** mechanism:

1. 17.01 Health check (201) → stop and mark the run **Blocked** if it fails
2. 17.02 Authenticate → **save `token`**
3. 17.03 Create the booking → **save `booking_id`**
4. 17.04 Retrieve **and** validate all important fields (validation table in its Docs tab)
5. 17.05 Update (PUT) → 17.06 verify updated values
6. 17.07 Partial update (PATCH) → 17.08 verify preserved and changed fields
7. 17.09 Delete → 17.10 verify deletion behaviour
8. Clean up: clear `booking_id` and `token` (see 18.04)

Run it without long pauses. If the API resets mid-flow (a sudden 404, or a 403 with a token you just saved), start again from 17.02. Record it as one end-to-end result: **Pass** only if every step passed.

## 13. Recording actual results

1. Copy `Test-Execution-Report-Template.md` for each run (for example `reports/2026-10-12-run-01.md`).
2. For each executed test, record: **Execution Date**, **Environment** (public or local), **Actual Result** (start with the status code and text, then the key facts), **Pass/Fail/Blocked**, **Defect ID**, **Remarks**.
3. **Documented vs observed:** the *Expected Result* is what the documentation (or the stated convention) says. The *Actual Result* is what **you** observed. Never copy the mentor notes into *Actual Result*: they describe a reference build, not your run.
4. **Pass/Fail rules:** use the *Mark as Pass if / Mark as Fail if* lines in each request's Docs tab. For *Investigate* tests, a debatable behaviour can be logged as an **observation/question** instead of a defect.
5. **Evidence:** for each failure, keep a screenshot of the request and response, or the Postman Console entry showing the exact request sent.
6. **Defects:** log them in the report's defect table with ID (`DEF-001`…), title, severity, steps, expected vs actual, and the test case ID(s).

## 14. Troubleshooting

| Symptom | Likely cause | What to do |
|---|---|---|
| `{{base_url}}` is red, or 'Could not send request' | No environment selected | Select **Restful Booker Environment** (top right) |
| Timeout or connection error | API down, slow wake-up, network/proxy/firewall/VPN | Retry later; mark the test **Blocked**; check whether your network allows `herokuapp.com` |
| `404` for *your* booking | `booking_id` wrong, has spaces or quotes, deleted, or wiped by a reset | Run **18.01**, paste the new ID |
| `GET /booking/{{booking_id}}` returns a **list** | `booking_id` is empty (URL becomes `/booking/`) | Fill `booking_id` |
| `403` on PUT/PATCH/DELETE | Token missing, quoted or stale; `Cookie` lacks `token=`; wrong Authorization setting | Run **18.02**, paste without quotes; check `Cookie: token={{token}}`; check the Authorization tab |
| `418 I'm a Teapot` | Missing or unsupported `Accept` header | Use `Accept: application/json` (or Postman's default `*/*`); see folder 04 |
| `500` on POST | Missing/invalid fields or wrong `Content-Type` | Compare with the 01.02 body and headers. In negative tests this may be the finding |
| `400 Bad Request` | Malformed JSON | Check commas, quotes and braces. In negative tests this may be expected |
| Unexpected success without credentials | A cookie stored in Postman's cookie jar is being sent | Open **Cookies** (below Send) and remove stored cookies for the domain |
| Cookie header seems ignored (Postman web) | Browsers don't let web pages set the `Cookie` header | Use the desktop app or Postman's desktop agent, or the Basic Auth alternative |
| Results differ from a mentor note | Public instance differs, other users' data, or a reset | Record what **you** observe; that's the point |

## 15. Limitations of the public shared API

- **Shared data:** anyone can read, change or delete bookings, including yours. Use only fictional test data (never real names, emails or other personal data) and modify only bookings you created.
- **Periodic reset:** the home page states the API resets every 10 minutes. Bookings and tokens can disappear mid-session, and IDs may be reused by new bookings. Always check that a booking returned for `booking_id` contains **your** data.
- **Deliberate bugs:** this is a practice API. Behaviour often differs from the documentation and from good practice. That's what makes it a good teacher, but it's not a model of correct API design.
- **Thin documentation:** no error responses, limits, rate limits or business rules are documented, so many expectations are *Investigate*.
- **No guarantees:** availability and performance aren't guaranteed, and the first request after an idle period may be slow.
- **Data-dependent results:** filter results include other users' bookings. Search for your own ID.
- **Be a good citizen:** no load testing, no scripted flooding, and no destructive tests against data you didn't create.

## 16. Documentation review notes

Reviewing documentation is static testing. While building this project, these points were found in the official documentation data (verified 10 October 2026). They make good first entries in your observations log:

1. The **PartialUpdateBooking** curl examples use `curl -X PUT` instead of `PATCH`.
2. The PartialUpdateBooking `Cookie`/`Authorization` header descriptions say they give access to *"the PUT endpoint"*.
3. DeleteBooking describes its `id` parameter as *"ID for the booking you want to update"*.
4. The `id` parameter is typed **String** for GetBooking but **Number** for UpdateBooking, PartialUpdateBooking and DeleteBooking.
5. The `Authorization` header's default value is cut off at `Basic`, and the rest of the value spills into the description.
6. `additionalneeds` is documented as **required** for POST and PUT, but optional for PATCH. Test 06.02 checks what the API actually does.
7. HealthCheck and DeleteBooking list `201 Created` responses under a *"Success 200"* heading.
8. CreateToken says the token is for *"PUT and DELETE"*. PATCH also accepts it.
9. No endpoint documents any error response (400, 401, 403, 404, 405, 418, 500…).
10. DeleteBooking's endpoint title uses the literal path `booking/1` instead of `booking/:id`.
11. The PUT and PATCH URL-encoded examples send `Accept: application/x-www-form-urlencoded`, which isn't one of the documented Accept values (application/json or application/xml).
12. The URL-encoded examples for POST and PUT omit `additionalneeds`, although it's documented as required.
13. The CreateBooking curl examples don't send an `Accept` header, although `Accept` is listed as a header without being marked optional.

## 17. How this project was verified

- **Documentation:** every endpoint, method, header, parameter, field and documented status code was checked against the official apidoc data that the documentation page renders.
- **JSON:** both files parse as valid JSON (UTF-8).
- **Schema:** the collection validates against the official **Postman Collection v2.1.0** JSON schema, with 0 errors.
- **Variables:** every `{{variable}}` in requests exists in the environment (`base_url`, `username`, `password`, `booking_id`, `token`). The only exception is the deliberate typo `{{bookingId}}` in test 15.05.
- **No scripts:** the collection contains no `event`, pre-request or test scripts.
- **Execution:** all 129 requests were executed once with Postman's runtime (Newman, used only for authoring-time verification) against a **local build of the official Restful Booker source** (commit 0046115, March 2026), simulating the manual copy/paste steps. Every request ran, and every status code matched the reference observations in the mentor notes.
- **Limitation:** the authoring environment couldn't reach the public instance at `restful-booker.herokuapp.com`, so behaviour there wasn't observed directly and may differ. That's why expected results are documentation-based and your recorded observations are what count.

## 18. Publishing on GitHub

1. Create an empty repository on GitHub (for example `restful-booker-manual-api-testing`) without a README.
2. In the folder that contains the five files:

```bash
git init
git add .
git commit -m "Add Restful Booker manual API testing project"
git branch -M main
git remote add origin https://github.com/<your-username>/restful-booker-manual-api-testing.git
git push -u origin main
```

3. Recommended `.gitignore` (create it before your first commit if you keep personal files nearby):

```gitignore
# Postman exports that might contain your local values (tokens, IDs)
*.local.postman_environment.json
# Private notes and raw evidence you don't want to publish
private/
.DS_Store
Thumbs.db
```

4. For later changes, work on a branch and open a pull request, even on a personal repo. It builds the habit and keeps `main` clean:

```bash
git checkout -b docs/execution-run-01
mkdir -p reports && cp Test-Execution-Report-Template.md reports/2026-10-12-run-01.md
# fill in reports/2026-10-12-run-01.md
git add reports/
git commit -m "Add execution report for run 01"
git push -u origin docs/execution-run-01
# open a pull request on GitHub, review the diff, then merge
```

5. **Before every commit:** if you re-export the collection or environment from Postman, open the files and confirm `token` and `booking_id` are empty and that no real credentials appear.
6. Make the portfolio shine: add a short repository description and topics (`api-testing`, `postman`, `manual-testing`, `qa`, `restful-booker`), add a `LICENSE` of your choice, include your execution reports and defect log, and add screenshots of interesting findings.

## 19. Future scope: Python requests + pytest

The manual test cases map one-to-one onto automated tests. Keep the IDs in test names (for example `test_rb_get_001_...`) for traceability.

**Suggested structure**

```
restful-booker-api-automation/
├── tests/
│   ├── conftest.py            # fixtures: base_url, credentials, token, booking (with cleanup)
│   ├── test_health.py         # RB-HC-*
│   ├── test_auth.py           # RB-AUTH-*, RB-AUTHZ-*
│   ├── test_booking_crud.py   # RB-GET/POST/PUT/PATCH/DEL-*, RB-CRUD-*
│   ├── test_negative.py       # RB-NEG-* (parametrized)
│   └── test_boundary.py       # RB-BND-* (parametrized)
├── schemas/booking.schema.json  # contract from folder 09 as JSON Schema
├── requirements.txt           # pinned versions (requests, pytest, jsonschema)
├── pytest.ini                 # markers: smoke, negative, boundary, known_defect
└── .env.example               # variable NAMES only (RB_BASE_URL, RB_USERNAME, RB_PASSWORD), no real values
```

**A first test file**

```python
import os

import pytest
import requests

BASE_URL = os.getenv("RB_BASE_URL", "https://restful-booker.herokuapp.com")
TIMEOUT = 15  # seconds


@pytest.fixture(scope="session")
def credentials():
    username, password = os.getenv("RB_USERNAME"), os.getenv("RB_PASSWORD")
    if not username or not password:
        pytest.skip("Set RB_USERNAME and RB_PASSWORD (the public demo credentials from the API docs).")
    return username, password


@pytest.fixture
def booking_id(credentials):
    """Create a booking for one test and delete it afterwards."""
    payload = {
        "firstname": "Asha",
        "lastname": "Verma",
        "totalprice": 4500,
        "depositpaid": True,
        "bookingdates": {"checkin": "2027-01-15", "checkout": "2027-01-20"},
        "additionalneeds": "Breakfast",
    }
    response = requests.post(f"{BASE_URL}/booking", json=payload,
                             headers={"Accept": "application/json"}, timeout=TIMEOUT)
    response.raise_for_status()
    new_id = response.json()["bookingid"]
    yield new_id
    requests.delete(f"{BASE_URL}/booking/{new_id}", auth=credentials, timeout=TIMEOUT)


def test_rb_hc_001_health_check_returns_201():
    response = requests.get(f"{BASE_URL}/ping", timeout=TIMEOUT)
    assert response.status_code == 201


def test_rb_get_001_get_booking_returns_submitted_data(booking_id):
    response = requests.get(f"{BASE_URL}/booking/{booking_id}",
                            headers={"Accept": "application/json"}, timeout=TIMEOUT)
    assert response.status_code == 200
    body = response.json()
    assert body["firstname"] == "Asha"
    assert body["bookingdates"] == {"checkin": "2027-01-15", "checkout": "2027-01-20"}
```

**Roadmap**

1. Automate the smoke path first (RB-HC-001, RB-AUTH-001, folder 16).
2. Turn folders 11 and 12 into `pytest.mark.parametrize` tables.
3. Validate response contracts with JSON Schema (the folder 09 checklist).
4. Mark confirmed defects with `pytest.mark.xfail(strict=True, reason="DEF-00x")`, so you notice when one is fixed.
5. Run against a **local** Restful Booker instance (the official repo provides Docker files) for deterministic results, and use the public instance only for smoke checks.
6. Add CI (for example GitHub Actions) with JUnit/HTML reports, reviewed through pull requests.

Read credentials from environment variables or your CI's secret store, never from source code, and check any new tool against your organisation's approved-software list.

## 20. Credits and disclaimer

- **Restful Booker** was created by **Mark Winteringham** and is open source (GPL-3.0): https://github.com/mwinteringham/restful-booker. This project is an independent learning resource. It isn't affiliated with or endorsed by the API's author and contains none of its code.
- Expected results reflect the official documentation as verified on 10 October 2026. The API and its documentation may change, so re-verify before relying on any expectation.
- All test data is fictional.
