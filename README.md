Knetik Architecture Test
==================================

Thank you for taking the time to do our architecture test. Feel free to use markdown or the github wiki to document your plan.  Please read through the scenario carefully:

## Scenario

We are partnered with a company that provides smart thermostats. The "kits" we received consist of a couple things:
- A gateway used to connect to the internet via WiFi or direct connect
- A thermostat to manage temperature (obviously)

The gateway and the thermostat talk through radio frequency and allows the thermostat to send and receive command through the cloud. You can have many thermostats to one gateway.  The partner has a simple API that allows us to set the mode (heating/cooling), a desired temperature on the thermostat and a variety of other things that are out of scope for this test. The kits are identified by a serial number in the vendor API. Ex: PUT https://theprovider.com/cloud/ABC123 {"target": 75}.

We want to build a simple app that enables the control of a thermostat, but with a twist:
- The thermostat settings can be overridden by a thermostat "admin"
- The ability to add more thermostat providers with similar APIs in the near future

The CEO is asking for a plan and estimate on the first version as he would like to start development ASAP. You have 2 full-stack developers at your disposal.

## Deliverables
- Brief outline of milestones
- Technologies used to achieve the goal
- Overall architecture of the system

#### Thanks for your time, we look forward to hearing from you!
- The [Knetik Tech team](http://github.com/knetikmedia)
