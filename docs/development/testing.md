# Testing Guide

RushChat testing documentation.

## Testing Overview

```markmap
# Testing Guide
## Test Types
- Unit Tests
  - Single Function
  - Single Module
  - Fast Execution
- Integration Tests
  - Multiple Modules
  - Module Collaboration
  - Interface Testing
- End-to-End Tests
  - Complete Flow
  - User Scenarios
  - System Testing
## Backend Testing
- Run Tests
  - cargo test
  - Test Suite
- Write Tests
  - #[cfg(test)]
  - #[test]
  - Assertions
## Frontend Testing
- Run Tests
  - npm test
  - Jest
- Write Tests
  - Component Tests
  - Utility Function Tests
## Test Coverage
- Code Coverage
- Feature Coverage
- Boundary Testing
```

## Test Types

### Unit Tests

Test single functions or modules.

### Integration Tests

Test collaboration between multiple modules.

### End-to-End Tests

Test complete user flows.

## Backend Testing

### Run Tests

```bash
cd server-rust
cargo test
```

### Write Tests

Add tests in Rust files:

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_function() {
        // Test code
    }
}
```

## Frontend Testing

### Run Tests

```bash
cd client
npm test
```

### Write Tests

Using React Testing Library:

```javascript
import { render, screen } from '@testing-library/react';
import Component from './Component';

test('renders component', () => {
  render(<Component />);
  expect(screen.getByText('Hello')).toBeInTheDocument();
});
```

## Manual Testing

### Feature Test Checklist

- [ ] User registration and login
- [ ] Send and receive messages
- [ ] Create and join channels
- [ ] Wallet connection
- [ ] Red packet send and claim
- [ ] Admin operations

## Related Documentation

- [Development Environment](setup.md)
- [Code Structure](structure.md)
