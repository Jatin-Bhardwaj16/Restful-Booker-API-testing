# Test Scenarios - Restful Booker Manual API Testing

Structured inventory of all **129 manual test cases** in the Postman collection `Restful-Booker-Manual-API-Testing.postman_collection.json`, grouped by concept (one section per collection folder).

Each test case is also fully documented in the **Docs** tab of its Postman request, with steps, what to inspect, common mistakes and pass/fail criteria.

## How to read this inventory

- **ID scheme:** `RB-<AREA>-<NNN>`. Area codes: HC health check, FUND fundamentals, GET/POST/PUT/PATCH/DEL HTTP methods, STAT status codes, HDR headers, PARAM parameters, JSON request body, AUTH authentication, AUTHZ authorization, CON contracts, POS positive, NEG negative, BND boundary, BIZ business validation, TCD test case design, CHAIN chaining, CRUD workflow, E2E end-to-end, UTIL reusable/cleanup.
- **Request:** the numbered Postman request (`NN.MM`) that executes the test.
- **Basis:** where the expected result comes from.
  - *Documented*: the official documentation states it. A deviation is a defect.
  - *Partly documented*: the documentation states the rule but not the response.
  - *Investigate*: the documentation is silent. The expectation is an HTTP convention or business rule, so record what you observe.
- **Priority:** High = core flow, security or data integrity; Medium = important variation; Low = nice to know.
- **Preconditions** assume the environment is imported and selected. `booking_id` and `token` are filled manually (see README).

Official documentation: https://restful-booker.herokuapp.com/apidoc/index.html (verified 10 October 2026).

## Summary

| Folder | Test cases |
|---|---|
| 00 - Introduction and Health Check | 1 |
| 01 - API Fundamentals and Request Anatomy | 3 |
| 02 - HTTP Methods | 7 |
| 03 - Status Codes | 5 |
| 04 - Headers and Content Types | 6 |
| 05 - Query and Path Parameters | 13 |
| 06 - JSON and Request Body | 8 |
| 07 - Authentication | 5 |
| 08 - Authorization | 7 |
| 09 - API Contracts and Response Validation | 4 |
| 10 - Positive Testing | 7 |
| 11 - Negative Testing | 10 |
| 12 - Boundary Testing | 12 |
| 13 - Business Validation | 9 |
| 14 - Test Case Design | 4 |
| 15 - API Chaining | 5 |
| 16 - CRUD Workflow | 9 |
| 17 - End-to-End Booking Flow | 10 |
| 18 - Cleanup and Reusable Requests | 4 |
| **Total** | **129** |

| Priority | Count |  | Type | Count |  | Basis | Count |
|---|---|---|---|---|---|---|---|
| High | 86 |  | Positive | 48 |  | Documented | 56 |
| Medium | 39 |  | Negative | 41 |  | Investigate | 49 |
| Low | 4 |  | Verification | 16 |  | Partly documented | 24 |
|  |  |  | Boundary | 12 |  |  |  |
|  |  |  | Exploratory | 8 |  |  |  |
|  |  |  | Setup | 4 |  |  |  |

## Concept coverage

| Learning concept | Where it's practised |
|---|---|
| A. API fundamentals | 01 (RB-FUND-001…003), 00 |
| B. HTTP methods (incl. PUT vs PATCH) | 02 (RB-GET-001, RB-POST-001, RB-PUT-001/002, RB-PATCH-001, RB-DEL-001/002) |
| C. Status codes | 03 (RB-STAT-001…005) and the expected/actual status of every test |
| D. Request anatomy | 01 (RB-FUND-001…003) |
| E. Query and path parameters | 05 (RB-PARAM-001…013), 12 (IDs) |
| F. Headers and content types | 04 (RB-HDR-001…006), 11 (RB-NEG-008) |
| G. JSON and request body | 06 (RB-JSON-001…008) |
| H. Authentication | 07 (RB-AUTH-001…005), 11 (RB-NEG-003) |
| I. Authorization | 08 (RB-AUTHZ-001…007), 14 (RB-TCD-002/003) |
| J. API contracts and response validation | 09 (RB-CON-001…004) |
| K. Positive testing | 10 (RB-POS-001…007) |
| L. Negative testing | 11 (RB-NEG-001…010) |
| M. Boundary testing | 12 (RB-BND-001…012) |
| N. Business validation | 13 (RB-BIZ-001…009) |
| O. Test case design | 14 (RB-TCD-001…004) and the template used by every test |
| P. API chaining | 15 (RB-CHAIN-001…005); full chain executed in 16 and 17 |
| Q. CRUD workflow | 16 (RB-CRUD-001…009) |
| R. End-to-end flow | 17 (RB-E2E-001…010) |
| Cleanup and reusable requests | 18 (RB-UTIL-001…004) |

## Endpoint traceability

| Endpoint (documented name) | Test cases |
|---|---|
| GET /ping (HealthCheck) | RB-HC-001, RB-E2E-001 |
| POST /auth (CreateToken) | RB-AUTH-001, RB-AUTH-002, RB-AUTH-003, RB-AUTH-004, RB-AUTH-005, RB-POS-001, RB-NEG-003, RB-CHAIN-003, RB-E2E-002, RB-UTIL-002 |
| GET /booking (GetBookingIds) | RB-FUND-001, RB-HDR-006, RB-PARAM-001, RB-PARAM-002, RB-PARAM-003, RB-PARAM-004, RB-PARAM-005, RB-PARAM-006, RB-PARAM-007, RB-PARAM-008, RB-PARAM-009, RB-PARAM-010, RB-PARAM-011, RB-CON-001, RB-POS-002, RB-BND-009, RB-BIZ-009, RB-CRUD-009 |
| GET /booking/{id} (GetBooking) | RB-GET-001, RB-DEL-002, RB-STAT-001, RB-HDR-001, RB-HDR-002, RB-PARAM-013, RB-CON-002, RB-POS-003, RB-NEG-001, RB-BND-010, RB-BND-011, RB-BIZ-002, RB-BIZ-008, RB-CHAIN-002, RB-CHAIN-005, RB-CRUD-002, RB-CRUD-004, RB-CRUD-006, RB-CRUD-008, RB-E2E-004, RB-E2E-006, RB-E2E-008, RB-E2E-010, RB-UTIL-004 |
| POST /booking (CreateBooking) | RB-FUND-002, RB-POST-001, RB-STAT-005, RB-HDR-003, RB-HDR-004, RB-HDR-005, RB-JSON-001, RB-JSON-002, RB-JSON-003, RB-JSON-004, RB-JSON-005, RB-JSON-006, RB-JSON-007, RB-JSON-008, RB-CON-003, RB-POS-004, RB-NEG-004, RB-NEG-005, RB-NEG-008, RB-BND-001, RB-BND-002, RB-BND-003, RB-BND-004, RB-BND-005, RB-BND-006, RB-BND-007, RB-BND-008, RB-BND-012, RB-BIZ-001, RB-TCD-004, RB-CHAIN-001, RB-CRUD-001, RB-E2E-003, RB-UTIL-001 |
| PUT /booking/{id} (UpdateBooking) | RB-PUT-001, RB-PUT-002, RB-STAT-003, RB-POS-005, RB-NEG-006, RB-NEG-007, RB-BIZ-003, RB-BIZ-006, RB-CRUD-003, RB-E2E-005 |
| PATCH /booking/{id} (PartialUpdateBooking) | RB-FUND-003, RB-PATCH-001, RB-STAT-004, RB-AUTHZ-001, RB-AUTHZ-002, RB-AUTHZ-003, RB-AUTHZ-004, RB-AUTHZ-005, RB-AUTHZ-006, RB-CON-004, RB-POS-006, RB-NEG-002, RB-BIZ-004, RB-BIZ-005, RB-TCD-001, RB-TCD-002, RB-TCD-003, RB-CHAIN-004, RB-CRUD-005, RB-E2E-007 |
| DELETE /booking/{id} (DeleteBooking) | RB-DEL-001, RB-STAT-002, RB-AUTHZ-007, RB-POS-007, RB-BIZ-007, RB-CRUD-007, RB-E2E-009, RB-UTIL-003 |
| GET /booking/ (missing ID, intentional) | RB-PARAM-012 |
| POST /booking/{id} (not documented, intentional negative) | RB-NEG-009 |
| GET /bookings (typo, intentional negative) | RB-NEG-010 |

## 00 - Introduction and Health Check

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-HC-001 | 00.01 | Verify that the Restful Booker API is up and responding. | Environment selected. | None. No parameters, headers or body. | 201 Created (documented); plain-text body. | Documented | High | Positive |

## 01 - API Fundamentals and Request Anatomy

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-FUND-001 | 01.01 | Retrieve the list of booking IDs and identify every part of the request and the response. | Environment selected. | None. Two optional query parameters (`firstname`, `lastname`) appear in **Params** but are unticked (disabled). | 200 OK; JSON array of {bookingid} objects (documented). | Documented | High | Positive |
| RB-FUND-002 | 01.02 | Create a booking with valid data and save its ID for later requests. | Environment selected. | Body: firstname `Asha`, lastname `Verma`, totalprice `4500`, depositpaid `true`, checkin `2027-01-15`, checkout `2027-01-20`, additionalneeds `Breakfast` (the standard practice data). | 200 OK; numeric bookingid; booking object echoes the request (documented). | Documented | High | Positive |
| RB-FUND-003 | 01.03 | Send an authenticated partial update and inspect the complete HTTP request and response. | Practice booking you created in `booking_id`. | Path `id` = `{{booking_id}}`. Basic Auth from `{{username}}` / `{{password}}`. Body: `{"additionalneeds": "Breakfast and late checkout"}`. | 200 OK; only additionalneeds changed (documented). | Documented | High | Positive |

## 02 - HTTP Methods

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-GET-001 | 02.01 | Retrieve an existing booking and confirm that repeated GETs return identical data. | Practice booking you created in `booking_id`. | Path `id` = `{{booking_id}}`; header `Accept: application/json`. | 200 OK; booking JSON; identical on repeat (documented). | Documented | High | Positive |
| RB-POST-001 | 02.02 | Send the same POST twice and confirm that two separate bookings are created. | Environment selected. | Body: Rahul Nair, totalprice `3200`, depositpaid `false`, 2027-02-10 → 2027-02-12, additionalneeds `Airport pickup`. | 200 OK on each send; two different bookingids. | Documented | High | Positive |
| RB-PUT-001 | 02.03 | Update all fields of an existing booking with PUT. | Practice booking you created in `booking_id`. Credentials are set in the environment (`username`, `password`). | Body with **all** fields: firstname `Asha`, lastname `Verma-Rao`, totalprice `5200`, depositpaid `false`, 2027-02-01 → 2027-02-05, additionalneeds `Dinner`. | 200 OK; every field replaced (documented). | Documented | High | Positive |
| RB-PATCH-001 | 02.04 | Update one field with PATCH and confirm the other fields are untouched. | Practice booking you created in `booking_id`. Run 02.03 first so you know the current values. | Body: `{"totalprice": 5600}`. | 200 OK; only totalprice changes (documented). | Documented | High | Positive |
| RB-PUT-002 | 02.05 | A PUT with an incomplete body must not be accepted as a full update. | Practice booking you created in `booking_id`. Run 02.04 first (the current price is 5600). | Body: `{"totalprice": 5800}` only. Every other documented field is missing. A different price from 02.04 lets you see whether anything changed. | Rejected with 4xx (likely 400); booking unchanged. Error code not documented. | Partly documented | High | Negative |
| RB-DEL-001 | 02.06 | Delete an existing booking that you created. | Practice booking you created in `booking_id`. | Path `id` = `{{booking_id}}`; Basic Auth; no body. | 201 Created (documented); booking removed. | Documented | High | Positive |
| RB-DEL-002 | 02.07 | A deleted booking must no longer be retrievable. | Environment selected. 02.06 returned success, and `booking_id` still contains the deleted ID. | Path `id` = `{{booking_id}}` (deleted); header `Accept: application/json`. | Booking not returned; 404 expected by convention (not documented). | Investigate | High | Verification |

## 03 - Status Codes

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-STAT-001 | 03.01 | Retrieving a non-existent booking returns a 'not found' client error. | Environment selected. | Path `id` = `999999999` (fixed non-existent test value, not a real booking). | 404 Not Found expected by convention (not documented). | Investigate | High | Negative |
| RB-STAT-002 | 03.02 | Deleting a non-existent booking returns a 'not found' client error consistent with GET. | Environment selected. | Path `id` = `999999999`; Basic Auth (so the request isn't rejected for missing credentials). | 404 expected by convention, consistent with GET (not documented). | Investigate | Medium | Negative |
| RB-STAT-003 | 03.03 | An update without credentials is rejected and doesn't change the booking. | Practice booking you created in `booking_id`. | Path `id` = `{{booking_id}}`; Authorization = **No Auth**; valid full body with lastname `Verma-NoAuth` and totalprice `9999`. | Rejected with 401/403; booking unchanged (error code not documented). | Investigate | High | Negative |
| RB-STAT-004 | 03.04 | A malformed JSON body is rejected with a client error. | Practice booking you created in `booking_id`. | Body: `{ additionalneeds: "Late checkout" }` (invalid: unquoted key). Basic Auth. | 400 Bad Request expected by convention; booking unchanged. | Investigate | High | Negative |
| RB-STAT-005 | 03.05 | Creating a booking without any required field is rejected with a client error. | Environment selected. | Body: `{}`. | Rejected with 4xx (likely 400); no booking created. Error code not documented. | Partly documented | High | Negative |

## 04 - Headers and Content Types

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-HDR-001 | 04.01 | Retrieve a booking in the documented alternative format (XML). | Practice booking you created in `booking_id`. | Header `Accept: application/xml`. | 200 OK with an XML body and the same values (documented); an XML Content-Type is expected by convention. | Partly documented | Medium | Positive |
| RB-HDR-002 | 04.02 | Retrieve a booking when the client doesn't send an Accept header. | Practice booking you created in `booking_id`. | No Accept header (auto-generated Accept disabled). | 200 with JSON (default) or a clear 400/406; behaviour without Accept not documented. | Partly documented | Medium | Exploratory |
| RB-HDR-003 | 04.03 | A request whose Content-Type doesn't match its body is rejected with a client error. | Environment selected. | Header `Content-Type: text/plain`; body: a valid booking with lastname `RB-HDR-003` (a marker to find it later). | 415/400 expected by convention; no booking created (not documented). | Investigate | High | Negative |
| RB-HDR-004 | 04.04 | A request with a body but no Content-Type is handled with a clear client error. | Environment selected. | No Content-Type header; body: a valid booking with lastname `RB-HDR-004`. | Clear 4xx (415/400) or correct handling; never 5xx (not documented). | Investigate | Medium | Negative |
| RB-HDR-005 | 04.05 | If the server rejects a create request because of an unsupported Accept value, it must not create the booking. | Environment selected. | Header `Accept: text/plain`; body: a valid booking with lastname `RB-HDR-005`. | 406 expected by convention and no booking created (not documented). | Investigate | High | Negative |
| RB-HDR-006 | 04.06 | A request that returned an error must leave no booking behind. | Environment selected. 04.05 was just executed. | Query `lastname=RB-HDR-005` (or the unique value you used). | 200 OK and [] if 04.05 had no side effect. | Partly documented | High | Verification |

## 05 - Query and Path Parameters

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-PARAM-001 | 05.01 | Filtering by firstname returns your booking's ID. | Fresh practice booking with standard data in `booking_id` (18.01). | Query `firstname=Asha`. | 200 OK; array contains your booking_id (documented). | Documented | High | Positive |
| RB-PARAM-002 | 05.02 | Filtering by lastname returns your booking's ID. | Fresh practice booking with standard data in `booking_id` (18.01). | Query `lastname=Verma`. | 200 OK; array contains your booking_id (documented). | Documented | Medium | Positive |
| RB-PARAM-003 | 05.03 | Combining firstname and lastname returns only bookings matching both, including yours. | Fresh practice booking with standard data in `booking_id` (18.01). | Query `firstname=Asha&lastname=Verma`. | 200 OK; your booking_id present; AND semantics (documented example). | Documented | High | Positive |
| RB-PARAM-004 | 05.04 | A checkin filter earlier than your check-in date returns your booking. | Fresh practice booking with standard data in `booking_id` (18.01). | Query `checkin=2027-01-14`. Your booking checks in on 2027-01-15. | 200 OK; your booking included (check-in 2027-01-15 >= 2027-01-14) (documented). | Documented | High | Positive |
| RB-PARAM-005 | 05.05 | A checkout filter earlier than your check-out date returns your booking (documented: check-out >= filter date). | Fresh practice booking with standard data in `booking_id` (18.01). | Query `checkout=2027-01-19`. Your booking checks out on 2027-01-20. | 200 OK; your booking included (check-out 2027-01-20 >= 2027-01-19) (documented). | Documented | High | Positive |
| RB-PARAM-006 | 05.06 | Combined date filters that both match your booking return its ID. | Fresh practice booking with standard data in `booking_id` (18.01). | Query `checkin=2027-01-14&checkout=2027-01-19`. | 200 OK; your booking included (documented). | Documented | Medium | Positive |
| RB-PARAM-007 | 05.07 | A search with no matches returns an empty list, not an error. | Environment selected. | Query `firstname=NoSuchGuestZz9`. | 200 OK with [] expected by convention (not documented). | Investigate | Medium | Negative |
| RB-PARAM-008 | 05.08 | Find out whether the firstname filter is case-sensitive. | Fresh practice booking with standard data in `booking_id` (18.01). | Query `firstname=asha`. | 200 OK; record whether matching is case-sensitive (not documented). | Investigate | Low | Exploratory |
| RB-PARAM-009 | 05.09 | A date filter in the wrong format is rejected with a clear client error. | Environment selected. | Query `checkin=15-01-2027`. | 400 expected by convention; never 5xx (format documented, error not). | Partly documented | High | Negative |
| RB-PARAM-010 | 05.10 | Discover how the API treats an empty filter value. | Environment selected. | Query `firstname=` (empty). | 200 or clear 4xx; record the interpretation (not documented). | Investigate | Low | Exploratory |
| RB-PARAM-011 | 05.11 | An undocumented query parameter is ignored or rejected, never misinterpreted. | Practice booking you created in `booking_id`. | Query `bookingid={{booking_id}}`. | Parameter ignored (full list) or 4xx; never misinterpreted (not documented). | Investigate | Medium | Exploratory |
| RB-PARAM-012 | 05.12 | Understand what a request with a missing path parameter actually addresses. | Environment selected. | URL `{{base_url}}/booking/` (trailing slash, no ID). | Record which resource answers (404 or list); never 5xx (not documented). | Investigate | High | Exploratory |
| RB-PARAM-013 | 05.13 | A malformed booking ID is rejected and doesn't return a booking. | Practice booking you created in `booking_id`. | Path `id` = `{{booking_id}}abc`. | 404/400 expected; no booking returned (not documented). | Investigate | Medium | Negative |

## 06 - JSON and Request Body

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-JSON-001 | 06.01 | A body with correct JSON types for every field is accepted and echoed with the same types. | Environment selected. | firstname `Neha` (string), lastname `Joshi` (string), totalprice `2750` (number), depositpaid `false` (boolean), bookingdates (object with two date strings), additionalneeds `Vegetarian meals` (string). | 200 OK; values and JSON types echoed unchanged (documented). | Documented | High | Positive |
| RB-JSON-002 | 06.02 | A POST without a documented-required field is rejected. | Environment selected. | All fields except `additionalneeds`; lastname `RB-JSON-002` as a marker. | Rejected (4xx) because additionalneeds is documented as required. | Partly documented | High | Negative |
| RB-JSON-003 | 06.03 | Find out how the API treats null for a String field. | Environment selected. | `"additionalneeds": null`; lastname `RB-JSON-003`. | Clear 4xx or consistent null handling (not documented). | Investigate | Medium | Exploratory |
| RB-JSON-004 | 06.04 | A non-numeric totalprice is rejected. | Environment selected. | `"totalprice": "four thousand five hundred"`; lastname `RB-JSON-004`. | 400 expected; no booking created (type documented, error not). | Partly documented | High | Negative |
| RB-JSON-005 | 06.05 | A string where a Boolean is expected is rejected, or at least interpreted correctly. | Environment selected. | `"depositpaid": "false"`; lastname `RB-JSON-005`. | 400 expected, or false preserved; never inverted to true. | Partly documented | High | Negative |
| RB-JSON-006 | 06.06 | A body with the wrong structure for a nested object is rejected. | Environment selected. | `"bookingdates": "2027-04-05 to 2027-04-08"`; lastname `RB-JSON-006`. | 400 expected; no booking created. | Partly documented | Medium | Negative |
| RB-JSON-007 | 06.07 | An array body is rejected by an endpoint that expects one object. | Environment selected. | Body: `[ { ...booking... } ]`; lastname `RB-JSON-007`. | 400 expected; no booking created. | Investigate | Medium | Negative |
| RB-JSON-008 | 06.08 | Syntactically invalid JSON is rejected with a client error. | Environment selected. | Valid booking data with a trailing comma after `"additionalneeds": "Breakfast"`. | 400 Bad Request expected by convention. | Investigate | High | Negative |

## 07 - Authentication

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-AUTH-001 | 07.01 | Valid credentials return a token. | Environment selected. `username` and `password` are set in the environment. | Body: `username` = `{{username}}` (admin), `password` = `{{password}}` (password123). | 200 OK; non-empty token string (documented). | Documented | High | Positive |
| RB-AUTH-002 | 07.02 | A wrong password doesn't produce a token and is reported as an authentication failure. | Environment selected. | `username` = `{{username}}`, `password` = `wrongPassword`. | No token; 401 expected by convention (not documented). | Investigate | High | Negative |
| RB-AUTH-003 | 07.03 | An unknown username doesn't produce a token. | Environment selected. | `username` = `administrator`, `password` = `{{password}}`. | No token; 401 expected; generic message (not documented). | Investigate | Medium | Negative |
| RB-AUTH-004 | 07.04 | A token request without credentials is rejected. | Environment selected. | Body `{}`. | No token; 400/401 expected (not documented). | Investigate | High | Negative |
| RB-AUTH-005 | 07.05 | A token request without a password is rejected. | Environment selected. | Body `{"username": "{{username}}"}`. | No token; 400/401 expected (not documented). | Investigate | Medium | Negative |

## 08 - Authorization

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-AUTHZ-001 | 08.01 | A request with a valid token is authorized. | Practice booking you created in `booking_id`. Fresh `token` (07.01/18.02). | Header `Cookie: token={{token}}`; body `{"additionalneeds": "Authorization check - valid token"}`. | 200 OK; update applied (documented). | Documented | High | Positive |
| RB-AUTHZ-002 | 08.02 | A request with valid Basic Auth credentials is authorized. | Practice booking you created in `booking_id`. | Authorization tab: Basic Auth `{{username}}` / `{{password}}`. | 200 OK; update applied (documented). | Documented | High | Positive |
| RB-AUTHZ-003 | 08.03 | An update without credentials is rejected and doesn't change data. | Practice booking you created in `booking_id`. | No Cookie header; Authorization = No Auth. | Rejected (401/403); booking unchanged (not documented). | Investigate | High | Negative |
| RB-AUTHZ-004 | 08.04 | An invalid token is rejected. | Practice booking you created in `booking_id`. | Header `Cookie: token=invalid-token-000`. | Rejected (403/401); booking unchanged (not documented). | Investigate | High | Negative |
| RB-AUTHZ-005 | 08.05 | A malformed Cookie header is rejected even when the token value itself is valid. | Practice booking you created in `booking_id`. Fresh `token` (07.01/18.02). | Header `Cookie: {{token}}` (missing `token=`). | Rejected (401/403); booking unchanged (not documented). | Investigate | Medium | Negative |
| RB-AUTHZ-006 | 08.06 | A malformed Authorization header doesn't grant access. | Practice booking you created in `booking_id`. Fresh `token` (07.01/18.02). | Header `Authorization: {{token}}`. | Rejected (401/403); booking unchanged (not documented). | Investigate | Medium | Negative |
| RB-AUTHZ-007 | 08.07 | An unauthenticated DELETE is rejected and the booking survives. | Practice booking you created in `booking_id`. | No Cookie, Authorization = No Auth. | Rejected (401/403); booking still exists (credentials required by docs). | Partly documented | High | Negative |

## 09 - API Contracts and Response Validation

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-CON-001 | 09.01 | The booking ID list matches the documented structure. | Fresh practice booking with standard data in `booking_id` (18.01). | Query `lastname=Verma`. | 200 OK; array of {bookingid:number}; JSON Content-Type (documented). | Partly documented | High | Positive |
| RB-CON-002 | 09.02 | A single booking response matches the documented contract. | Fresh practice booking with standard data in `booking_id` (18.01). | Path `id` = `{{booking_id}}`; no explicit Accept header (Postman sends `Accept: */*`). | 200 OK; all documented fields with correct types and YYYY-MM-DD dates. | Partly documented | High | Positive |
| RB-CON-003 | 09.03 | The create response matches the documented wrapper contract and echoes the request exactly. | Environment selected. | Vikram Singh, 6200, true, 2027-05-10 → 2027-05-14, `Twin beds`. | 200 OK; {bookingid:number, booking:{...}} echoing request (documented). | Partly documented | High | Positive |
| RB-CON-004 | 09.04 | The booking representation is identical across GET and PATCH, and an empty partial update changes nothing. | Fresh practice booking with standard data in `booking_id` (18.01). | Body `{}`; Basic Auth. | 200 OK; unchanged booking identical to GET. | Partly documented | Medium | Positive |

## 10 - Positive Testing

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-POS-001 | 10.01 | Successful authentication returns a non-empty token every time. | Environment selected. | Body: `{{username}}` / `{{password}}`. | 200 OK; non-empty token on every login (documented). | Documented | High | Positive |
| RB-POS-002 | 10.02 | A valid combination of documented filters returns your booking. | Fresh practice booking with standard data in `booking_id` (18.01). | Query `firstname=Asha&lastname=Verma&checkin=2027-01-14`. | 200 OK; your booking_id included (documented). | Documented | Medium | Positive |
| RB-POS-003 | 10.03 | Any existing booking can be retrieved and matches the documented contract. | Environment selected. | Path `id` = any ID currently listed by 01.01, other than yours. | 200 OK; contract-compliant booking (documented). | Documented | Medium | Positive |
| RB-POS-004 | 10.04 | Valid special characters are stored and returned unchanged. | Environment selected. | firstname `Anne-Marie`, lastname `O'Brien`, totalprice `3999`, additionalneeds `Wheelchair access; ground-floor room, please!`. | 200 OK; special characters echoed unchanged (documented). | Documented | Medium | Positive |
| RB-POS-005 | 10.05 | A full update authorized by a valid token succeeds. | Fresh practice booking with standard data in `booking_id` (18.01). Fresh `token` (07.01/18.02). | Cookie `token={{token}}`; body: Asha Verma, `4800`, `false`, 2027-01-15 → 2027-01-20, `Breakfast and dinner`. | 200 OK; booking replaced (documented). | Documented | High | Positive |
| RB-POS-006 | 10.06 | A partial update of several fields, including a complete nested object, succeeds and preserves the other fields. | Practice booking you created in `booking_id`. Fresh `token` (07.01/18.02). Ideally run 10.05 first. | Body: `bookingdates` = {checkin `2027-01-15`, checkout `2027-01-22`}, additionalneeds `Extended stay`. | 200 OK; supplied fields changed, others preserved (documented). | Documented | Medium | Positive |
| RB-POS-007 | 10.07 | A delete authorized by a valid token succeeds. | Environment selected. 10.04 executed and its ID noted. Fresh `token` (07.01/18.02). | Path `id` = the ID from 10.04; Cookie `token={{token}}`. | 201 Created (documented). | Documented | High | Positive |

## 11 - Negative Testing

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-NEG-001 | 11.01 | A non-numeric booking ID is rejected. | Environment selected. | Path `id` = `abc`. | 404/400 expected; no data or internals leaked (not documented). | Investigate | High | Negative |
| RB-NEG-002 | 11.02 | Updating a non-existent booking reports 'not found' and creates nothing. | Environment selected. | Path `id` = `999999999`; Basic Auth; body `{"firstname": "Ghost"}`. | 404 expected (consistent with GET); nothing created (not documented). | Investigate | High | Negative |
| RB-NEG-003 | 11.03 | A username that differs only in letter case doesn't authenticate. | Environment selected. | `username` = `ADMIN`, `password` = `{{password}}`. | No token; 401 expected (not documented). | Investigate | Medium | Negative |
| RB-NEG-004 | 11.04 | A booking without required name fields is rejected. | Environment selected. | All fields except `firstname` and `lastname`. | 400 expected; nothing created (fields documented as required). | Partly documented | High | Negative |
| RB-NEG-005 | 11.05 | A numeric firstname is rejected with a client error. | Environment selected. | `"firstname": 12345` (number, no quotes); lastname `RB-NEG-005`. | 400 expected; nothing created. | Partly documented | High | Negative |
| RB-NEG-006 | 11.06 | A truncated JSON body is rejected and the booking is unchanged. | Practice booking you created in `booking_id`. | Standard practice data without the closing brace; Basic Auth. | 400 expected; booking unchanged. | Investigate | High | Negative |
| RB-NEG-007 | 11.07 | A token passed in the URL isn't accepted as authentication. | Practice booking you created in `booking_id`. Fresh `token` (07.01/18.02). | URL `...?token={{token}}`; no Cookie; Authorization = No Auth; valid body. | Rejected (401/403); booking unchanged (not documented). | Investigate | Medium | Negative |
| RB-NEG-008 | 11.08 | A body that doesn't match its declared Content-Type is rejected. | Environment selected. | Header `Content-Type: application/xml`; JSON body with lastname `RB-NEG-008`. | 400/415 expected; nothing created (not documented). | Investigate | Medium | Negative |
| RB-NEG-009 | 11.09 | An unsupported method on an existing resource is rejected and changes nothing. | Practice booking you created in `booking_id`. | POST `{{base_url}}/booking/{{booking_id}}` with a valid body. | 405 expected by convention; nothing changed (not documented). | Investigate | Medium | Negative |
| RB-NEG-010 | 11.10 | A non-existent endpoint returns 'not found'. | Environment selected. | URL `{{base_url}}/bookings`. | 404 Not Found expected. | Investigate | Low | Negative |

## 12 - Boundary Testing

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-BND-001 | 12.01 | Discover whether a zero price is accepted and stored exactly. | Environment selected. | `"totalprice": 0`; lastname `RB-BND-001`. | Accepted with 0 or clear 4xx; record (no documented minimum). | Investigate | Medium | Boundary |
| RB-BND-002 | 12.02 | A negative price should be rejected (business plausibility). | Environment selected. | `"totalprice": -1`; lastname `RB-BND-002`. | Rejected (4xx) expected on business grounds; not documented. | Investigate | High | Boundary |
| RB-BND-003 | 12.03 | A decimal price is stored exactly or rejected, never silently changed. | Environment selected. | `"totalprice": 4500.99`; lastname `RB-BND-003`. | Stored exactly (4500.99) or clear 4xx; never silently changed. | Partly documented | High | Boundary |
| RB-BND-004 | 12.04 | An extreme number is stored exactly or rejected, never corrupted. | Environment selected. | `"totalprice": 1000000000000000000000`; lastname `RB-BND-004`. | Exact value or clear 4xx; never corrupted (no documented max). | Investigate | Medium | Boundary |
| RB-BND-005 | 12.05 | A booking with an empty guest name is rejected. | Environment selected. | `"firstname": ""`; lastname `RB-BND-005`. | Rejected (4xx) expected; empty name shouldn't be stored. | Partly documented | High | Boundary |
| RB-BND-006 | 12.06 | Discover whether long names are stored exactly or rejected cleanly. | Environment selected. | `firstname` = 256 × `A`; lastname `RB-BND-006`. | Exact value or clear 4xx; never truncated (no documented max). | Investigate | Medium | Boundary |
| RB-BND-007 | 12.07 | A booking with a reversed date range is rejected. | Environment selected. | checkin `2027-07-10`, checkout `2027-07-05`; lastname `RB-BND-007`. | Rejected (4xx) expected on business grounds; not documented. | Investigate | High | Boundary |
| RB-BND-008 | 12.08 | A non-existent calendar date is rejected, not silently changed. | Environment selected. | checkin `2027-02-29`; lastname `RB-BND-008`. | Rejected (4xx) expected; never silently rolled to another date. | Partly documented | Medium | Boundary |
| RB-BND-009 | 12.09 | A booking whose check-in equals the filter date is included. | Practice booking you created in `booking_id`. Your practice booking checks in on **2027-01-15** (standard data; 10.05/10.06 keep that date). | Query `checkin=2027-01-15`. | 200 OK; your booking included (>= is documented). | Documented | High | Boundary |
| RB-BND-010 | 12.10 | ID 0 is reported as not found. | Environment selected. | Path `id` = `0`. | 404 expected (not documented). | Investigate | Medium | Boundary |
| RB-BND-011 | 12.11 | An oversized ID is handled as 'not found' or 'bad request', never a crash. | Environment selected. | Path `id` = `99999999999999999999`. | 404/400 expected; never 5xx. | Investigate | Medium | Boundary |
| RB-BND-012 | 12.12 | An empty value for the 'additional needs' free-text field is handled consistently. | Environment selected. | `"additionalneeds": ""`; lastname `RB-BND-012`. | Echoed as "" or clear 4xx (not documented). | Investigate | Low | Boundary |

## 13 - Business Validation

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-BIZ-001 | 13.01 | Create a baseline booking and record its ID. | Environment selected. | Meera Pillai, totalprice `8900`, depositpaid `true`, 2027-08-12 → 2027-08-15, `Sea-view room`. | 200 OK; booking created (documented). | Documented | High | Setup |
| RB-BIZ-002 | 13.02 | The persisted booking equals the submitted data. | Environment selected. 13.01 done and `booking_id` saved. | Path `id` = `{{booking_id}}`. | 200 OK; stored = submitted (documented). | Documented | High | Verification |
| RB-BIZ-003 | 13.03 | A full update changes exactly the intended fields. | Environment selected. 13.01 done. | Changed: lastname `Pillai-Nair`, totalprice `9400`, checkout `2027-08-16`, additionalneeds `Sea-view room and breakfast`. Unchanged: firstname, depositpaid, checkin. | 200 OK; stored state equals PUT body (documented). | Documented | High | Positive |
| RB-BIZ-004 | 13.04 | A partial update preserves unrelated fields. | Environment selected. 13.03 done. | Body `{"totalprice": 9900}`. | 200 OK; only totalprice changes (documented). | Documented | High | Positive |
| RB-BIZ-005 | 13.05 | Updating one nested field preserves its sibling field. | Environment selected. 13.04 done (checkout is 2027-08-16). | Body `{"bookingdates": {"checkin": "2027-08-13"}}`. | 200 OK; checkin changes, checkout preserved (documented field list). | Partly documented | High | Positive |
| RB-BIZ-006 | 13.06 | PUT either rejects the missing field or replaces the booking completely (dropping additionalneeds). It must not silently keep the old value. | Environment selected. 13.05 done. | All fields except `additionalneeds`; dates 2027-08-13 → 2027-08-16. | 4xx, or 200 with additionalneeds removed; never silently kept. | Partly documented | High | Negative |
| RB-BIZ-007 | 13.07 | A booking can be deleted. | Environment selected. 13.01-13.06 done. | Path `id` = `{{booking_id}}`; Basic Auth. | 201 Created (documented). | Documented | High | Positive |
| RB-BIZ-008 | 13.08 | A deleted booking can't be retrieved. | Environment selected. 13.07 returned success. | Path `id` = `{{booking_id}}` (deleted). | 404 expected; booking not returned. | Investigate | High | Verification |
| RB-BIZ-009 | 13.09 | A deleted booking doesn't appear in search results. | Environment selected. 13.07 done. | Query `firstname=Meera&lastname=Pillai-Nair`. | 200 OK; deleted ID absent. | Partly documented | Medium | Verification |

## 14 - Test Case Design

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-TCD-001 | 14.01 | An invalid state transition (update after delete) is refused. | Environment selected. `booking_id` holds a booking **you deleted** (the state after folder 13). | Path `id` = deleted booking; Basic Auth; body `{"additionalneeds": "Should not be applied"}`. | 404/410 expected; booking stays deleted (not documented). | Investigate | High | Negative |
| RB-TCD-002 | 14.02 | Discover the rule the API applies when one credential is valid and the other isn't. | Practice booking you created in `booking_id`. | Cookie `token=invalid-token-000`; Basic Auth `{{username}}`/`{{password}}`. | Discover and record the rule (allow or deny); not documented. | Investigate | Medium | Exploratory |
| RB-TCD-003 | 14.03 | Complete the decision table: valid token plus invalid Basic Auth. | Practice booking you created in `booking_id`. Fresh `token` (07.01/18.02). | Cookie `token={{token}}`; Basic Auth `{{username}}` / `wrong-password`. | Consistent with R5 (14.02); record (not documented). | Investigate | Medium | Exploratory |
| RB-TCD-004 | 14.04 | A numeric value for a Boolean field is rejected, or interpreted without changing its meaning. | Environment selected. | `"depositpaid": 0`; lastname `RB-TCD-004`. | 4xx, or false preserved (type documented, coercion not). | Partly documented | Medium | Negative |

## 15 - API Chaining

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-CHAIN-001 | 15.01 | Create a booking and store its ID for the following requests. | Environment selected. | Farhan Ali, 5100, true, 2027-10-01 → 2027-10-04, `Late check-in`. | 200 OK; bookingid returned and stored manually. | Documented | High | Positive |
| RB-CHAIN-002 | 15.02 | The stored booking ID retrieves exactly the booking created in 15.01. | Environment selected. 15.01 done and `booking_id` saved. | Path `id` = `{{booking_id}}`. | 200 OK; booking from 15.01 returned. | Documented | High | Verification |
| RB-CHAIN-003 | 15.03 | Obtain a token and store it for authorized requests. | Environment selected. | `{{username}}` / `{{password}}`. | 200 OK; token returned and stored manually. | Documented | High | Positive |
| RB-CHAIN-004 | 15.04 | A request built from two chained values succeeds. | Environment selected. 15.01 and 15.03 done. | Path `{{booking_id}}`; Cookie `token={{token}}`; body `{"additionalneeds": "Late check-in and airport transfer"}`. | 200 OK; update applied using both chained values. | Documented | High | Positive |
| RB-CHAIN-005 | 15.05 | Recognise an unresolved variable and its effect on the request. | Environment selected. | Path `id` = `{{bookingId}}` (typo). | 4xx (404) and the unresolved variable identified. | Investigate | Medium | Negative |

## 16 - CRUD Workflow

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-CRUD-001 | 16.01 | Create a booking and store its ID. | Environment selected. | Kavya Menon, 7300, true, 2027-11-20 → 2027-11-23, `Extra pillows`. | 200 OK; bookingid returned and saved. | Documented | High | Positive |
| RB-CRUD-002 | 16.02 | The created booking matches the submitted data. | Environment selected. Previous CRUD steps done; `booking_id` from 16.01. | Path `id` = `{{booking_id}}`. | 200 OK; equals 16.01 body. | Documented | High | Verification |
| RB-CRUD-003 | 16.03 | A full update replaces all fields. | Environment selected. 16.01 done. | Kavya Menon-Iyer, 7600, false, 2027-11-21 → 2027-11-24, `Extra pillows and breakfast`. | 200 OK; all fields replaced. | Documented | High | Positive |
| RB-CRUD-004 | 16.04 | The stored booking equals the PUT body (the update was persisted). | Environment selected. Previous CRUD steps done; `booking_id` from 16.01. | Path `id` = `{{booking_id}}`. | 200 OK; equals 16.03 body. | Documented | High | Verification |
| RB-CRUD-005 | 16.05 | A partial update changes only the supplied fields. | Environment selected. 16.03 done. | Body `{"totalprice": 7900, "depositpaid": true}`. | 200 OK; only totalprice and depositpaid change. | Documented | High | Positive |
| RB-CRUD-006 | 16.06 | After the partial update, changed fields are updated and all other fields are preserved. | Environment selected. Previous CRUD steps done; `booking_id` from 16.01. | Path `id` = `{{booking_id}}`. | 200 OK; changed + preserved fields correct. | Documented | High | Verification |
| RB-CRUD-007 | 16.07 | The booking can be deleted. | Environment selected. 16.01-16.06 done. | Path `{{booking_id}}`; Basic Auth. | 201 Created. | Documented | High | Positive |
| RB-CRUD-008 | 16.08 | The deleted booking can no longer be retrieved. | Environment selected. Previous CRUD steps done; `booking_id` from 16.01. | Path `id` = `{{booking_id}}`. | 404 expected; no data. | Investigate | High | Verification |
| RB-CRUD-009 | 16.09 | The deleted booking is absent from search results. | Environment selected. 16.07 done. | Query `firstname=Kavya&lastname=Menon-Iyer`. | 200 OK; deleted ID absent. | Documented | Medium | Verification |

## 17 - End-to-End Booking Flow

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-E2E-001 | 17.01 | The API is available before the flow starts. | Environment selected. | None. | 201 Created. | Documented | High | Positive |
| RB-E2E-002 | 17.02 | Obtain a token for the journey. | Environment selected. | `{{username}}` / `{{password}}`. | 200 OK; token saved. | Documented | High | Positive |
| RB-E2E-003 | 17.03 | Create the guest's booking. | Environment selected. | Daniel Fernandes, 12500, true, 2027-12-22 → 2027-12-27, `Late checkout on departure day`. | 200 OK; bookingid saved. | Documented | High | Positive |
| RB-E2E-004 | 17.04 | The stored booking matches the guest's request in every field. | Environment selected. 17.03 done. | Path `{{booking_id}}`. | 200 OK; all fields equal the submitted data. | Documented | High | Verification |
| RB-E2E-005 | 17.05 | Update the booking with the token. | Environment selected. 17.02 and 17.03 done. | checkout `2027-12-29`, totalprice `14200`, additionalneeds `Late checkout and airport transfer`; other fields unchanged. | 200 OK; booking updated. | Documented | High | Positive |
| RB-E2E-006 | 17.06 | The stored booking reflects the update. | Environment selected. 17.05 done. | Path `{{booking_id}}`. | 200 OK; equals 17.05 body. | Documented | High | Verification |
| RB-E2E-007 | 17.07 | Partially update the booking with the token. | Environment selected. 17.05 done. | Body `{"additionalneeds": "Late checkout, airport transfer and vegetarian meals"}`. | 200 OK; only additionalneeds changes. | Documented | High | Positive |
| RB-E2E-008 | 17.08 | The partial update changed only additionalneeds. | Environment selected. 17.07 done. | Path `{{booking_id}}`. | 200 OK; changed and preserved fields correct. | Documented | High | Verification |
| RB-E2E-009 | 17.09 | Delete the booking with the token. | Environment selected. 17.08 done. | Path `{{booking_id}}`; Cookie `token={{token}}`. | 201 Created. | Documented | High | Positive |
| RB-E2E-010 | 17.10 | The cancelled booking is gone. | Environment selected. 17.09 done. | Path `{{booking_id}}` (deleted). | 404 expected; booking gone. | Investigate | High | Verification |

## 18 - Cleanup and Reusable Requests

| ID | Request | Scenario | Preconditions | Test data | Expected result | Basis | Priority | Type |
|---|---|---|---|---|---|---|---|---|
| RB-UTIL-001 | 18.01 | Set up a known practice booking. | Environment selected. | Asha Verma, 4500, true, 2027-01-15 → 2027-01-20, `Breakfast`. | 200 OK; practice booking created and ID saved. | Documented | High | Setup |
| RB-UTIL-002 | 18.02 | Set up a valid token. | Environment selected. | `{{username}}` / `{{password}}`. | 200 OK; token saved. | Documented | High | Setup |
| RB-UTIL-003 | 18.03 | Remove test data you created. | Environment selected. `booking_id` holds a booking you created. | Path `{{booking_id}}`; Basic Auth. | 201 Created. | Documented | Medium | Setup |
| RB-UTIL-004 | 18.04 | Verify cleanup and leave the environment clean. | Environment selected. 18.03 (or 16.07 / 17.09) done. | Path `{{booking_id}}`. | 404 expected; booking_id and token cleared. | Investigate | Medium | Verification |

---

_Expected results come from the official documentation where it exists. Everything else is marked **Investigate** and must be confirmed by executing the test. Record actual results in `Test-Execution-Report-Template.md`._
