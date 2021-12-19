---
title: Lessons from Acquisition Migration
date: 2021-12-08
categories: ["programming"]
---

Recently for a client we needed to migrate users from their system to ours. There were a lot of lessons learned: 
 * Engineering team should know what data is needed to create records in specific state (e.g. user name, email, etc.)
 * Data obscuration is a must
 * System should not allow for data to exist in "wrong" state (database constraints, validations etc)
 * Migration script should be validated from database perspective as much as from UI perspective.
 * 
 * 