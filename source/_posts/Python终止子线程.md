---
title: Python终止子线程
url: 353.html
id: 353
categories:
  - Linux &amp; VPS
date: 2019-04-21 23:12:19
toc: true
tags:
---

### 利用event()

    import threading
    
    class StoppableThread(threading.Thread):
        """Thread class with a stop() method. The thread itself has to check
        regularly for the stopped() condition."""
    
        def __init__(self):
            super(StoppableThread, self).__init__()
            self._stop_event = threading.Event()
    
        def stop(self):
            self._stop_event.set()
    
        def stopped(self):
            return self._stop_event.is_set()