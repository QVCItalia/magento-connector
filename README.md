Mule Magento Cloud Connector
============================

Mule Cloud connector to Magento

Installation
------------

The connector can either be installed for all applications running within the Mule instance or can be setup to be used
for a single application.

*All Applications*

Download the connector from the link above and place the resulting jar file in
/lib/user directory of the Mule installation folder.

*Single Application*

To make the connector available only to single application then place it in the
lib directory of the application otherwise if using Maven to compile and deploy
your application the following can be done:

Add the connector's maven repo to your pom.xml:

    <repositories>
        <repository>
            <id>muleforge-releases</id>
            <name>MuleForge Snapshot Repository</name>
            <url>https://repository.muleforge.org/release/</url>
            <layout>default</layout>
        </repsitory>
    </repositories>

Add the connector as a dependency to your project. This can be done by adding
the following under the dependencies element in the pom.xml file of the
application:

    <dependency>
        <groupId>org.mule.modules</groupId>
        <artifactId>mule-module-magento</artifactId>
        <version>1.0-SNAPSHOT</version>
    </dependency>

Configuration
-------------

You can configure the connector as follows:

    <magento:config username="value" password="value" address="value"/>

Here is detailed list of all the configuration attributes:

| attribute | description | optional | default value |
|:-----------|:-----------|:---------|:--------------|
|name|Give a name to this configuration so it can be later referenced by config-ref.|yes||
|username||no|
|password||no|
|address||no|









Add Order Shipment Comment
--------------------------

Adds a comment to the shipment. 

Example:



     <magento:add-order-shipment-comment 
    			shipmentId="#[map-payload:shipmentId]" 
           	comment="#[map-payload:comment]" 
             sendEmail="true" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|shipmentId| the shipment's increment id|no||
|comment| the comment to add|no||
|sendEmail| if an email must be sent after shipment creation|yes|false|
|includeCommentInEmail| if the comment must be sent in the email|yes|false|

Add Order Shipment Track
------------------------

Adds a new tracking number

Example:



     <magento:add-order-shipment-track
    			shipmentId="#[map-payload:shipmentId]" 
    			carrierCode="#[map-payload:carrierCode]"
    		title="#[map-payload:title]" 
    		trackId="#[map-payload:trackId]" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|shipmentId| the shipment id|no||
|carrierCode| the new track's carrier code|no||
|title| the new track's title|no||
|trackId||no||

Cancel Order
------------

Cancels an order

Example:



     <magento:cancel-order
     	   orderId="#[map-payload:orderId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|orderId| the order to cancel|no||

Create Order Shipment
---------------------

Creates a shipment for order

Example:



     <magento:create-order-shipment 
    			orderId="#[map-payload:orderId]"
    			comment="#[map-payload:comment]">
    		<magento:itemsQuantities>
    			<magento:itemsQuantity key="#[map-payload:orderItemId1]" value="#[map-payload:Quantity1]"/>
    			<magento:itemsQuantity key="#[map-payload:orderItemId2]" value="#[map-payload:Quantity2]"/>
    		</magento:itemsQuantities>
    	</magento:create-order-shipment>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|orderId| the order increment id|no||
|itemsQuantities| a map containing an entry per each (orderItemId,
           quantity) pair|no||
|comment| an optional comment|yes||
|sendEmail| if an email must be sent after shipment creation|yes|false|
|includeCommentInEmail| if the comment must be sent in the email|yes|false|

Get Order
---------

Answers the order properties for the given orderId

Example:



      <magento:get-order orderId="#[map-payload:orderId]" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|orderId| the order whose properties to fetch|no||

Get Order Invoice
-----------------

Retrieves order invoice information

Example:



      	<magento:get-order-invoice invoiceId="#[map-payload:invoiceId]"  />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|invoiceId||no||

Get Order Shipment Carriers
---------------------------

Creates an invoice for the given order

Example:



      <magento:get-order-shipment-carriers  orderId="#[map-payload:orderId]"  />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|orderId||no||

Get Order Shipment
------------------

Adds a comment to the given order's invoice

Example:



      <magento:get-order-shipment 
    			shipmentId="#[map-payload:orderShipmentId]" /> 

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|shipmentId||no||

Hold Order
----------

Puts order on hold

Example:



      <magento:hold-order orderId="#[map-payload:orderId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|orderId||no||

List Orders
-----------

Lists order attributes that match the 
given filtering expression

Example



     <magento:list-orders 
    			filter="gt(subtotal, #[map-payload:minSubtotal])"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|filter||yes||

List Orders Invoices
--------------------

Lists order invoices that match the given filtering expression

Example:



     <magento:list-orders-invoices filter="notnull(parent_id)" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|filter||yes||

List Orders Shipments
---------------------

Lists order shipment atrributes that match the given 
optional filtering expression

Example:



     <magento:list-orders-shipments filter="null(parent_id)" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|filter||yes||

Delete Order Shipment Track
---------------------------

Deletes the given track of the given order's shipment

<magento:delete-order-shipment-track
	shipmentId="#[map-payload:shipmentId]" trackId="#[map-payload:trackId]" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|shipmentId| the target shipment id|no||
|trackId| the id of the track to delete|no||

Add Order Comment
-----------------

Adds a comment to the given order id



     <magento:add-order-comment 
    				orderId="#[map-payload:orderId]"
    			status="#[map-payload:status]" 
    			comment="#[map-payload:comment]" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|orderId| the order id|no||
|status| TODO possible values?|no||
|comment||no||
|sendEmail| if an email must be sent after shipment creation|yes|false|

Unhold Order
------------

Releases order

Example:



      <magento:unhold-order orderId="#[map-payload:orderId]" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|orderId||no||

Create Order Invoice
--------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|orderId||no||
|itemsQuantities||no||
|comment||yes||
|sendEmail||yes|false|
|includeCommentInEmail||yes|false|

Add Order Invoice Comment
-------------------------

Adds a comment to the given order's invoice

Example: 



      <magento:add-order-comment 
    			orderId="#[map-payload:orderId]"
    			status="#[map-payload:status]" 
    			comment="#[map-payload:comment]" 

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|invoiceId| the invoice id|no||
|comment| the comment to add|no||
|sendEmail| if an email must be sent after shipment creation|yes|false|
|includeCommentInEmail| if the comment must be sent in the email|yes|false|

Capture Order Invoice
---------------------

Captures and invoice

Example: 



      <magento:capture-order-invoice invoiceId="#[map-payload:invoiceId]"  />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|invoiceId| the invoice to capture|no||

Void Order Invoice
------------------

Voids an invoice

Example: 



      <magento:void-order-invoice invoiceId="#[map-payload:invoiceId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|invoiceId| the invoice id|no||

Cancel Order Invoice
--------------------

Cancels an order's invoice

Example: 



      <magento:cancel-order-invoice invoiceId="#[map-payload:invoiceId]"  />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|invoiceId| the invoice id|no||

Create Customer Address
-----------------------

Creates a new address for the given customer using the given address
attributes



     <magento:create-customer-address customerId="#[map-payload:customerId]"  >
    	    <magento:attributes >
    		  <magento:attribute key="city_code" value="#[map-payload:cityCode]"/>
    	    </magento:attributes>
          </magento:create-customer-address>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|customerId||no||
|attributes||no||

Create Customer
---------------

Creates a customer with the given attributes

Example: 



     	<magento:create-customer>
    	      <magento:attributes >
    		    <magento:attribute key="email" value="#[map-payload:email]"/>
    		    <magento:attribute key="firstname" value="#[map-payload:firstname]"/>
    		    <magento:attribute key="lastname" value="#[map-payload:lastname]"/>
    			    <magento:attribute key="password" value="#[map-payload:password]"/>
    	      </magento:attributes>
           </magento:create-customer>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|attributes| the attributes of the new customer|no||

Delete Customer
---------------

Deletes a customer given its id

Example:



     <magento:delete-customer customerId="#[map-payload:customerId]" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|customerId||no||

Delete Customer Address
-----------------------

Deletes a Customer Address

Example:



     <magento:delete-customer-address addressId="#[map-payload:addressId]" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|addressId||no||

Get Customer
------------

Answers customer attributes for the given id. Only the selected attributes are
retrieved

Example:



     <magento:get-customer  customerId="#[map-payload:customerId]"  >
    	<magento:attributeNames>
    		<magento:attributeName>customer_name</magento:attributeName>
    			<magento:attributeName>customer_last_name </magento:attributeName>
    		<magento:attributeName>customer_age</magento:attributeName>
    	</magento:attributeNames>
      </magento:get-customer>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|customerId||no||
|attributeNames| the attributes to retrieve. Not empty|no||

Get Customer Address
--------------------

Answers the customer address attributes

Example: 


     <magento:get-customer-address  addressId="#[map-payload:addressId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|addressId||no||

List Customer Addresses
-----------------------

Lists the customer address for a given customer id

Example: 



      <magento:list-customer-addresses customerId="#[map-payload:customerAddresses]" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|customerId| the id of the customer|no||

List Customer Groups
--------------------

Lists all the customer groups

Example: 



     <magento:list-customer-groups />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||

List Customers
--------------

Answers a list of customer attributes for the given filter expression.

Example:



     <magento:list-customers filters="gteq(customer_age, #[map-payload:minCustomerAge])" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|filters| an optional filtering expression.|yes||

Update Customer
---------------

Updates the given customer attributes, for the given customer id. Password can
not be updated using this method

Example:



     <magento:update-customer customerId="#[map-payload:customerId]">
    	    <magento:attributes>
    	       <magento:attribute key="lastname" value="#[map-payload:lastname]"/>
    	    </magento:attributes>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|customerId||no||
|attributes| the attributes map|no||

Update Customer Address
-----------------------

Updates the given map of customer address attributes, for the given customer address

Example:



     <magento:update-customer-address addressId="#[map-payload:addressId]">
    	  <magento:attributes>
    		<magento:attribute key="street" value="#[map-payload:street]"/>
    		<magento:attribute key="region" value="#[map-payload:region]"/>
    	   </magento:attributes>
        </magento:update-customer-address>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|addressId| the customer address to update|no||
|attributes|  the address attributes to update|no||

List Stock Items
----------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|productIdsOrSkus||no||

Update Stock Item
-----------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|productIdOrSku||no||
|attributes||no||

List Directory Countries
------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||

List Directory Regions
----------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|countryId||no||

Assign Product Link
-------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|type||no||
|product||no||
|linkedProduct||no||
|attributes||no||
|productIdentifierType||no||

Create Product Attribute Media
------------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|product||no||
|attributes||no||
|storeView||no||
|productIdentifierType||no||

Delete Product Attribute Media
------------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|product||no||
|file||no||
|productIdentifierType||no||

Delete Product Link
-------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|type||no||
|product||no||
|linkedProduct||no||
|productIdentifierType||no||


Get Product Attribute Media
---------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|product||no||
|file||no||
|storeView||no||
|productIdentifierType||no||



List Category Attributes
------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||

List Category Attributes Options
--------------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|attributeId||no||
|storeView||no||

List Product Attribute Media
----------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|product||no||
|storeView||no||
|productIdentifierType||no||

List Product Attribute Media Types
----------------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|setId||no||

List Product Attribute Options
------------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|attributeId||no||
|storeView||no||

List Product Attributes
-----------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|setId||no||

List Product Attribute Sets
---------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||

List Product Attribute Tier Prices
----------------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|product||no||
|productIdentifierType||no||

List Product Link
-----------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|type||no||
|product||no||
|productIdentifierType||no||

List Product Link Attributes
----------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|type||no||

List Product Link Types
-----------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||

List Product Types
------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||

Update Category Attribute Store View
------------------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|storeView||no||

Update Product Attribute Media
------------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|product||no||
|file||no||
|attributes||no||
|storeView||no||
|productIdentifierType||no||

Update Product Attribute Media Store View
-----------------------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|storeView||no||

Update Product Attribute Store View
-----------------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|storeView||no||


Update Product Link
-------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|type||no||
|product||no||
|linkedProduct||no||
|attributes||no||
|productIdentifierType||no||

















