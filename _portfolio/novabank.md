---
title: "Nova Bank: Full-Stack Banking Application"
excerpt: "Independent project (2026). A banking app built from scratch with a double-entry ledger, row-level locking, two-factor login, and 59 automated tests. Spring Boot, PostgreSQL, Next.js."
collection: portfolio
---

**Independent project** · August – October 2026

[GitHub repository](https://github.com/PW13052003/nova-bank) · [Live demo](https://nova-bank-beta.vercel.app) (demo login details are in the repository's README)

## Overview

Nova Bank is a full-stack banking application I built from scratch to learn how backend, database, and security concerns fit together in a system that moves money. Users can open checking and savings accounts, deposit, withdraw, and transfer between them, view their transaction history, and turn on two-factor login.

## Design

**Ledger**

- Balances are never stored and overwritten. Every movement writes double-entry ledger records, and an account's balance is the sum of its entries.
- Money is stored as integer cents, never floating point.
- Each transaction, its ledger entries, and its audit record are written in a single database transaction, so a failure saves none of them.
- Idempotency keys stop a repeated request from moving money twice.

**Concurrency**

- Withdrawals and transfers lock account rows before checking the balance.
- Transfers always lock accounts in the same order, so two opposite transfers can't deadlock.
- Tested directly: ten simultaneous withdrawals against a $50 balance produce exactly five successes and a final balance of zero.

**Security**

- BCrypt password hashing, and 15-minute sessions in HttpOnly, Secure cookies
- Optional two-factor login with an authenticator app, using separately scoped tokens so a password alone can't start a session
- Account lockout, rate limiting on login and code checks, and an audit log of logins and money movements
- Ownership checks on every account operation, and parameterized queries throughout

## Testing and deployment

- 59 automated tests covering authentication, the ledger, concurrency, audit logging, two-factor login, and rate limiting
- GitHub Actions runs the full test suite against a PostgreSQL container and builds the frontend on every push
- Deployed with Docker on Render (backend), Vercel (frontend), and Neon (database)

## Tools

Java 21, Spring Boot, Spring Security, PostgreSQL, JDBC, Next.js, TypeScript, Tailwind CSS, JUnit 5, Docker, GitHub Actions
