# Warehouse tools

Small Python utilities for warehouse order and shipping workflows.

Run the tests with `python3 -m unittest discover -s tests -v`.

## Shipping

`shipping_quote(weight_kg, zone, service="standard")` returns a delivery quote
in dollars. Zones are `local` and `regional`; weights must be positive.
Standard shipping costs $5 locally or $8 regionally, plus $1.50 per kg.
Express shipping adds $7 for either zone. Quotes are rounded to two decimal
places. Unknown zones or services and nonpositive weights raise `ValueError`.
Omitting `service` preserves standard shipping.

```python
from warehouse.rates import shipping_quote

shipping_quote(2, "local")  # 8.0
shipping_quote(2, "local", service="express")  # 15.0
shipping_quote(2, "regional", service="express")  # 18.0
```

The command-line entry point prints a quote for an order. `--service` accepts
`standard` (the default) or `express`:

```sh
python3 -m warehouse.cli 2 local                    # $8.00
python3 -m warehouse.cli 2 regional --service express  # $18.00
```
