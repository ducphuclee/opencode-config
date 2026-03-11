# Task Creation Templates

## Domain Layer Task Template

```yaml
Title: [{FEATURE}-DOMAIN] Implement {ComponentName} with unit tests

Description:
  Create {ComponentName} following D-ONE domain layer standards.
  Must include comprehensive unit tests.

AC:
  - {ComponentName} class/interface created in domain layer
  - Unit tests cover happy path, error cases, edge cases
  - All tests pass following TDD workflow
  - Follows done-domain-layer conventions
  - Pure Dart (no Flutter imports)

Plan:
  1. Create {ComponentName} skeleton
  2. Write failing unit tests (RED)
  3. Implement logic to pass tests (GREEN)
  4. Refactor if needed
  5. Verify all tests pass

References:
  - done-domain-layer
  - done-testing-workflow

Labels: [domain, test, {feature}]
```

## Data Layer Task Template

```yaml
Title: [{FEATURE}-DATA] Implement {RepositoryName} with tests

Description:
  Implement {RepositoryName} following repository pattern.
  Must test with mocked data sources.

AC:
  - Repository implements domain interface
  - Unit tests with mocked data sources
  - Error handling follows conventions
  - All tests pass
  - Converts Model ↔ Entity properly

Plan:
  1. Create repository class structure
  2. Write tests with mock data sources
  3. Implement repository methods
  4. Verify tests pass

References:
  - done-data-layer
  - done-testing-workflow

Labels: [data, test, {feature}]
```

## Presentation Layer Task Template

```yaml
Title: [{FEATURE}-UI] Implement {PageName} with BLoC tests

Description:
  Create {PageName} UI with {BlocName} following D-ONE presentation standards.

AC:
  - {BlocName} extends BaseCubit with proper states
  - BLoC unit tests for all state transitions
  - {PageName} uses DoneUI components only
  - Widget tests for critical user interactions
  - Uses AppLocalizations for all text
  - Error handling uses ErrorUtils

Plan:
  1. Create {BlocName} with state classes
  2. Write BLoC unit tests
  3. Create {PageName} widget
  4. Write widget tests
  5. Verify all tests pass

References:
  - done-presentation-layer
  - done-testing-bloc
  - done-ui-layout

Labels: [presentation, ui, test, {feature}]
```
