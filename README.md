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
    task = self.loop.create_task(self.async_func())
    self.loop.run_until_complete(task)

thread = CustomThread()
thread.start()
```


<p>You should only ever use asyncio with QThreads when required</p>
<p>This example creates three threads - main stack, QThread, and asyncio loop</p>
<p>An example of use with async tasks is websockets / tcp communications</p>
<p>An ideal scenario is no QThread dependencies, and Python to refine it's async implementations</p>
