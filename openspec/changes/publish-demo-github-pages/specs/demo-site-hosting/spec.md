# Spec Delta

## Purpose

Makes the interactive Sharon's Kitchen demo publicly reachable at a stable web address, while keeping the private business and specification documents out of the public repository.

## ADDED Requirements

### Requirement: Demo is served at a public URL
The interactive demo SHALL be reachable over HTTPS at `https://omerel.github.io/sharons-kitchen/`, serving the demo's `index.html` together with its stylesheet, script and images.

#### Scenario: Opening the site root
- **WHEN** a visitor opens `https://omerel.github.io/sharons-kitchen/`
- **THEN** the demo home page loads in Hebrew RTL with its styles applied and the customer view working

#### Scenario: Assets load from relative paths
- **WHEN** the demo page loads at the site URL
- **THEN** `styles.css` and `app.js` are fetched from the same site without 404 errors

#### Scenario: Single-file version is also reachable
- **WHEN** a visitor opens `https://omerel.github.io/sharons-kitchen/Sharon_Kitchen_Interactive_Demo.html`
- **THEN** the single-file version of the demo loads and works

### Requirement: Hosted demo behaves like the local demo
The hosted demo SHALL keep the behaviour it has when opened locally, including browser-local persistence and the reset action, and SHALL NOT require any server, account or build step.

#### Scenario: Placing an order on the hosted demo
- **WHEN** a visitor adds a dish to the cart and completes checkout on the hosted site
- **THEN** the order appears in the admin view in the same browser, as it does locally

#### Scenario: Resetting the hosted demo
- **WHEN** a visitor clicks the demo reset button
- **THEN** the demo returns to its initial sample data

### Requirement: Business documents are not published
The public repository SHALL NOT contain the handoff documents folder or the complete specification PDF and DOCX files.

#### Scenario: Inspecting the public repository
- **WHEN** someone browses the `main` branch of `omerel/sharons-kitchen` on GitHub
- **THEN** `sharons_kitchen_handoff/`, `Sharon_Kitchen_Complete_Specification.pdf` and `Sharon_Kitchen_Complete_Specification.docx` are not present

#### Scenario: Accidental staging is prevented
- **WHEN** a contributor runs `git add .` in the project root
- **THEN** none of the excluded business documents are staged
