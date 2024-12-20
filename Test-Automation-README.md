## Setting Up the automation test for TernKey:

We will use Cypress for End-to-End Testing (E2E) and Jest for Unit Testing

## E2E testing:

Cypress: An excellent choice for E2E testing. It provides a developer-friendly interface, built-in test runners, and great debugging tools

## Unit Testing:

Jest: Widely regarded as the best testing library for React and Next.js.
    - Built-in support for JavaScript and TypeScript.
    - Provides mocking capabilities.
    - Works seamlessly with Next.js.

# Per-installations on Next.js project:

## Installation of Cypress:

# Add Cypress to your Next.js project:

        npm install --save-dev cypress

# Open Cypress for the first time to create the configuration files:

        npx cypress open

# This will create configration file for cypress with name cypress.config.js:

        const { defineConfig } = require("cypress");

        module.exports = defineConfig({
        e2e: {
            baseUrl: "http://localhost:3000", // Replace with your local development URL
            supportFile: "cypress/support/e2e.js",
            specPattern: "cypress/e2e/**/*.cy.{js,jsx,ts,tsx}",
        },
        });

## Installation of Jest:

# install Jest and it's dependencies:

        npm install --save-dev jest @testing-library/react @testing-library/jest-dom babel-jest

# Add a Jest configuration in jest.config.js:

        const nextJest = require("next/jest");

        const createJestConfig = nextJest({
        dir: "./", // Path to your Next.js app
        });

        const customJestConfig = {
        setupFilesAfterEnv: ["<rootDir>/jest.setup.js"],
        testEnvironment: "jest-environment-jsdom",
        };

        module.exports = createJestConfig(customJestConfig);

## Create the Tests

# E2E Tests (Cypress): Place your Cypress tests under cypress/e2e/. Example:

        // cypress/e2e/home.cy.js
        describe("Home Page", () => {
        it("should display the home page correctly", () => {
            cy.visit("/");
            cy.contains("Welcome to Next.js").should("be.visible");
        });
        });

# Unit Tests (Jest + React Testing Library): Place your unit tests under __tests__/. Example:

        // __tests__/Home.test.js
        import { render, screen } from "@testing-library/react";
        import Home from "../pages/index";

        test("renders welcome message", () => {
        render(<Home />);
        const heading = screen.getByText("Welcome to Next.js");
        expect(heading).toBeInTheDocument();
        });

