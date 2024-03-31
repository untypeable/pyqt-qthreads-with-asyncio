# Qt QThreads with Python asyncio
A demonstration of implementing async methods to Qt QThreads

```
from PyQt6.QtCore import QThread
import asyncio

class CustomThread(QThread):
  def __init__(self):
    self.loop = asnycio.get_event_loop()

  async def async_func(self):
    print("ASYNC HELLO :)")

  def run(self):
    asyncio.set_event_loop(self.loop)
    asyncio.run(self.async_func())
    self.loop.run_forever()
```
