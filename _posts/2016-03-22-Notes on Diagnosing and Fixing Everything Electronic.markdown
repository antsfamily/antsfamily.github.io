---
layout: post
title: Notes on Diagnosing and Fixing Everything Electronic
date: 2016-03-22 15:32:24.000000000 +09:00
---


[TOC]

# 前言

本人维修的一点经验记录。

维修的意义是什么呢？"How to Diagnose and Fix Everything Electronic - by Michael Jay Geier"（[book_how](book_how "How to Diagnose and Fix Everything Electronic - by Michael Jay Geier")）这本书中给出了参考：

> - *It might be easier*, but it's usually not cheaper! Sans the cost of labor, repair can be quite cost effective. There are lots of other good reasons to become a proficient technician, too: ? 
- *It's fun*. You'll get a strong sense of satisfaction when your efforts yield a properly working gadget. It feels a bit like you're a detective solving a murder case, and it's more fun to use your noodle than your wallet.
- *It's absorbing*. Learning to repair things is a great hobby to which you can devote many fruitful hours. It's good for your brain, and it beats watching TV any day (unless you fixed that TV yourself!).
- *It's economical*. Why pay retail for new electronics when you can get great stuff cheap or even free? Especially if you live in or near a city, resources like craigslist.org will provide all the tech toys you want, often for nothing. Lots of broken gadgets are given away, since bringing them in for repair costs so much.
They're yours for the taking. All you have to do is fix 'em! 
- *It can be profitable*. Some of the broken items people nonchalantly discard are surprisingly valuable. When your tech skills become well developed, you'll be able to repair a wide variety of devices and sell what you don't want for yourself.
- *It can preserve rare or obsolete technology*. Obsolete isn’t always a negative term! Some older technologies were quite nice and have not been replaced by newer devices offering the same features, utility or quality. The continued zeal of analog audio devotees painstakingly tweaking their turntables offers a prime example of the enduring value of a technology no longer widely available.
- *It's green*. Every product kept out of the landfill is worth two in ecological terms: the one that doesn't get thrown away and the one that isn't purchased to replace it. The wastefulness of tossing out, say, a video projector with a single capacitor is staggering. To rip off an old song, “Nothing saves the green'ry like repairing the machin'ry in the morning….”
-  *Your friends and family will drive you crazy*. Being a good tech is like being a doctor: everyone will come to you for advice and help. Okay, maybe this one isn't such an incentive, but it feels great to be able to help your friends and loved ones, doesn't it? Being admired as an expert isn't such a terrible thing either.


可见，这涉及到经济、环境（绿色）、学习、乐趣、保护稀有技术、潜在的收益等等。乐趣在于你努力过后装置正常工作，所带给你的强烈满足感与成就感，毕竟动一动脑子比挥一挥皮夹更有趣！这就像亲手为心爱的女孩做花要比买得更让自己刻骨铭心！


# 心得

## 检修步骤

-	先检查外观，如电源线及插头有无烧焦或断裂。若有则修复，然后进入下一步；无则进行下一步。
-	拆机，观察电路板及元器件，看有无损坏现象，如：电路板折断、保险丝熔断、电阻发黑、电容鼓起、焊点脱落等。
-	用万用表欧姆档最高档测试输入端电阻，应较大，再测试输出端电阻，应较小。
-	根据上步结果，观察电路板，锁定可能坏的元件，进行检测。若坏则予以更换。确保所有元件均完好后，进入下一步。
-	通电检查，若仍不能正常工作，则应先检测电源供应部分，若电压与标准值相差较大，则应先维修电源模块。否则测试其它模块电压。


# 实录


## 电磁炉

**故障现象**：开机无任何反应
**维修日期**：2014年寒假

**检测与分析**：数字式万用表，二极管档，可以在板初步检测出：保险丝、IGBT、整流桥已坏。但是什么原因导致这三个元件损坏呢？仔细观察线路板，发现一个个头大的电容的引脚已经脱离板子（焊接有问题），是它造成的。

**损坏元件**：保险丝（熔断）、IGBT（击穿）、整流桥（击穿）

补焊电容引脚并更换损坏元件后正常工作至今。


## 卫星机顶盒

### 卫星机顶盒

**故障现象**：开机无反应
**维修日期**：2014年暑假

**检测与分析**：询问了具体情况，得知暴风雨晚打雷打闪后，出现此故障，于是猜测是雷电带来的点击损坏。首先怀疑电源模块有问题，在确定电路中无明显元件损坏、电路没有短路的前提下，从其它正常机顶盒上取下电源小板，试机正常！故更换电源小板，淘宝有售，10元左右。

### 机顶盒&遥控器

**故障现象**：按任意键，无任何反应。
**维修日期**：2014年寒假

**检测与分析**：使用手机摄像头检测遥控器，正常，怀疑是机顶盒接收电路已坏。然而，检测机顶盒后，发现接收头输出端电压随遥控按键按下变化，单片机输入脚电压也变化。后来，用万能遥控器，成功实现遥控。


## 数码播放器

**故障现象**：扬声器正常，插入耳机耳机无声音，调大音量，耳机扬声器同时有声
**维修日期**：2016年3月21

**检测与分析**：

- **拆机**：这个机器稍微有点难拆。背部1颗螺丝钉，前部数码管保护罩下一枚，扬声器防尘防护网罩下5颗，不对，是六颗，哈哈，见图：
![扬声器防尘防护网罩下5颗](http://img.blog.csdn.net/20160704120039641)
![不对，是六颗，哈哈](http://img.blog.csdn.net/20160704120211817)

- **检修**：经观察发现无明显元器件损坏，于是上网查原理电路，了解到，数码播放器有静音脚，耳机插入时，该引脚作用，紧接着微控制器控制关断音频功放输出（耳机功率小，不需要功放的，记得初中有个无需电池的收音机电路，直接利用无线电能量就能驱动耳机）。
![数码播放器原理框图](http://img.blog.csdn.net/20160322165131143 "数码播放器原理框图")

此款播放器，采用YX8002D单声道音频功放，4欧姆扬声器，没有查到该芯片资料，不过查到了TC8002D音频功放，完全兼容，如下图：
![数码播放器音频功放原理图](http://img.blog.csdn.net/20160322170058108 "数码播放器音频功放原理图")

补张耳机图以后备用：
![耳机结构图](http://img.blog.csdn.net/20160322170404018)

可见：对于含有4引脚的耳机母座，插入只有3极的耳机，相当于母座3、4脚同接GND，所以一般静音控制为低电平使能；美标耳机与国标耳机不应混用，虽然能够正常听音，当控制键和话筒不起作用或错乱。

*重点查耳机静音线、静音控制线、音频功放、主控*

经检测，无论插入耳机与否，音频功放8002D的关断脚（1脚）电压恒为$0V$，将8002D拆下后再检测，正常，故更换8002D。可惜西安中工、电子市场都跑了，没有，无奈只能淘宝（0.1~2.0￥不等）。

**损坏元件**：单声道音频功放8002D



# 参考资料

[book_how]: "How to Diagnose and Fix Everything Electronic - by Michael Jay Geier"


