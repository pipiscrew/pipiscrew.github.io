---
title: Task Scheduler repeat task not triggering
author: PipisCrew
date: 2019-03-11
categories: [news]
toc: true
---

It seems that repeated tasks are not executed when run manually (right click on a task and then select "Run").

When run manually, the task will run only once and that's it!

This is a trip wire since it's natural that people simply run the task manually right after its creation to check whether it's working as expected.

What you could do, set the trigger to "At startup". After you rebooted the machine, the task should then be in the "Queued" status. This means it will run at the configured interval.

--

A better solution is to check 'Run task as soon as possible after a scheduled start is missed' with whatever trigger you want (time based, etc). Then it should start running automatically on schedule as expected

src - https://superuser.com/a/896413

origin - https://www.pipiscrew.com/?p=14761 task-scheduler-repeat-task-not-triggering