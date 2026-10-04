# Small checkout service

Python 3.11+; runtime uses only the standard library. Amounts are integer cents.
Install the pinned test dependency from `requirements-dev.txt`, then run
`python -m pytest`. The public modules are `orders`, `pricing` and `checkout`.

```python
from checkout import render_receipt

print(render_receipt("R-1", [("pen", 2, 125)], member=True))
```

`orders.normalize_items` validates and snapshots item triples. `orders.subtotal`
returns their undiscounted value; `orders.summarize` adds a quote.
`pricing.quote` applies a 10% member discount rounded down, then free shipping
at a discounted subtotal of 5,000 cents. Other nonempty baskets pay 499 cents.
Empty baskets have zero totals. Receipt lines retain item order and duplicates.
