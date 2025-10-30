# Safe Refactoring Notepad

Objective: Improve [readability/structure/performance/maintainability] without changing behavior

Guardrails:
- Keep public APIs stable (same signatures, same behavior)
- Retain all existing tests (update if needed, don't remove functionality)
- Make small, atomic commits that preserve working state
- Document any intentional behavior changes (if any)
- Maintain backward compatibility

Checklist:
- [ ] Identify seams to isolate (boundaries between components)
- [ ] Propose rename/move plan (if applicable)
- [ ] Apply changes incrementally (one small change at a time)
- [ ] Note risks and rollback plan
- [ ] Run full test suite after each increment
- [ ] Verify no performance regressions

Approach:
[Specify the refactoring approach: Extract function? Move to module? Simplify logic? Introduce abstraction?]

Files to Modify:
@[list of files that will be changed]

Preserve:
- [What must stay the same: behavior, API, data structures, etc.]

Change:
- [What will be improved: structure, naming, organization, etc.]

Validation:
- All tests pass: `make test`
- No linting errors: `make lint`
- Behavior verification: [specific manual checks if needed]
- Performance check: [if performance is a concern]

Example Usage:
```
Objective: Extract payment processing logic into a separate service module for better organization

Approach: Extract payment-related functions from order.service.ts into payment.service.ts using dependency injection

Files to Modify:
@src/services/order.service.ts
@src/services/payment.service.ts
@src/services/payment.types.ts

Preserve:
- Order service public API (order processing interface)
- Payment processing behavior (same logic, same results)
- All existing tests should still pass

Change:
- Move payment logic to dedicated service
- Use dependency injection to connect services
- Improve separation of concerns

Validation:
- Run: make test (all order and payment tests pass)
- Manual: Verify order processing still works end-to-end
```

