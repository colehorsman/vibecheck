# Test Generator Prompt

Use this to generate tests for your code.

---

## The Prompt

```
Write tests for this code:

[PASTE CODE]

Testing framework: [FRAMEWORK - e.g., Jest, Vitest, pytest]

Include:
- Unit tests for each function
- Edge cases
- Error handling tests
- [SPECIFIC REQUIREMENT]

Use descriptive test names that explain what's being tested.
```

---

## Quick Unit Tests

```
Write unit tests for this function:

[PASTE FUNCTION]

Framework: [Jest/Vitest/pytest]

Cover:
- Happy path
- Edge cases
- Error cases
```

---

## React Component Tests

```
Write tests for this React component:

[PASTE COMPONENT]

Framework: [React Testing Library + Jest/Vitest]

Test:
- Renders correctly
- User interactions work
- Props are handled correctly
- Loading/error states
```

---

## API Endpoint Tests

```
Write tests for this API endpoint:

[PASTE ENDPOINT CODE]

Framework: [Supertest + Jest / pytest]

Test:
- Successful requests
- Validation errors
- Authentication (if applicable)
- Error responses
```

---

## Integration Tests

```
Write integration tests for this feature:

[DESCRIBE FEATURE OR PASTE CODE]

The feature involves:
- [COMPONENT 1]
- [COMPONENT 2]
- [DATABASE/API CALLS]

Test the full flow from user action to result.
```

---

## Test Edge Cases

```
I have this function:

[PASTE FUNCTION]

What edge cases should I test? Generate tests for:
- Boundary values
- Empty/null inputs
- Invalid inputs
- Large inputs
- Concurrent calls (if applicable)
```

---

## Add Tests to Existing Code

```
This code has no tests. Add comprehensive test coverage:

[PASTE CODE]

Framework: [FRAMEWORK]

Prioritize:
1. Critical paths
2. Error handling
3. Edge cases

Aim for [X]% coverage.
```

---

## Mock External Dependencies

```
Write tests for this code that calls external services:

[PASTE CODE]

Mock these dependencies:
- [DEPENDENCY 1 - e.g., database]
- [DEPENDENCY 2 - e.g., API call]

Show how to set up mocks and verify they're called correctly.
```

---

## Snapshot Tests

```
Create snapshot tests for these components:

[LIST COMPONENTS]

Framework: Jest

Include:
- Default render
- With different props
- Different states (loading, error, empty)
```

---

## E2E Test Scenarios

```
Write E2E test scenarios for this user flow:

Flow: [DESCRIBE USER JOURNEY]
1. User goes to [PAGE]
2. User [ACTION]
3. User sees [RESULT]

Framework: [Playwright/Cypress]

Include setup and teardown.
```

---

## Tips

- Start with happy path, then edge cases
- Use descriptive test names
- Don't test implementation details
- Mock external dependencies
- Keep tests independent
- Run tests after generating to verify they pass
