# Orbit Scheduler: operations and security

This guide organizes runtime behavior documented by the package. It does not certify production readiness. Verify provider/client versions, permissions, transport security, limits, and failure behavior in the target environment before release.

## Configuration surface

Environment names found in the package README:

The package README does not name `ORBIT_*` variables. Use its typed constructors and application configuration, and confirm exact runtime inputs in the implementation before deployment.

Use the package README's constructor and deployment examples. Store credentials in a secret manager and avoid logging credentials, raw provider errors, request data, or opaque cursors.

## Lifecycle, failure behavior, and limits

`orbit-scheduler` is an optional, provider-neutral in-process scheduler for bounded asynchronous
interval jobs. It is separate from Orbit Core, whose lifecycle and request timeouts continue to
govern the application. The package supports Python 3.11 through 3.14 and is pre-alpha.

```bash
python -m pip install orbit-scheduler
```

## Delivery and deployment limits

Schedules and run state exist only in this process. A restart loses schedules; multiple workers each
run their own copy. The package does not provide cron/time-zone rules, persistence, leader election,
distributed locks, retries, durable delivery, or execution guarantees. Do not use it for work that
must survive process failure or must run exactly once across workers. Those needs require a separate
durable scheduler/worker backend and an adapter that defines its delivery and acknowledgement
semantics.

## Production validation

Validate startup/shutdown cleanup, timeout and cancellation behavior, concurrency and payload bounds where applicable, secret rotation and least-privilege access, data durability, backup/restore, and failover against the selected provider. Do not infer distributed or durable guarantees from an in-process API or fake-client tests.
