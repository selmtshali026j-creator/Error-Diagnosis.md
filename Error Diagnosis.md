



**Error Description:**
`IndexError: list index out of range` 
This means the code tried to access an item in the list using an index that doesn't exist. The traceback shows it happened on line 10 in `print_inventory_report` when trying to do `items[i]`.

**Root Cause:**
The for loop uses `range(len(items) + 1)`. 
If `items` has 3 elements, `len(items)` = 3. `range(3 + 1)` = `range(4)` which gives indexes 0, 1, 2, 3.
But a list with 3 items only has valid indexes 0, 1, 2. When `i = 3` the code tries to access `items[3]` which doesn't exist, so Python throws IndexError.
This is a classic "off by one" error.

**Solution:**
Remove the `+ 1` from the range.
```python
def print_inventory_report(items):
    print("===== INVENTORY REPORT =====")
    # Fixed: removed the + 1
    for i in range(len(items)):
        print(f"Item {i+1}: {items[i]['name']} - Quantity: {items[i]['quantity']}")
    print("============================")
Note: We keep `i+1` in the print statement so it still displays "Item 1, Item 2, Item 3" to the user.

*Learning Points:*
1. *Python lists are 0-indexed*: A list with length `n` has indexes from `0` to `n-1`
2. *`range(len(items))` is the safe pattern* for looping through a list by index
3. *Better practice*: Avoid indexing when possible. Use `for item in items:` instead to prevent off-by-one errors entirely:
    for idx, item in enumerate(items):
        print(f"Item {idx+1}: {item['name']} - Quantity: {item['quantity']}")
4. *Always test edge cases*: Try with 0 items, 1 item, and many items.

*Reflection:*
1. *AI vs Docs*: The AI explained both the traceback AND why `+1` was wrong. Docs just define IndexError. AI connected it to the code.
2. *Hard to diagnose manually*: If you didn't see the `+1`, you might think the list is empty. The stack trace points to the line but not the logic error.
3. *Better error messages*: Add a guard clause: `if not items: print("No items to report")` and use `enumerate` instead of manual indexing.
4. *AI helped with concepts*: It explained 0-indexing and suggested `enumerate`, not just "delete +1".
