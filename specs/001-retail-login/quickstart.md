# Quickstart: Retail Login Validation

This guide describes validation of the implemented login experience. The
repository currently has no authentication integration or test runner, so
end-to-end authentication checks require the approved provider and routes.

## Prerequisites

- Node.js and npm versions supported by the repository.
- Dependencies installed from the project lockfile.
- The approved authentication provider and the application's recovery,
  registration, and authenticated landing destinations configured before
  testing live sign-in.

## Run quality checks

From the repository root:

```sh
npm run lint
npm run build
```

Expected result: both commands complete successfully with no lint or production
build errors.

## Manual validation scenarios

1. Open the login page at desktop width and confirm Email Address, Password,
   Remember Me, Login, Forgot Password?, and Sign Up / Register are present.
2. Submit with both fields empty, then with each field empty in turn. Confirm
   the missing field is identified and no authentication request is made.
3. Enter a malformed email address and a password. Confirm email validation
   prevents submission.
4. Enter a password, toggle Show Password and Hide Password repeatedly, and
   confirm the value is unchanged.
5. Submit rejected credentials. Confirm access is denied and the message does
   not identify which credential was wrong.
6. Simulate an unavailable authentication provider. Confirm a recoverable
   message appears and the form permits retry.
7. Sign in successfully with Remember Me selected and verify provider-managed
   persistence on a later visit on the same device. Repeat with Remember Me
   unchecked and verify only the standard session is applied. Confirm failed
   sign-in never creates a remembered session and the password is not stored
   as a preference.
8. Follow Forgot Password? and Sign Up / Register and verify each reaches its
   existing application journey.
9. Repeat the layout and interaction checks at 320 CSS pixels, a representative
   tablet width, and a desktop width. Confirm controls, links, and messages
   remain readable and operable without unintended horizontal scrolling.

## Test limitation

`package.json` defines lint, build, dev, and start scripts but no automated
test script. Automated interaction coverage may be added only if the project
adopts a test runner; do not treat visual checks as proof of a live
authentication integration.
