Testing of App

These are three main types of testing to ensure code quality and application reliability:

Unit Testing
Purpose:
    Test individual functions or components in isolation.
    These are the tools use for it: jest and react test library.

    Example:
        // utils/calc.js
        export const add = (a, b) => a + b;

        // utils/calc.test.js
        import { add } from './calc';

        test('adds two numbers correctly', () => {
        expect(add(2, 3)).toBe(5);
        });


Integration Testing
Purpose:
    Test how multiple units (e.g. components, functions) work together.

    Example:
        // components/LoginForm.jsx
        export function LoginForm({ onSubmit }) {
        return (
            <form onSubmit={onSubmit}>
            <input placeholder="Email" />
            <button type="submit">Login</button>
            </form>
        );
        }

        // components/LoginForm.test.jsx
        import { render, screen, fireEvent } from '@testing-library/react';
        import { LoginForm } from './LoginForm';

        test('form submits when button is clicked', () => {
        const handleSubmit = jest.fn();
        render(<LoginForm onSubmit={handleSubmit} />);
        fireEvent.click(screen.getByText('Login'));
        expect(handleSubmit).toHaveBeenCalled();
        });


End-to-End (E2E) Testing
Purpose:
    Test the entire app flow from a user's perspective.
    Tool used is Cypress

    Example:
        // cypress/e2e/home.cy.js
        describe('Homepage', () => {
        it('should load and display welcome message', () => {
            cy.visit('/');
            cy.contains('Welcome');
        });

        it('adds a product to cart', () => {
            cy.get('[data-testid="add-to-cart"]').first().click();
            cy.get('[data-testid="cart-count"]').should('contain', '1');
        });
        });


To get started with the test use:
    # Unit & integration tests (Jest)
        npm test

    # E2E tests (Cypress)
        npx cypress open