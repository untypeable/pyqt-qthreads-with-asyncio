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


<span>Only use asyncio and QThreads when absolutely required.</span><br />
<span>The example creates three threads: Main Stack, QThread, and Event Loop.</span><br />
<span>There is no need for asyncio.run if we create and manage our own event loop.</span><br />
<span>Setting the event loop in main stack will allow QThreads to await eachother.</span><br />
<span>QThreads suck and Python's asyncio is a lie.</span>
