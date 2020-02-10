title: Python下使用多线程的两种方式
url: 351.html
id: 351
categories:
  - Python
tags: []
date: 2019-04-21 23:11:00
---
## 1.继承threading类，重写run()函数

    import threading 
    import time
    class timer(threading.Thread): #继承threading.Thread类
        def __init__(self, num, interval): 
            threading.Thread.__init__(self) 
            self.thread_num = num 
            self.interval = interval 
            self.thread_stop = False 
    
        def run(self): #Overwrite run() method, put what you want the thread do here 
            while not self.thread_stop: 
                print &#039;Thread Object(%d), Time:%s\n&#039; %(self.thread_num, time.ctime()) 
                time.sleep(self.interval) 
        def stop(self): 
            self.thread_stop = True
    def test(): 
        thread1 = timer(1, 1) 
        thread2 = timer(2, 2) 
        thread1.start() 
        thread2.start() 
        time.sleep(10) 
        thread1.stop() 
        thread2.stop() 
        return 
    
    if __name__ == &#039;__main__&#039;: 
        test()