---
description: Hide low-value messages from AI context to free context window
---
Free up context window by hiding messages no longer needed to continue the current work.

1. Inspect all messages:
```python
from dialoghelper import *
msgs = await find_msgs()
for m in msgs: print(m['id'], m.get('type',''), repr(str(m.get('content',''))[:100]))
```

2. Identify low-value messages. Good candidates:
   - Superseded exploratory attempts
   - Verbose raw outputs already discussed
   - Failed intermediate debugging steps
   - Long install/setup cells whose results are stable

   Always keep: current working code, open errors, active decisions, recent context.

3. Hide them with retry logic (`update_msg` can occasionally fail on bulk ops):
```python
async def hide(mid):
    for _ in range(3):
        try: return await update_msg(mid, skipped=1)
        except: pass
    print(f"failed: {mid}")

for mid in [...]:  # fill in selected IDs
    await hide(mid)
```

4. Report how many were hidden and estimate context saved.

$ARGUMENTS
