# Orbit Scheduler: architecture and boundaries

## Responsibility

`orbit-scheduler` is an optional, provider-neutral in-process scheduler for bounded asynchronous
interval jobs. It is separate from Orbit Core, whose lifecycle and request timeouts continue to
govern the application. The package supports Python 3.11 through 3.14 and is pre-alpha.

```bash
python -m pip install orbit-scheduler
```

## Declared dependencies

The following dependency declarations come from the checked-in manifests. Optional groups and development dependencies are called out separately.

### `pyproject.toml`
- No dependencies declared.
- Optional `dev` group: `pytest>=8,<10`, `pytest-asyncio>=0.24,<2`, `ruff>=0.8,<1`, `mypy>=1.13,<2`.

Declared dependencies do not mean that optional providers or services are bundled with this package.

## Implementation layout

Representative implementation files in this checkout:

- `src/orbit_scheduler/__init__.py`
- `src/orbit_scheduler/scheduler.py`

## Public contract and scope

The README does not contain a separately headed architecture section. Its responsibility statement above and the public source files define the implemented scope; this guide adds no behavior beyond that description.

## Boundary rules

Keep provider SDKs, credentials, transports, and provider-specific error translation in provider adapters. Keep reusable capability contracts in the matching capability package and lifecycle orchestration in Core. Apply the relevant layer for this repository and preserve the dependency direction shown above.
