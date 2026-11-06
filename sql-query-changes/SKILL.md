---
name: sql-query-changes
description: Use whenever you change a SQL query or the code that builds one, for speed/memory optimization or for correctness. Prove what the change does to results, ground it in real traffic, and explain it from how the database reads data.
---

# SQL query changes

A query change ships when you can prove what it does to results, show it matters on real traffic, and explain why it works.

## Bar

- **Results:** the same rows, order and values for every request shape, apart from changes made on purpose and listed. Back the parity numbers with a written argument for why results cannot differ. A speed-up never costs correctness.
- **Impact:** start with production evidence: slow/failing requests with tenants and filters they used, and limits that turn slowness into errors. Benchmark real shapes, not invented extremes.
- **Mechanism:** explain the gain from how the engine queries data from first principles of the query. Put one mechanism in each PR and stack the related ones.
- **Understanding:** the owner can say what every CTE or step does for the business, can explain each edge case with an example from the data, and can sum up the change in one plain sentence.

## Checks

- **Parity:**
  - Render both versions' SQL through the real query builders and callers, not hand-copied SQL. Run the old version from the base branch.
  - Run both on real data. Compare row membership, order and every field.
- **Coverage:** review parity and correctness in every caller and filter path.
- **Refactors:** rendered SQL and parameters stay identical across a grid of request shapes. Any SQL change moves to its own stacked PR, which is verified on its own.
- **Benchmark:**
  - Check small cases too: a win on large inputs can regress on small ones.
  - Re-run the full parity check and benchmark after successive meaningful code changes.
- **Tests:** live database tests should be scaled down to capture correctness and regressions, not to mimic live traffic.
- **Safety:** use read-only credentials, memory and time caps, query cache off, and no concurrent benchmarks on a shared host. Confirm exploratory queries touch only the intended data before running at scale.

## Reporting

Show how the engine ran the old query and runs the new one, a before-and-after chart of rows, bytes, memory and time, the argument for unchanged results, and who hit the problem in production. List gaps that existed before the change under "Not changed here".
