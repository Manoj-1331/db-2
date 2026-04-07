# Online Fitness Coaching Platform – ER Diagram Explanation

## Overview

This database design represents an online fitness coaching platform where trainers provide coaching services to clients. The system supports multiple types of interactions such as selling plans, managing subscriptions, scheduling sessions, tracking client progress, and handling payments.

This is not a gym management system. It focuses on online coaching where one trainer can manage multiple clients and clients can enroll in different plans over time.

---

## Core Entities Explanation

### 1. Users

The `users` table stores all individuals in the system.

It includes both trainers and clients in a single table. The `role` attribute is used to differentiate between them.

Key points:

* A user can either be a trainer or a client.
* Basic details like name and email are stored here.
* This avoids duplication and keeps authentication simple.

---

### 2. Plans

The `plans` table represents the programs or services offered by trainers.

Each plan is created by a trainer and can be purchased by multiple clients.

Examples of plans:

* Monthly coaching
* Diet plan
* Workout program

Key points:

* One trainer can create many plans.
* Each plan has a price and duration.
* This is what clients actually purchase.

---

### 3. Subscriptions

The `subscriptions` table tracks which client has purchased which plan.

This is a very important table because it connects clients and plans.

Key points:

* A client can buy multiple plans over time.
* A plan can be purchased by multiple clients.
* Start date and end date help track plan duration.
* Status shows whether the plan is active or completed.

This resolves the many-to-many relationship between clients and plans.

---

### 4. Sessions

The `sessions` table stores scheduled interactions between trainers and clients.

These can include:

* Consultation calls
* Live training sessions

Key points:

* Each session is linked to one trainer and one client.
* It has a scheduled date and a status.
* Sessions are optional; not all plans require them.

---

### 5. Check-ins

The `checkins` table is used for tracking client progress.

Clients submit updates regularly, such as:

* Weight
* Notes about progress

Key points:

* One client can have many check-ins over time.
* This data is separate from the user table to keep the design clean.
* It helps trainers monitor progress and make adjustments.

---

### 6. Payments

The `payments` table stores payment information.

It is linked to subscriptions because payments are made when a client purchases a plan.

Key points:

* Each payment corresponds to a subscription.
* It stores amount and payment status.
* Helps track whether a plan is paid or pending.

---

## Relationships and Cardinality

1. User to Plan (Trainer Side)

* One trainer can create many plans.
* Each plan belongs to one trainer.

2. User to Subscription (Client Side)

* One client can have many subscriptions.
* Each subscription belongs to one client.

3. Plan to Subscription

* One plan can have many subscriptions.
* Each subscription is linked to one plan.

4. Trainer and Client to Sessions

* One trainer can conduct many sessions.
* One client can attend many sessions.
* Each session connects one trainer and one client.

5. Client to Check-ins

* One client can submit multiple check-ins.
* Each check-in belongs to one client.

6. Subscription to Payment

* One subscription can have one or more payments.
* Each payment is linked to one subscription.

---

## Design Decisions

* A single users table is used instead of separate trainer and client tables to reduce redundancy.
* Subscriptions are used to handle the many-to-many relationship between clients and plans.
* Sessions and check-ins are kept separate because they serve different purposes.
* Progress data is not stored in the users table to maintain proper normalization.
* Payments are linked to subscriptions instead of users to reflect real transactions.

---

## Conclusion

This ER design is simple, practical, and suitable for an online fitness coaching platform. It supports multiple trainers, multiple clients, flexible plan structures, and proper tracking of sessions, progress, and payments.

The structure avoids unnecessary complexity while still covering all important business requirements.
