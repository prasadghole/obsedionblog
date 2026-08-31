---
title: "Python for embedded software modelling"
date: 2022-07-06
tags: []
publish: true
---

# Why Python?
Quick prototyping and availability of rich library set makes easy to model
embedded software in python. Current scope of this blog post is to modelling
embedded software and not embedded system.

# Architectural patterns
[pypubsub](https://pypubsub.readthedocs.io) is suitable for simulating decoupled
system using observer pattern. Hierarchical topic pattern gives more structured
view to design and build decoupled system.

[rxpy](https://rxpy.readthedocs.io/en/latest/) is more natural pattern for 
modelling embedded systems as it a reactive framework.

# Basic building blocks
Below sections I am exploring many alternative approaches, which may not bind
to above mentioned Architectural patterns. 

## Timers
This is most fundamental unit of embedded system. On windows OS we can use
win32event module to generate timing events. Based on these events as basic
timer tick we can run or simulate the embedded system.

We need to use thread and win32event to create an actor which will wait for
timer event and execute function or in case of reactive system emit message.

```python

fromm threading import Thread
import win32event

class TimerEventGenerator(Thread):
  def __init__(self,period):
    super(TimerEventGenerator,self).__init__()
    self.period = period
    self.event = win32event.CreateWaitableTimer(None,False,None)
    self.stoprequest = False

  def Start(self):
    win32event.SetWaitableTimer(self.event.handle,0,self.period,None,None,None)

  def run(self):
    while not self.stoprequest:
      win32event.WaitForSingleObject(self.event.handle,self.period)
      print("Do your work")ku

t = TimerEventGenerator(1000)

t.start()


```
