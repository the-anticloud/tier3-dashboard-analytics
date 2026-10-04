# Developer Cookbook — dashboard-analytics
**Stack:** Python 3.11, FastAPI, HTMX, Chart.js (local), SQLite, AIOSS_FORMAT
**Domain:** Sovereign web dashboard: real-time visualization of Anticloud metrics and AIOSS chain
**License:** Apache-2.0 | **IP:** USPTO pending 2026, Anticloud FZ LLE

## Core Usage

```bash
python -m dashboard_analytics --port 8090 --aioss ./dashboard.aioss
# Open http://localhost:8090
# Displays: tok/s, AIOSS chain growth, compliance status, GPU utilization
# NL query: 'Why did latency spike at 14:23 today?'
# PAX response: 'Chain append to audit.aioss blocked for 847ms due to concurrent writes'
```

## AIOSS Chain Append

```python
import hashlib, time

def aioss_append(chain_path, payload: bytes, module_id: str):
    entry_hash = hashlib.sha3_256(payload).digest()
    ts = int(time.time_ns()).to_bytes(8, 'big')
    with open(chain_path, 'rb') as f:
        f.seek(-32, 2); prev_hash = f.read(32)
    new_hash = hashlib.sha3_256(prev_hash + entry_hash + ts).digest()
    with open(chain_path, 'ab') as f:
        f.write(ts + entry_hash + new_hash)
    return new_hash.hex()

# After every dashboard-analytics output:
chain_hash = aioss_append("./dashboard_analytics.aioss",
                           result_bytes, "dashboard-analytics")
```

## Performance & Integration

Performance: profile with api-oss-devtools. Benchmark with api-oss-analytics. Integration: all dashboard-analytics operations are logged to api-oss-logging and audited by api-oss-compliance.
