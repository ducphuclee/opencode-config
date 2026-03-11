# Task Granularity Examples

## ❌ WRONG - God Tasks (REJECT)

### Example 1: Too many layers
```
[LOGIN] Implement login feature
AC:
1. LoginUseCase works (Domain)
2. LoginRepository works (Data)
3. LoginBloc works (Presentation)
4. LoginPage works (Presentation)

REJECT: 4 components in 1 task. Split into 4 tasks.
```

### Example 2: Vague scope
```
[TEST] Achieve 90% coverage
AC:
1. Coverage reaches 90%

REJECT: Too vague. Which files? Which layers?
```

## ✅ CORRECT - Small Tasks (APPROVE)

### Example 1: Single UseCase
```
[LOGIN-DOMAIN] Implement LoginByEmailUseCase with unit tests

AC:
1. LoginByEmailUseCase class created in domain layer
2. Unit tests cover:
   - Happy path: valid credentials
   - Error case: invalid email format
   - Error case: wrong password
   - Edge case: empty email
3. All tests pass (TDD: RED → GREEN)
4. Follows done-domain-layer conventions

APPROVE: 1 component, Domain layer only, clear AC.
```

### Example 2: Single Bloc
```
[LOGIN-PRESENTATION] Implement LoginBloc with unit tests

AC:
1. LoginBloc extends BaseCubit<LoginState>
2. State transitions tested:
   - Initial → Loading → Success
   - Initial → Loading → Error
3. All tests pass
4. Uses ErrorUtils.getUserMessage() for errors

APPROVE: 1 component, Presentation layer only.
```

### Example 3: Single Widget
```
[LOGIN-UI] Implement LoginForm widget with tests

AC:
1. LoginForm widget created using DoneUI components
2. Email field validation works
3. Password field validation works
4. Widget tests for user interactions
5. Submit button triggers bloc event

APPROVE: 1 UI component, clear scope.
```

## Task Size Guidelines

| Task Size | Lines of Code | Duration | Example |
|-----------|--------------|----------|---------|
| **Small** | < 100 lines | 30-60 min | 1 entity test |
| **Medium** | 100-300 lines | 1-2 hours | 1 UseCase + test |
| **Large** | 300-500 lines | 2-4 hours | 1 Bloc + test |
| **TOO BIG** | > 500 lines | > 4 hours | **Split it!** |
