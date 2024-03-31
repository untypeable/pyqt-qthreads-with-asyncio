# Qt QThreads with Python asyncio
A demonstration of implementing async methods to Qt QThreads

```
from PyQt6.QtCore import QThread
import asyncio

asyncio.set_event_loop(asyncio.new_event_loop())

class CustomThread(QThread):
  def __init__(self):
    self.loop = asyncio.get_event_loop()
    QThread.__init__(self)

  async def async_func(self):
    print("ASYNC HELLO :)")

  def run(self):
    asyncio.set_event_loop(self.loop)
    asyncio.run(self.async_func())
    self.loop.run_forever()

thread = CustomThread()
thread.start()
```


<p>You should only ever use asyncio with QThreads when 100% required.</p>
<p>This example creates three threads - main stack, dummy thread (qthread), and asyncio</p>
<p>An example of required use would be an application with ASYNC tasks, like websockets</p>
