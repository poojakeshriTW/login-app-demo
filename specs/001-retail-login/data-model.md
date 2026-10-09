# Data Model: Retail Login Page

The login page has transient form and request state only. Credentials are
submitted to the application's authentication provider; this feature adds no
database entities or credential persistence.

## Entities

### Login Credentials

| Field | Type | Rules |
|-------|------|-------|
| Email address | Text | Required; must have a valid email format before submission. |
| Password | Secret text | Required; value is passed to the authentication provider and is not retained as a Remember Me preference. |

### Remember Me Preference

| Field | Type | Rules |
|-------|------|-------|
| Selected | Boolean | Optional; defaults to unchecked for a new form session. |

The preference is sent with the sign-in attempt. It requests provider-managed
session persistence on the current device; it does not store or prefill the
password. A failed sign-in cannot establish a persistent authenticated session.

### Authentication Outcome

| Outcome | Meaning | User-visible behavior |
|---------|---------|-----------------------|
| Accepted | Provider authenticated the credentials. | Continue to the normal authenticated destination; persistence follows the Remember Me choice. |
| Rejected | Provider did not accept the credentials. | Keep the customer unauthenticated and show a generic credentials error. |
| Unavailable | The provider could not complete the request. | Keep the customer unauthenticated, explain that sign-in could not be completed, and allow retry. |

## Form State

The form interaction has these mutually exclusive request states:

- **Idle**: Accepting input and ready to submit.
- **Invalid**: Local validation failed; identify missing fields or malformed
  email and do not submit.
- **Submitting**: Authentication is pending; prevent duplicate submission and
  expose progress to the customer.
- **Rejected**: Credentials were not accepted; show a non-specific error and
  allow correction/retry.
- **Unavailable**: Authentication could not complete; show a recoverable error
  and allow retry.
- **Authenticated**: Authentication succeeded; leave the login flow for the
  authenticated destination.

Password visibility is a presentation state and must not alter the password
value. Form state is cleared according to the application's established
security/session handling; no persistent password storage is introduced.
