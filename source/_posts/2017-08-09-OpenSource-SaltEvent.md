---
title: "saltstack event system笔记"
date: 2017-08-09 08:00:00
updated: 2017-08-07 16:26:09
tags: ["Saltstack"]
---
**• 深度了解事件系统（event system）。**
  
Salt 基于消息队列（message queue）构建。命令首先由 Master 产生任务（job）并推送到队列中。Minion监听队列中能够匹配到自己的任务。当 Minion 获取到一个任务时，会尝试执行和自己相关联的任务。一旦任务完成，会将任务的执行结果发送到另外一个Master 监听的队列。
  
Minion 并不是只能处理由 Master 产生的任务，自身也具有发送（fire）消息的能力。这些信息块就构成了基本的事件总线（event bus）。
  
事实上有两个事件总线：一个是 Minion 内部沟通（并不能和其他 Minion 通信）的总线，另一个是 Minion 和 Master沟通的总线。Minion 的事件总线目前应用在 Salt 内部，只用于自身内部产生事件使用。当然也允许用户手动或甚至编程地在 Minion消息总线上发送消息（firemessage），但对于用户来说并没有内置直接的高级用法。
  
Master事件总线则完全不同。Minion发送消息到Master的能力是很强大的，尤其是Master结合反应器系统（Reactor system），我们将在稍后详细介绍它。
![blob.png](/uploads/ueditor/php/upload/image/20170807/1502087899.png)
  
**• 理解反应器（Reactor）系统。**
  
  
**• 构建更复杂的反应器（Reactor）。**
  
  
**• 使用队列系统（queue system）。**
  
  
  
