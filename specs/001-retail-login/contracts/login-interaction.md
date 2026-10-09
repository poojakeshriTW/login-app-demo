# Login Interaction Contract

This contract describes the login UI's boundary with the application's
authentication and account-navigation capabilities. It does not prescribe
network endpoints or an authentication implementation.

## Sign-in request

The login experience submits:

- Required email address.
- Required password.
- Optional `rememberMe` boolean, unchecked by default.

The authentication provider owns credential verification and session
creation. A successful request with `rememberMe` selected asks the provider to
retain the authenticated session on the current device. An unchecked choice
uses the provider's standard session. Neither outcome permits storing the
password as the Remember Me preference.

## Sign-in outcomes

- **Success**: Provider confirms authentication and establishes the requested
  session; the UI continues to the application's normal authenticated
  destination.
- **Rejected credentials**: Provider denies authentication; the UI displays a
  generic incorrect-email-or-password message and does not disclose which
  credential failed.
- **Unavailable**: Provider reports or encounters an inability to complete
  sign-in; the UI explains the failure and permits retry.
- **Local validation failure**: Required-field or email-format validation
  prevents the provider request.

The UI MUST NOT display success or navigate as authenticated before the
provider confirms success. Failed requests MUST NOT create an authenticated
persistent session.

## Account navigation

- Forgot Password? navigates to the application's existing password recovery
  journey.
- Sign Up / Register navigates to the application's existing registration
  journey.

The host application must supply the provider integration and destination
routes. Their endpoint and path details are intentionally not invented here.
