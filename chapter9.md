# Chapter 9: Unit Tests

## The Three Laws of TDD

TDD (test-driven development) asks us to write unit tests first, before we write production code. But there is more:

1) Do not write any production code without a failing test first.
2) Write only enough test code as is sufficient enough to fail.
3) Only implement a minimal code that makes the failing test pass.

## Keeping Tests Clean

 *Test code is just as important as production code.* .
 
 Having dirty tests is equivalent to having no tests at all. In any change you make in the production code will make the tests harder to change if they are not clean.

 **If you have tests, you do not fear making changes in the code**.

 ## Clean Tests

 Readability is even more important in unit tests than it is in the production code.

 The *BUILD-OPERATE-CHECK* pattern makes the tests obvious. Each test is clearly split into three parts: 
 
 - The first part builds up the test data,
 - the second part operates on that test data, 
 - and the third part checks that the operation yielded the expected results.

## One Assert per Test

Every test function should have one and only one *assert* statement.

### Single Concept per Test

We don't want long test functions that go testing one miscellaneous thing after another. **Split your test into independent tests.**

## F.I.R.S.T

Clean tests follow five other rules that form the above acronym:

- **Fast**: Tests should be fast. You won't run slow tests frequently, and if you don't run them frequently, you won't find problems early enough to fix them.
- **Independent**: Tests should not depend on each other. One test should not set up the conditions for the next test.
- **Repeatable**: Tests should be repeatable in any environment. (In production, QA, on your laptop etc.)
- **Self-Validating**: The tests should have a boolean output. Either they pass or fail.
- **Timely**: The tests need to be written in a timely fashion. Unit tests should be written just before the production code that makes them pass. If you write them after the production code, then you may find the production code to be hard to test.
