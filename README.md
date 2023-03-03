Reproduce bug in kyverno test.

The second test case fails:

```
kyverno test https://github.com/joebowbeer/repro-kyverno-dup-bug

Executing repro-dups-bug...
applying 1 policy to 2 resources...

│───│────────────────────│───────────────────────│───────────────────│────────│
│ # │ POLICY             │ RULE                  │ RESOURCE          │ RESULT │
│───│────────────────────│───────────────────────│───────────────────│────────│
│ 1 │ restrict-something │ validate-some-foo     │ foo/Pod/nginx-foo │ Pass   │
│ 2 │ restrict-something │ validate-some-non-foo │ foo/Pod/nginx-too │ Fail   │
│───│────────────────────│───────────────────────│───────────────────│────────│

Test Summary: 1 tests passed and 1 tests failed

Aggregated Failed Test Cases :
│───│────────────────────│───────────────────────│───────────────────│────────│
│ # │ POLICY             │ RULE                  │ RESOURCE          │ RESULT │
│───│────────────────────│───────────────────────│───────────────────│────────│
│ 2 │ restrict-something │ validate-some-non-foo │ foo/Pod/nginx-too │ Fail   │
│───│────────────────────│───────────────────────│───────────────────│────────│
```

But if the first test case is commented-out then the remaining test case passes.

This may be related to issue:

https://github.com/kyverno/kyverno/issues/2878

Closed by PR:

https://github.com/kyverno/kyverno/pull/3612

However, note that there is no warning printed in the output of the failing test run above.