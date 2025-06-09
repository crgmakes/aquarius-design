# Product Requirement Document

This is the PRD for Aquarius. 

## Overview

Aquarius is a hardware and software suite that simplifies the task of automating your workshop. 

Aquarius can be used to automate just about anything, not just workshops.

## Goals

+ Inexpensive and approachable
+ Small form factor; sleek and unassuming
+ Easy to set up; easy to use
+ Self contained by default (no additional parts required)
+ Easily configurable for many tasks
+ Easily expandable; add new node with mininal work
+ Plug and play for new modules and peripherals
+ Open hardware and open source

## Non-Goals

+ Support for other wireless protocols such as NRF24, LORA, etc.
+ Production workshops
+ 3 Phase
+ More than 30A tools

## Audience

Aquarius is designed and built for the hobbyist, weekend warrior, up to mid-scale woodworker in a small to medium sized shop.

Targeted at saving the wood worker time and increasing the long-term safty of the shop by automating tasks that are burdensome or forgetful for the user (e.g., turning on the dust collector for every cut).

Time is money and being able to quickly get the capability installed and running without issues is paramount.

The average user is not highly technical and does not undestand computers or networking.
Simplisity and reliability are critical for the user.

## Existing solutions and issues

There are few options on the market to today. Two primary options come to mind. Both are relatively user friendly, but are very limited in capabilies and are costly.

- iVac
  - Super simple - plug in and go
  - Configure is manual through dip switches
  - No useful feedback while using
  - Expensive to scale
  - Very limited options - switch, remote, and distance sensor
  - Not hackable/modifiable

- Grit Automation
  - Highly configurable
  - Hub and spoke model
  - Fully comprehensive suite of tools
  - Mobile app
  - Targeted at higher end shops with asset management, multi-users
  - Very expensive
  - Not hackable/modifiable

## Assumptions

- Users would use dust collection more if it's automated
- Users are more concerned with their long-term health more now than ever
- Cost is a barrier to entry for existing solutions
- Users want plug and play without any hassle
- Most users are not computer literial or highly technical
- Most users are 30-70 in age; half are older than 45
- Some users want to hack the device and make it do things it was not designe to do
- Most users want an out-of-the-box experience
- Some users want kits or just the hardware

## Constraints

The machine should be easy to use, highly reliable, and support a wide range of configurations. Constraints include:

- Each device should be less than $50; ideally less than $30.
- User interface should be large and easily readable
- Some units will not be physically accessible and must be administered remotely
- Device will be in a high EMI environment with significant electrical noise
- Device must support standard 120v 15A as well as 20A, 220v 10A, 15A, and 20A tools
- Must be capable of using existing blast gates on market with easy modification
- No rewiring of tools or shop electrical modification required
- Must be capable of triggering non-Aquarius devices via IR and RF

## Key Use Cases

### 5 Minute Install

An average user should be capable of getting up and running within 5 minutes of unboxing. The default configuration of the product should simple work out of the box for at least one peripheral.

### Simple yet Complex

An industrious user should be able to create very complicated and complex routines with little effort.

A single "start" routine and a single "stop" routine should be able to control everything a user needs.

### Highly Configurable

A single node should be configurable via software to be any peripheral or multiple peripherals. Nodes within the system should be notified of new features and peripherals and allow the user to adapt or control the newly added features from the UI.

### Web Enabled

The solution should have an open API that allows any application to control the system remotely. Features include:
- Setting parameters
- Sending commands
- Getting status

> ## Research

> This section outlines any research questions that helped inform how this PRD was written. Although at the end, this section **must be completed before the PRD is written**, as it fully informs what the product is.

> ### User Research

> This section should inform the vast majority of the rest of this document. It should be in the format of a few key questions as headers that will inform how you build your product, with an answer based on your research below.

> This entire section should contain links to notes from interviews you've performed with current or potential customers.

> Example:

> ### How important is speed?

> The speed of the machine (usually referred to in Sandwiches Per Hour, or SPH) is the core metric of a sandwich assembly machine. Our users are mostly using their machines to assemble sandwiches for their sandwich shop, so making sure the machine can keep up with demand is critical for them.

> From [many]() [interviews]() [with]() [customers](), it seems we need to hit about 20 SPH to fulfill the demands of their production. After around 20 SPH, the bottleneck becomes how quickly their counter clerks can take the order and handle the customer's payment. To safely cover almost all customer use cases, we'll ensure we can make at least 25 SPH. Anything beyond that is great, but not a requirement.

> ### Technical Research

> This section should inform the the rough structure of how your product will be built. Math, component spec research, and even some quick prototypes might be required to complete this section.
