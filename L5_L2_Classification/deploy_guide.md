# Deploy Guide — dashboard-analytics
**Platform:** Anticloud sovereign infrastructure | Air-gap capable
**Stack:** Python 3.11, FastAPI, HTMX, Chart.js (local), SQLite, AIOSS_FORMAT

## Prerequisites
Python 3.11+. See stack: Python 3.11, FastAPI, HTMX, Chart.js (local), SQLite, AIOSS_FORMAT. AIOSS_FORMAT required. PAX 27B weights for AI-assisted features.

## AIOSS Integration
```bash
aioss init --module dashboard-analytics --output ./dashboard_analytics.aioss
aioss append --chain ./dashboard_analytics.aioss --payload ./output.bin --module dashboard-analytics
aioss verify --chain ./dashboard_analytics.aioss
```

## Air-Gap Deployment
```bash
# On networked machine:
pip download -r requirements.txt -d ./wheels/
# Transfer wheels/ to air-gap host, then:
pip install --no-index --find-links ./wheels/ -r requirements.txt
```

## PAX 27B Harness Wiring
```python
from anticloud_pax import PAXHarness
harness = PAXHarness(
    model_path="./pax-27b-q4.gguf",
    module="dashboard-analytics",
    aioss_chain="./dashboard_analytics.aioss",
    classification="L5_NARROW_L2_GENERAL"
)
result = harness.process(input_data)
```

## Verification
```bash
aioss verify --chain ./dashboard_analytics.aioss --verbose
python -m dashboard_analytics.tests.smoke
```
