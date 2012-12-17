---
layout: post
title: "Arquillian Persistence Extension - JPA testing without pain"
date: 2012-11-14 23:18
comments: true
categories: arquillian ape testing jee
published: false
---

### Should it be really that hard?
<!-- this goes as slide -->

* highlight problems I've seen a lot in the projects
	* seeding database
	* building test fixture
	* wrapping in transaction
	* comparing state of the database with the expect set of data

<!-- 
	live coding // using forge to tame myths that it's complex
		- forge build project + add arquillian
		- make domain model (beer many-to-one brewery)
		- dao
		- ? maybe arquillian eclipse plugin ?
		- start writing test (the naive way)
			!!! look at the current test and start coding it to conclude that we have put shit load of effort resulting in a bit brittle and not flexible test structure
		- first thing - extract test data (now mention YAML, XML, Excel and JSON)
		- seeding options
		- transactions // also demonstrate options
		- comparing data sets with db [+ exclusion ]
		- we can control cache eviction [extra]
-->

### What is Arquillian Persistence Extension

* Inspired by Unitils and DBUnit brings database control for your tests running in the container
* Wrapping each test in the seperated transaction (with **commit**(default) or **rollback** at the end).
* Seeding database using:
    * [DBUnit](http://dbunit.org) with **XML**, **XLS**, **YAML**  and **JSON** supported as data sets format.
    * Custom SQL scripts.
* Comparing database state at the end of the test using given data sets (with column exclusion).
* Eviction JPA second level cache between test method invocation, see `@JpaCacheEviction`.


### What's coming? 
<!-- this goes as slide -->

* Support for NoSQL databases (thanks to Alex Soto contribution!!!)
* Data providers (similar in concept to TestNG), so you can define your test fixtures in the type safe manner using builders etc.
* Fluent api alternative (providing the same stuff as annotations)
* Forge support