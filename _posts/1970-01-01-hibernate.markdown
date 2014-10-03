---
layout: post
title:  "Hibernate"
date:   2014-10-03 20:59:15
categories: public
---

#### Enable Hibernate SQL logging on runtime
Set a breakpoint somewhere. In the breakpoint, evaluate following expression in your IDE.

`Logger.getLogger("org.hibernate.SQL").setLevel(Level.DEBUG)`