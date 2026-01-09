# Prevent Over-Selling

A reference implementation and design guide to **prevent overselling and ensure proper stock management** for:

- 🎟️ Ticket Booking Systems  
- 🏨 Hotel Room Booking Systems  
- 🛒 E-commerce Inventory Management  

This repository focuses on **concurrency-safe stock reservation and restoration techniques** using proven system design patterns.

---

## 🔐 Optimistic Locking – Stock Reserve & Restore Scenario

Optimistic locking is used to prevent overselling **without applying database-level locks**.  
It works by validating a version number during updates and rejecting conflicting writes.

This approach is suitable when:
- Read operations are frequent
- Write conflicts are relatively rare
- High scalability is required

---

### 📊 Scenario: Preventing Overselling with Optimistic Locking

👉 [Details View: Optimistic Locking in Ticket Booking System](  
https://github.com/faisal-porag/prevent_over_selling/wiki/Case-1:-Preventing-Over%E2%80%90Selling-in-E%E2%80%90commerce-Systems
)

**Figure:** Optimistic locking flow showing successful stock updates (no conflict) and failed updates due to concurrent version mismatch.

---

### 🧠 How It Works (High Level)

1. Client reads current stock along with its `version`
2. Client attempts to reserve stock
3. Database updates succeed **only if version matches**
4. Version increments on successful update
5. Conflicting requests fail and must retry

---

### ✅ Benefits

- Prevents overselling
- No database row locks
- High performance under low contention
- Scales well for distributed systems

---

### ⚠️ Limitations

- Performance degrades under high contention
- Retrying logic required at application level
- Not ideal for flash-sale–like traffic spikes

---

### 🏁 Use Cases

- Ticket booking systems
- Hotel room reservations
- Limited-stock e-commerce items

---

> **Note:** Optimistic locking works best when conflicts are rare.  
> For heavy contention scenarios, consider pessimistic locking or queue-based reservation systems.
