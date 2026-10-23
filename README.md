# Software Security Test Plan and Assessment

## Overview
An academic software-security assessment of DBABA, a Python
command-line address-book application.

The project evaluates five security requirements through structured
test scenarios, manual application testing, requirements traceability,
defect reporting, and supporting static analysis with Pylint.

Testing used synthetic accounts and contact information in a
local Linux environment.

## Academic Context
Completed for CYBR 510: Security Test Engineering at the
University of San Diego.

Assignment: Software Security Test Plan

## Assessment Scope
- Application: DBABA Python application
- Interface reference: ABA Command Line Interface Specification v1.3.2
- Environment: Local Linux terminal
- Test data: Synthetic accounts and address-book records
- Static-analysis tool: Pylint

The assessment documents observed behavior in the tested build.
It does not claim complete security coverage or that defects
have been remediated.

## Security Requirements

| ID | Area | Assessment Focus |
|---|---|---|
| SR-1 | Credential complexity | Password validation and documented length restrictions |
| SR-2 | Account lockout | Alarm and 60-second lockout after three consecutive failed login attempts |
| SR-3 | Authentication | Prevention of unauthenticated access and account-identity bypass |
| SR-4 | Access rights | Administrative privileges, role restrictions, and cross-user record isolation |
| SR-5 | Sensitive information | Credential storage, database and export permissions, audit logs, and error messages |

Password-validation tests evaluated the assignment's stated
requirements and interface specification. They are not presented
as a universal password-policy recommendation.

## Methodology
1. Identified five security requirements.
2. Developed nine test scenarios covering those requirements.
3. Defined 43 test cases with expected results.
4. Executed applicable cases using synthetic accounts and data.
5. Recorded actual results and pass, fail, or not-applicable status.
6. Traced test results back to security requirements.
7. Distinguished specification deficiencies from implementation
   and interface-conformance defects.
8. Used Pylint to identify supporting code-quality and reliability
   concerns.

## Test Coverage
The test plan included:
- Password creation and validation boundaries
- Failed-login handling and account lockout
- Unauthenticated command execution
- Attempts to authenticate as another account
- Normal-user access to administrative commands
- Administrator restrictions on confidential records
- Cross-user record access and modification
- Password hashing and salt behavior
- Local database and export-file permissions
- Sensitive information in audit logs and error messages
- Applicability of encryption-in-transit testing

## Selected Findings

| Area | Documented Observation |
|---|---|
| Password length | A six-character password was accepted despite the account-identification specification's eight-character minimum. |
| Account lockout | Three failed login attempts did not trigger the required alarm or lockout; a correct password was accepted immediately afterward. |
| Account enumeration | A normal authenticated user could list application accounts through LSU. |
| Interface responses | Some rejected edit operations returned no required completion message, even though the targeted records remained unchanged. |
| Database storage | The SQLite database was readable by other local users and exposed synthetic contact information through direct queries. |
| Export protection | An export contained only the correct user's records but had permissions allowing other local users to read it. |

These findings distinguish unauthorized disclosure from
interface-response defects. A missing denial message does not
by itself demonstrate that an unauthorized modification occurred.

## Controls That Passed Selected Tests
- Commands requiring authentication rejected unauthenticated use.
- Another user's password did not authenticate the requested account.
- Tested cross-user record operations did not disclose or change
  the other user's records.
- Established passwords were stored as bcrypt-formatted hashes
  rather than plaintext.
- Two accounts using the same test password had different stored
  bcrypt hash values.
- Tested audit output did not expose passwords, password hashes,
  or full contact information.
- Tested error messages did not expose tracebacks, database
  schemas, or other users' confidential records.

Passing these cases demonstrates the observed behavior only,
not that every possible bypass was excluded.

## Static Analysis
Pylint reported a score of 7.15 out of 10.

Selected findings included:
- A variable potentially used before assignment
- An unused comparison expression that may indicate an
  assignment error
- Statements with no apparent effect
- Broad exception handling
- File operations without explicit encoding or context managers
- Complex branching and deeply nested logic
- Documentation, naming, and formatting issues

Pylint findings were treated as code-review leads rather than
automatic proof of exploitable vulnerabilities.

The Pylint score is not an application-security rating.

## Test Limitations
- Account-lockout expiration and counter-reset behavior could
  not be meaningfully validated because the required lockout
  behavior was not demonstrated.
- Encryption-in-transit testing was not applicable to the
  provided standalone build because it had no implemented
  network-transfer interface.
- Testing was limited to the specified requirements,
  application build, environment, and selected cases.
- The project reports assessment results, not verified fixes.

## Deliverables
The accompanying report contains:
- Security requirements
- Test scenarios and priorities
- Detailed test cases
- Expected and actual results
- Supporting screenshots
- Requirements-to-test traceability
- Defect documentation
- Pylint findings and output

## Skills Demonstrated
- Requirements-based security testing
- Positive, negative, and boundary test design
- Authentication and authorization assessment
- Role-based and cross-user access testing
- Sensitive-data protection assessment
- Requirements traceability
- Defect classification and reporting
- Static-analysis interpretation
- Evidence-based technical writing

## Report
See the accompanying Assignment 4.1 report for detailed test
procedures, execution evidence, traceability, and analysis.

## Responsible Use
This repository documents an educational assessment using
synthetic accounts and data.

It does not grant permission to test other applications or systems.
