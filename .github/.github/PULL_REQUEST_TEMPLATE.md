<!-- Thank you for your contribution! Please review the following guidelines and check the boxes to confirm. -->

### Coding Guidelines Compliance

---

### 1. Pre-Push Local Checks
- [ ] I have at least **tried** to run all of the following commands locally and they pass without error:
  - `cargo fmt`
  - `cargo clippy -- -D warnings`
  - `cargo check`
  - `cargo test`
  - `[if applicable: tests_sgx]`
Reminder: use `[ci skip]` if you know the code is not compiling or some tests are broken

---

### 2. Code Structure
- [ ] All new functions, structs, and fields are **private by default** and only `pub` where necessary.
- [ ] No code has been copy-pasted; logic has been moved into reusable functions or shared crates.
- [ ] No `trait` has been added for a single `impl`.
- [ ] Complex modules have been moved into their own files (no inline `mod`).

---

### 3. Error Handling
- [ ] The code contains **no `.unwrap()` or `.expect()`** in runtime logic. All fallible logic returns a `Result`.

---

### 4. Testing
- [ ] **Every `pub` function** (extrinsic, getter) introduced or modified by this PR is fully tested.
- [ ] Tests include both **success ("happy path") and failure** cases.
- [ ] A test case exists for **every logical branch** (each `ensure!`, `match`, `if/else`, `map_err`, `?`).
- [ ] External APIs are **not** called directly in unit tests. (Mocking is a last resort; `testcontainers` or local servers are preferred).
- [ ] Tests are self-contained and perform their own setup/teardown.
- [ ] Tests are not mixed; each test function verifies a single, specific behavior.
- [ ] A logger (`env_logger::try_init()`) is initialized in the test setup.

---

### 5. Security
- [ ] **No secrets** (private keys, seeds, pins) are returned from any getter.
- [ ] The public API of the pallet is minimal and secure by design (e.g., exposing `check_pin` instead of `get_pin`).
- [ ] New, safe structs are used for getter return types to avoid exposing sensitive internal state.

---

### 6. Bonus Points & Best Practices
- [ ] No hardcoded URLs have been added; configuration is handled by env vars or parameters.
- [ ] No default values are used for environment variables.
- [ ] Logging has been added to all new functions and error paths (`map_err`).
- [ ] `ensure_has_root_account` (or equivalent authorization check) is present on **every** new extrinsic and getter.

