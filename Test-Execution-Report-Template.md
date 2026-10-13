# Test Execution Report - Restful Booker Manual API Testing

> **How to use this template:** make a copy for each test run (for example `reports/2026-10-12-run-01.md`), fill in the run information, then record every test you execute. Keep this original file blank so you can reuse it.

## 1. Run information

| Field | Value |
|---|---|
| Project | Restful Booker - Manual API Testing Practice |
| Test run ID |  |
| Tester |  |
| Execution start (date and time, with time zone) |  |
| Execution end |  |
| Environment (Public: https://restful-booker.herokuapp.com / Local / Other) |  |
| Postman version |  |
| Collection version / Git commit |  |
| Test scope (folders executed) |  |
| Notes (API resets, outages, network issues) |  |

## 2. Summary

| Total test cases | Executed | Pass | Fail | Blocked | Not run | Pass rate (Pass / Executed) |
|---|---|---|---|---|---|---|
| 129 |  |  |  |  |  |  |

## 3. Status definitions

- **Pass:** the actual result meets the expected result and the *Mark as Pass if* criteria in the request's Docs tab.
- **Fail:** the actual result deviates from the expected result. Log a defect (section 5), or an observation/question (section 6) when the expectation is *Investigate* and the behaviour is debatable.
- **Blocked:** the test couldn't be executed or judged (API down, precondition can't be met, data reset mid-test). Explain why in *Remarks*.
- **Not run:** leave *Pass/Fail/Blocked* empty and write `Not run` in *Remarks*.

**Actual Result:** always start with the status code and text (for example `418 I'm a Teapot`), then summarise the body and anything notable (for example `booking created anyway, ID 57`). Attach screenshots or Console output as evidence when you raise a defect.

## 4. Test execution log

| Test Case ID | Scenario | Execution Date | Environment | Expected Result | Actual Result | Pass/Fail/Blocked | Defect ID | Remarks |
|---|---|---|---|---|---|---|---|---|
| RB-HC-001 | 00.01 Verify that the Restful Booker API is up and responding. |  |  | 201 Created (documented); plain-text body. |  |  |  |  |
| RB-FUND-001 | 01.01 Retrieve the list of booking IDs and identify every part of the request and the response. |  |  | 200 OK; JSON array of {bookingid} objects (documented). |  |  |  |  |
| RB-FUND-002 | 01.02 Create a booking with valid data and save its ID for later requests. |  |  | 200 OK; numeric bookingid; booking object echoes the request (documented). |  |  |  |  |
| RB-FUND-003 | 01.03 Send an authenticated partial update and inspect the complete HTTP request and response. |  |  | 200 OK; only additionalneeds changed (documented). |  |  |  |  |
| RB-GET-001 | 02.01 Retrieve an existing booking and confirm that repeated GETs return identical data. |  |  | 200 OK; booking JSON; identical on repeat (documented). |  |  |  |  |
| RB-POST-001 | 02.02 Send the same POST twice and confirm that two separate bookings are created. |  |  | 200 OK on each send; two different bookingids. |  |  |  |  |
| RB-PUT-001 | 02.03 Update all fields of an existing booking with PUT. |  |  | 200 OK; every field replaced (documented). |  |  |  |  |
| RB-PATCH-001 | 02.04 Update one field with PATCH and confirm the other fields are untouched. |  |  | 200 OK; only totalprice changes (documented). |  |  |  |  |
| RB-PUT-002 | 02.05 A PUT with an incomplete body must not be accepted as a full update. |  |  | Rejected with 4xx (likely 400); booking unchanged. Error code not documented. |  |  |  |  |
| RB-DEL-001 | 02.06 Delete an existing booking that you created. |  |  | 201 Created (documented); booking removed. |  |  |  |  |
| RB-DEL-002 | 02.07 A deleted booking must no longer be retrievable. |  |  | Booking not returned; 404 expected by convention (not documented). |  |  |  |  |
| RB-STAT-001 | 03.01 Retrieving a non-existent booking returns a 'not found' client error. |  |  | 404 Not Found expected by convention (not documented). |  |  |  |  |
| RB-STAT-002 | 03.02 Deleting a non-existent booking returns a 'not found' client error consistent with GET. |  |  | 404 expected by convention, consistent with GET (not documented). |  |  |  |  |
| RB-STAT-003 | 03.03 An update without credentials is rejected and doesn't change the booking. |  |  | Rejected with 401/403; booking unchanged (error code not documented). |  |  |  |  |
| RB-STAT-004 | 03.04 A malformed JSON body is rejected with a client error. |  |  | 400 Bad Request expected by convention; booking unchanged. |  |  |  |  |
| RB-STAT-005 | 03.05 Creating a booking without any required field is rejected with a client error. |  |  | Rejected with 4xx (likely 400); no booking created. Error code not documented. |  |  |  |  |
| RB-HDR-001 | 04.01 Retrieve a booking in the documented alternative format (XML). |  |  | 200 OK with an XML body and the same values (documented); an XML Content-Type is expected by convention. |  |  |  |  |
| RB-HDR-002 | 04.02 Retrieve a booking when the client doesn't send an Accept header. |  |  | 200 with JSON (default) or a clear 400/406; behaviour without Accept not documented. |  |  |  |  |
| RB-HDR-003 | 04.03 A request whose Content-Type doesn't match its body is rejected with a client error. |  |  | 415/400 expected by convention; no booking created (not documented). |  |  |  |  |
| RB-HDR-004 | 04.04 A request with a body but no Content-Type is handled with a clear client error. |  |  | Clear 4xx (415/400) or correct handling; never 5xx (not documented). |  |  |  |  |
| RB-HDR-005 | 04.05 If the server rejects a create request because of an unsupported Accept value, it must not create the booking. |  |  | 406 expected by convention and no booking created (not documented). |  |  |  |  |
| RB-HDR-006 | 04.06 A request that returned an error must leave no booking behind. |  |  | 200 OK and [] if 04.05 had no side effect. |  |  |  |  |
| RB-PARAM-001 | 05.01 Filtering by firstname returns your booking's ID. |  |  | 200 OK; array contains your booking_id (documented). |  |  |  |  |
| RB-PARAM-002 | 05.02 Filtering by lastname returns your booking's ID. |  |  | 200 OK; array contains your booking_id (documented). |  |  |  |  |
| RB-PARAM-003 | 05.03 Combining firstname and lastname returns only bookings matching both, including yours. |  |  | 200 OK; your booking_id present; AND semantics (documented example). |  |  |  |  |
| RB-PARAM-004 | 05.04 A checkin filter earlier than your check-in date returns your booking. |  |  | 200 OK; your booking included (check-in 2027-01-15 >= 2027-01-14) (documented). |  |  |  |  |
| RB-PARAM-005 | 05.05 A checkout filter earlier than your check-out date returns your booking (documented: check-out >= filter date). |  |  | 200 OK; your booking included (check-out 2027-01-20 >= 2027-01-19) (documented). |  |  |  |  |
| RB-PARAM-006 | 05.06 Combined date filters that both match your booking return its ID. |  |  | 200 OK; your booking included (documented). |  |  |  |  |
| RB-PARAM-007 | 05.07 A search with no matches returns an empty list, not an error. |  |  | 200 OK with [] expected by convention (not documented). |  |  |  |  |
| RB-PARAM-008 | 05.08 Find out whether the firstname filter is case-sensitive. |  |  | 200 OK; record whether matching is case-sensitive (not documented). |  |  |  |  |
| RB-PARAM-009 | 05.09 A date filter in the wrong format is rejected with a clear client error. |  |  | 400 expected by convention; never 5xx (format documented, error not). |  |  |  |  |
| RB-PARAM-010 | 05.10 Discover how the API treats an empty filter value. |  |  | 200 or clear 4xx; record the interpretation (not documented). |  |  |  |  |
| RB-PARAM-011 | 05.11 An undocumented query parameter is ignored or rejected, never misinterpreted. |  |  | Parameter ignored (full list) or 4xx; never misinterpreted (not documented). |  |  |  |  |
| RB-PARAM-012 | 05.12 Understand what a request with a missing path parameter actually addresses. |  |  | Record which resource answers (404 or list); never 5xx (not documented). |  |  |  |  |
| RB-PARAM-013 | 05.13 A malformed booking ID is rejected and doesn't return a booking. |  |  | 404/400 expected; no booking returned (not documented). |  |  |  |  |
| RB-JSON-001 | 06.01 A body with correct JSON types for every field is accepted and echoed with the same types. |  |  | 200 OK; values and JSON types echoed unchanged (documented). |  |  |  |  |
| RB-JSON-002 | 06.02 A POST without a documented-required field is rejected. |  |  | Rejected (4xx) because additionalneeds is documented as required. |  |  |  |  |
| RB-JSON-003 | 06.03 Find out how the API treats null for a String field. |  |  | Clear 4xx or consistent null handling (not documented). |  |  |  |  |
| RB-JSON-004 | 06.04 A non-numeric totalprice is rejected. |  |  | 400 expected; no booking created (type documented, error not). |  |  |  |  |
| RB-JSON-005 | 06.05 A string where a Boolean is expected is rejected, or at least interpreted correctly. |  |  | 400 expected, or false preserved; never inverted to true. |  |  |  |  |
| RB-JSON-006 | 06.06 A body with the wrong structure for a nested object is rejected. |  |  | 400 expected; no booking created. |  |  |  |  |
| RB-JSON-007 | 06.07 An array body is rejected by an endpoint that expects one object. |  |  | 400 expected; no booking created. |  |  |  |  |
| RB-JSON-008 | 06.08 Syntactically invalid JSON is rejected with a client error. |  |  | 400 Bad Request expected by convention. |  |  |  |  |
| RB-AUTH-001 | 07.01 Valid credentials return a token. |  |  | 200 OK; non-empty token string (documented). |  |  |  |  |
| RB-AUTH-002 | 07.02 A wrong password doesn't produce a token and is reported as an authentication failure. |  |  | No token; 401 expected by convention (not documented). |  |  |  |  |
| RB-AUTH-003 | 07.03 An unknown username doesn't produce a token. |  |  | No token; 401 expected; generic message (not documented). |  |  |  |  |
| RB-AUTH-004 | 07.04 A token request without credentials is rejected. |  |  | No token; 400/401 expected (not documented). |  |  |  |  |
| RB-AUTH-005 | 07.05 A token request without a password is rejected. |  |  | No token; 400/401 expected (not documented). |  |  |  |  |
| RB-AUTHZ-001 | 08.01 A request with a valid token is authorized. |  |  | 200 OK; update applied (documented). |  |  |  |  |
| RB-AUTHZ-002 | 08.02 A request with valid Basic Auth credentials is authorized. |  |  | 200 OK; update applied (documented). |  |  |  |  |
| RB-AUTHZ-003 | 08.03 An update without credentials is rejected and doesn't change data. |  |  | Rejected (401/403); booking unchanged (not documented). |  |  |  |  |
| RB-AUTHZ-004 | 08.04 An invalid token is rejected. |  |  | Rejected (403/401); booking unchanged (not documented). |  |  |  |  |
| RB-AUTHZ-005 | 08.05 A malformed Cookie header is rejected even when the token value itself is valid. |  |  | Rejected (401/403); booking unchanged (not documented). |  |  |  |  |
| RB-AUTHZ-006 | 08.06 A malformed Authorization header doesn't grant access. |  |  | Rejected (401/403); booking unchanged (not documented). |  |  |  |  |
| RB-AUTHZ-007 | 08.07 An unauthenticated DELETE is rejected and the booking survives. |  |  | Rejected (401/403); booking still exists (credentials required by docs). |  |  |  |  |
| RB-CON-001 | 09.01 The booking ID list matches the documented structure. |  |  | 200 OK; array of {bookingid:number}; JSON Content-Type (documented). |  |  |  |  |
| RB-CON-002 | 09.02 A single booking response matches the documented contract. |  |  | 200 OK; all documented fields with correct types and YYYY-MM-DD dates. |  |  |  |  |
| RB-CON-003 | 09.03 The create response matches the documented wrapper contract and echoes the request exactly. |  |  | 200 OK; {bookingid:number, booking:{...}} echoing request (documented). |  |  |  |  |
| RB-CON-004 | 09.04 The booking representation is identical across GET and PATCH, and an empty partial update changes nothing. |  |  | 200 OK; unchanged booking identical to GET. |  |  |  |  |
| RB-POS-001 | 10.01 Successful authentication returns a non-empty token every time. |  |  | 200 OK; non-empty token on every login (documented). |  |  |  |  |
| RB-POS-002 | 10.02 A valid combination of documented filters returns your booking. |  |  | 200 OK; your booking_id included (documented). |  |  |  |  |
| RB-POS-003 | 10.03 Any existing booking can be retrieved and matches the documented contract. |  |  | 200 OK; contract-compliant booking (documented). |  |  |  |  |
| RB-POS-004 | 10.04 Valid special characters are stored and returned unchanged. |  |  | 200 OK; special characters echoed unchanged (documented). |  |  |  |  |
| RB-POS-005 | 10.05 A full update authorized by a valid token succeeds. |  |  | 200 OK; booking replaced (documented). |  |  |  |  |
| RB-POS-006 | 10.06 A partial update of several fields, including a complete nested object, succeeds and preserves the other fields. |  |  | 200 OK; supplied fields changed, others preserved (documented). |  |  |  |  |
| RB-POS-007 | 10.07 A delete authorized by a valid token succeeds. |  |  | 201 Created (documented). |  |  |  |  |
| RB-NEG-001 | 11.01 A non-numeric booking ID is rejected. |  |  | 404/400 expected; no data or internals leaked (not documented). |  |  |  |  |
| RB-NEG-002 | 11.02 Updating a non-existent booking reports 'not found' and creates nothing. |  |  | 404 expected (consistent with GET); nothing created (not documented). |  |  |  |  |
| RB-NEG-003 | 11.03 A username that differs only in letter case doesn't authenticate. |  |  | No token; 401 expected (not documented). |  |  |  |  |
| RB-NEG-004 | 11.04 A booking without required name fields is rejected. |  |  | 400 expected; nothing created (fields documented as required). |  |  |  |  |
| RB-NEG-005 | 11.05 A numeric firstname is rejected with a client error. |  |  | 400 expected; nothing created. |  |  |  |  |
| RB-NEG-006 | 11.06 A truncated JSON body is rejected and the booking is unchanged. |  |  | 400 expected; booking unchanged. |  |  |  |  |
| RB-NEG-007 | 11.07 A token passed in the URL isn't accepted as authentication. |  |  | Rejected (401/403); booking unchanged (not documented). |  |  |  |  |
| RB-NEG-008 | 11.08 A body that doesn't match its declared Content-Type is rejected. |  |  | 400/415 expected; nothing created (not documented). |  |  |  |  |
| RB-NEG-009 | 11.09 An unsupported method on an existing resource is rejected and changes nothing. |  |  | 405 expected by convention; nothing changed (not documented). |  |  |  |  |
| RB-NEG-010 | 11.10 A non-existent endpoint returns 'not found'. |  |  | 404 Not Found expected. |  |  |  |  |
| RB-BND-001 | 12.01 Discover whether a zero price is accepted and stored exactly. |  |  | Accepted with 0 or clear 4xx; record (no documented minimum). |  |  |  |  |
| RB-BND-002 | 12.02 A negative price should be rejected (business plausibility). |  |  | Rejected (4xx) expected on business grounds; not documented. |  |  |  |  |
| RB-BND-003 | 12.03 A decimal price is stored exactly or rejected, never silently changed. |  |  | Stored exactly (4500.99) or clear 4xx; never silently changed. |  |  |  |  |
| RB-BND-004 | 12.04 An extreme number is stored exactly or rejected, never corrupted. |  |  | Exact value or clear 4xx; never corrupted (no documented max). |  |  |  |  |
| RB-BND-005 | 12.05 A booking with an empty guest name is rejected. |  |  | Rejected (4xx) expected; empty name shouldn't be stored. |  |  |  |  |
| RB-BND-006 | 12.06 Discover whether long names are stored exactly or rejected cleanly. |  |  | Exact value or clear 4xx; never truncated (no documented max). |  |  |  |  |
| RB-BND-007 | 12.07 A booking with a reversed date range is rejected. |  |  | Rejected (4xx) expected on business grounds; not documented. |  |  |  |  |
| RB-BND-008 | 12.08 A non-existent calendar date is rejected, not silently changed. |  |  | Rejected (4xx) expected; never silently rolled to another date. |  |  |  |  |
| RB-BND-009 | 12.09 A booking whose check-in equals the filter date is included. |  |  | 200 OK; your booking included (>= is documented). |  |  |  |  |
| RB-BND-010 | 12.10 ID 0 is reported as not found. |  |  | 404 expected (not documented). |  |  |  |  |
| RB-BND-011 | 12.11 An oversized ID is handled as 'not found' or 'bad request', never a crash. |  |  | 404/400 expected; never 5xx. |  |  |  |  |
| RB-BND-012 | 12.12 An empty value for the 'additional needs' free-text field is handled consistently. |  |  | Echoed as "" or clear 4xx (not documented). |  |  |  |  |
| RB-BIZ-001 | 13.01 Create a baseline booking and record its ID. |  |  | 200 OK; booking created (documented). |  |  |  |  |
| RB-BIZ-002 | 13.02 The persisted booking equals the submitted data. |  |  | 200 OK; stored = submitted (documented). |  |  |  |  |
| RB-BIZ-003 | 13.03 A full update changes exactly the intended fields. |  |  | 200 OK; stored state equals PUT body (documented). |  |  |  |  |
| RB-BIZ-004 | 13.04 A partial update preserves unrelated fields. |  |  | 200 OK; only totalprice changes (documented). |  |  |  |  |
| RB-BIZ-005 | 13.05 Updating one nested field preserves its sibling field. |  |  | 200 OK; checkin changes, checkout preserved (documented field list). |  |  |  |  |
| RB-BIZ-006 | 13.06 PUT either rejects the missing field or replaces the booking completely (dropping additionalneeds). It must not silently keep the old value. |  |  | 4xx, or 200 with additionalneeds removed; never silently kept. |  |  |  |  |
| RB-BIZ-007 | 13.07 A booking can be deleted. |  |  | 201 Created (documented). |  |  |  |  |
| RB-BIZ-008 | 13.08 A deleted booking can't be retrieved. |  |  | 404 expected; booking not returned. |  |  |  |  |
| RB-BIZ-009 | 13.09 A deleted booking doesn't appear in search results. |  |  | 200 OK; deleted ID absent. |  |  |  |  |
| RB-TCD-001 | 14.01 An invalid state transition (update after delete) is refused. |  |  | 404/410 expected; booking stays deleted (not documented). |  |  |  |  |
| RB-TCD-002 | 14.02 Discover the rule the API applies when one credential is valid and the other isn't. |  |  | Discover and record the rule (allow or deny); not documented. |  |  |  |  |
| RB-TCD-003 | 14.03 Complete the decision table: valid token plus invalid Basic Auth. |  |  | Consistent with R5 (14.02); record (not documented). |  |  |  |  |
| RB-TCD-004 | 14.04 A numeric value for a Boolean field is rejected, or interpreted without changing its meaning. |  |  | 4xx, or false preserved (type documented, coercion not). |  |  |  |  |
| RB-CHAIN-001 | 15.01 Create a booking and store its ID for the following requests. |  |  | 200 OK; bookingid returned and stored manually. |  |  |  |  |
| RB-CHAIN-002 | 15.02 The stored booking ID retrieves exactly the booking created in 15.01. |  |  | 200 OK; booking from 15.01 returned. |  |  |  |  |
| RB-CHAIN-003 | 15.03 Obtain a token and store it for authorized requests. |  |  | 200 OK; token returned and stored manually. |  |  |  |  |
| RB-CHAIN-004 | 15.04 A request built from two chained values succeeds. |  |  | 200 OK; update applied using both chained values. |  |  |  |  |
| RB-CHAIN-005 | 15.05 Recognise an unresolved variable and its effect on the request. |  |  | 4xx (404) and the unresolved variable identified. |  |  |  |  |
| RB-CRUD-001 | 16.01 Create a booking and store its ID. |  |  | 200 OK; bookingid returned and saved. |  |  |  |  |
| RB-CRUD-002 | 16.02 The created booking matches the submitted data. |  |  | 200 OK; equals 16.01 body. |  |  |  |  |
| RB-CRUD-003 | 16.03 A full update replaces all fields. |  |  | 200 OK; all fields replaced. |  |  |  |  |
| RB-CRUD-004 | 16.04 The stored booking equals the PUT body (the update was persisted). |  |  | 200 OK; equals 16.03 body. |  |  |  |  |
| RB-CRUD-005 | 16.05 A partial update changes only the supplied fields. |  |  | 200 OK; only totalprice and depositpaid change. |  |  |  |  |
| RB-CRUD-006 | 16.06 After the partial update, changed fields are updated and all other fields are preserved. |  |  | 200 OK; changed + preserved fields correct. |  |  |  |  |
| RB-CRUD-007 | 16.07 The booking can be deleted. |  |  | 201 Created. |  |  |  |  |
| RB-CRUD-008 | 16.08 The deleted booking can no longer be retrieved. |  |  | 404 expected; no data. |  |  |  |  |
| RB-CRUD-009 | 16.09 The deleted booking is absent from search results. |  |  | 200 OK; deleted ID absent. |  |  |  |  |
| RB-E2E-001 | 17.01 The API is available before the flow starts. |  |  | 201 Created. |  |  |  |  |
| RB-E2E-002 | 17.02 Obtain a token for the journey. |  |  | 200 OK; token saved. |  |  |  |  |
| RB-E2E-003 | 17.03 Create the guest's booking. |  |  | 200 OK; bookingid saved. |  |  |  |  |
| RB-E2E-004 | 17.04 The stored booking matches the guest's request in every field. |  |  | 200 OK; all fields equal the submitted data. |  |  |  |  |
| RB-E2E-005 | 17.05 Update the booking with the token. |  |  | 200 OK; booking updated. |  |  |  |  |
| RB-E2E-006 | 17.06 The stored booking reflects the update. |  |  | 200 OK; equals 17.05 body. |  |  |  |  |
| RB-E2E-007 | 17.07 Partially update the booking with the token. |  |  | 200 OK; only additionalneeds changes. |  |  |  |  |
| RB-E2E-008 | 17.08 The partial update changed only additionalneeds. |  |  | 200 OK; changed and preserved fields correct. |  |  |  |  |
| RB-E2E-009 | 17.09 Delete the booking with the token. |  |  | 201 Created. |  |  |  |  |
| RB-E2E-010 | 17.10 The cancelled booking is gone. |  |  | 404 expected; booking gone. |  |  |  |  |
| RB-UTIL-001 | 18.01 Set up a known practice booking. |  |  | 200 OK; practice booking created and ID saved. |  |  |  |  |
| RB-UTIL-002 | 18.02 Set up a valid token. |  |  | 200 OK; token saved. |  |  |  |  |
| RB-UTIL-003 | 18.03 Remove test data you created. |  |  | 201 Created. |  |  |  |  |
| RB-UTIL-004 | 18.04 Verify cleanup and leave the environment clean. |  |  | 404 expected; booking_id and token cleared. |  |  |  |  |

## 5. Defect log

| Defect ID | Title | Severity | Priority | Test Case ID(s) | Steps to reproduce | Expected | Actual | Evidence | Status |
|---|---|---|---|---|---|---|---|---|---|
| DEF-001 |  |  |  |  |  |  |  |  | Open |
| DEF-002 |  |  |  |  |  |  |  |  | Open |

**Severity guide:**

- **Critical:** security or data loss (for example a change accepted without credentials, or a booking deleted by an unauthorised request).
- **High:** wrong or corrupted business data (for example a value stored with the opposite meaning, or a field lost during an update).
- **Medium:** wrong status codes, contract or header mismatches, or validation gaps with a workaround.
- **Low:** cosmetic issues and documentation typos.

## 6. Observations and questions for the product owner

Use this for behaviour the documentation doesn't define (tests marked *Investigate*), where you need a decision rather than a fix.

| # | Test Case ID | Observation | Question / suggested rule | Raised with | Answer |
|---|---|---|---|---|---|
| 1 |  |  |  |  |  |

## 7. Sign-off

| Role | Name | Date | Comment |
|---|---|---|---|
| Tester |  |  |  |
| Reviewer |  |  |  |
