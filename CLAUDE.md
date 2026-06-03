# CLAUDE.md

## Stack
- React + Vite (browser-based, runs locally)
- Vitest for unit tests (logic, data model)
- Playwright for UI/integration tests

## Engineering Principles
Favor low complexity through:
- **Modularity** — small, focused, understandable pieces
- **High cohesion** — elements within a module are related and focused on a single task
- **Low coupling** — modules are as independent from one another as reasonably possible
- **Separation of concerns** — single responsibility, interface segregation, ports and adapters pattern
- **Abstraction and information hiding** — expose only what's necessary; hide implementation details

## Testing
- TDD: write tests before implementation
- Test behavior, not implementation details
- Unit tests cover game logic and data model
- Playwright tests cover user interactions and game states
- Given/When/Then structure in test descriptions
- Tests should provide high confidence the system functions correctly

## Code Style
- ESLint + Prettier with default configs