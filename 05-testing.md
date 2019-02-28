# Testing Rego Policies

OPA has a built-in test concept and facilities to execute unit tests.

## Example

authz.rego:

```rego
package authz

allow {
    data.users[u].name = input.user
    data.users[u].roles[_] = "admin"
}
```

authz_test.rego:

```rego
package authz

test_allowed {
    allow with input as { "user": "alice" } with data.users as users
}

test_denied_no_admin {
    not allow with input as { "user": "bob" } with data.users as users
}

test_denied_unknown_user {
    not allow with input as { "user": "oscar" } with data.users as users
}

users = [
    {"name": "alice", "roles": ["admin", "user"] },
    { "name": "bob", "roles": ["user"] }
]
```

## Executing Tests

Run the test case:

```bash
./opa test -v .
```

Coverage:

```bash
./opa test --coverage .
```

Also, there is support for profiling using `opa eval`.
See the OPA documentation for details:
[openpolicyagent.org/docs/how-do-i-test-policies](https://www.openpolicyagent.org/docs/how-do-i-test-policies.html#profiling).
