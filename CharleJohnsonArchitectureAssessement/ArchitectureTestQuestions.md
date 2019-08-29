# Architecture Test Questions

<h2> Scenario </h>

We are partnered with a company that provides smart thermostats. The "kits" we received consist of a couple things:

-   A gateway used to connect to the internet via WiFi or direct connect
-   A thermostat to manage temperature (obviously)

The gateway and the thermostat talk through radio frequency and allows the thermostat to send and receive command through the cloud. You can have many thermostats to one gateway. The partner has a simple API that allows us to set the mode (heating/cooling), a desired temperature on the thermostat and a variety of other things that are out of scope for this test. The kits are identified by a serial number in the vendor API. Ex: PUT  [https://theprovider.com/cloud/ABC123](https://theprovider.com/cloud/ABC123)  {"target": 75}.

We want to build a simple app that enables the control of a thermostat, but with a twist:

-   The thermostat settings can be overridden by a thermostat "admin"
-   The ability to add more thermostat providers with similar APIs in the near future

The CEO is asking for a plan and estimate on the first version as he would like to start development ASAP. You have 2 full-stack developers at your disposal.

<h2> Overall architecture of the system </h2>
You would need an application that is constantly running on a computer connected to the internet. This application would constantly, or at some determined time interval, ping the "admin" Thermostats for their settings and ping all the other Thermostats using the same gateway for their settings. If the non-admin Thermostats don't have the same settings as the Admin Thermostat, the application would change the settings. All this would be done through the API.
<p> The application would make calls to the vendor's web API using simple https requests. You would start with a base abstract class, lets call it ThermostatAPI, that would have abstract functions for things such as GetThermostat() or SetThermostatMode(). From there you would have a class that inherits, such as Vendor1API, from this base class that would implement the correct calls to the vendor's API. If a new vendor comes along the, a new inherited class could be created to implement their specific API.
<p>A Thermostat object would then include as part of their object a member variable that would allow the correct API to be used. For example, a Thermostat would have a string member named "Vendor" and a ThermostatAPI member named "API". Vendor would be set in the constructor of the Thermostat and when it would access "API" through a getter, a Vendor1API object will be returned if "Vendor" is set to "Vendor1", or a Vendor2API object would be returned if "Vendor" is set to "Vendor2", etc. That way, the rest of the Thermostat object's code you could just call API.SetTemperature() or API.GetStats(), and the correct API calls would be made. (The framework I made at General Dyanmics Information Technology was similar with returning specific WebRequestControllers, with WebRequestController as the abstract class, and Admin_WebRequstController and Reports_WebRequestController being the child classes of WebRequestController).
<p>The application would need a simple user-interface where each set of Thermostats can be viewed by their gateway, and so the admin can get set by selecting the serial number of the Thermostat you want to set as an admin, and even set the settings for either the admin Thermostat or any of the Thermostat from the application. A simple XML data file could be used to store the settings, unless we are thinking of having multiple user be able to monitor and edit settings, which I would suggest a lightweight SQL Database Server. A couple 2 or 3 tables should be all thats needed to manage the settings for the Thermostats.
<p> So the program would ping the Thermostats for their settings, if any Thermostats are admin and that gateway group is set to have the admin override the other Thermostats, then the program would make the API calls to set the settings of those Thermostats if the settings differ from the Admin.


<h2> Milestones </h2>
<ul>
<li>First Prototype - The Admin Thermostat serial number is hardcoded into the system and is in "admin-override" mode, so we can see the settings on the Thermostats change when the setting on the Admin Thermostat changes. </li>
<li> Second Prototype - Includes the user interface to set the settings for the Admin Thermostat remotely. <li>
Database Prototype - Database is designed so that settings can be saved for Thermostats and test out turning off "admin-override" mode. Application should interact with the database
<li> Base Abstract API Class Created and Vendor Specific Child Class Created - Make sure all API calls are implemented in their specific Vendor class instead of on the Thermostat Objects </li>
<li> Create a Second Vendor Specific Class - create a dummy if there is no second vendor. At this point we are making sure that added a new vendor's API can be done in as short of time as possible

	
</ul>

<h2> Technologies used to achieve the goal  </h2>
You'll need a desktop, or laptop computer connected to the internet to run the application once it's built. The application should ideally be built in Java or C#, depending on the programmer's flavor of code. Also a database, I prefer using a SQL database.

