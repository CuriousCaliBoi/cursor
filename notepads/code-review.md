# Code Review Checklist Notepad

Code Review for: [PR/Change Description]

## Functionality
- [ ] Does it solve the stated problem or implement the requested feature?
- [ ] Are edge cases handled appropriately?
- [ ] Error handling is appropriate and consistent?
- [ ] Performance implications considered? (if relevant)

## Code Quality
- [ ] Follows project style guide and conventions
- [ ] No unnecessary code duplication
- [ ] Appropriate abstractions (not over-engineered, not under-engineered)
- [ ] Clear, descriptive naming
- [ ] Functions/classes have single responsibility
- [ ] No commented-out code or debug statements

## Testing
- [ ] Tests added/updated for new/changed functionality
- [ ] Test coverage maintained or improved
- [ ] Integration tests added if needed
- [ ] Tests are meaningful and test the right things
- [ ] Tests are maintainable and readable

## Architecture
- [ ] Fits existing architectural patterns
- [ ] No breaking changes (or breaking changes properly documented)
- [ ] Dependencies are appropriate and minimal
- [ ] Module boundaries respected
- [ ] Changes don't introduce architectural debt

## Security
- [ ] No sensitive data exposed (secrets, tokens, etc.)
- [ ] Input validation present where needed
- [ ] Authentication/authorization handled correctly (if applicable)
- [ ] SQL injection / XSS / other vulnerabilities considered
- [ ] Dependencies are up-to-date and secure

## Documentation
- [ ] Public APIs documented (if applicable)
- [ ] Complex logic has explanatory comments
- [ ] Breaking changes documented
- [ ] README updated if needed

## Performance
- [ ] No obvious performance issues (N+1 queries, unnecessary loops, etc.)
- [ ] Database queries are optimized
- [ ] Large data handled appropriately
- [ ] Caching considered where appropriate

## Accessibility (if UI changes)
- [ ] Semantic HTML used
- [ ] ARIA labels where needed
- [ ] Keyboard navigation works
- [ ] Screen reader friendly

## Suggestions
[Add specific feedback, questions, or improvement suggestions]

Example Usage:
```
Code Review for: Add user profile editing feature

Functionality:
✅ Solves the feature request
✅ Handles invalid input gracefully
⚠️ Missing: validation for email format
❌ Error messages could be more specific

Code Quality:
✅ Follows React component patterns
✅ Good separation of concerns
⚠️ Consider extracting validation logic to utility

Testing:
✅ Unit tests added
✅ Integration test covers happy path
❌ Missing: Test for error case when API fails

Architecture:
✅ Uses existing API service pattern
✅ No breaking changes
✅ Fits current component structure

Suggestions:
1. Add email format validation
2. Extract email validation to shared utility
3. Add error case test
4. Consider loading state for better UX
```

