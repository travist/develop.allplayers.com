---
layout: default
title: Partner Application Framework
---
# Partner Application Framework

## Overview
The Partner Application Framework allows our partners to hook into the AllPlayers.com infrastructure to inject their
products and services into platform.  This feature allows our partners to participate in the AllPlayers.com ecosystem
and further provide value added features to our customers who use our system.  For example, with the Partner
Application Framework, a sports equipment supplier can inject their products during the registration workflow.  This
provides them the ability to display only the relevant sports equipment based on the information collected during
registration.

There are currently three different methods for our Partners to inject their services into our platform (with many more
in the works).

 - __Registration__ - This allows our partners to inject their products and services within the Group registration workflow.
 - __Checkout__ - This allows our partners to provide their own checkout system so that we can process their products within
 their own merchant processing system.
 - __Group Dashboard__ - This allows our partners to provide group dashboard content that can be added to the group pages.

## Setup
To get started, you will first need to create an account on AllPlayers.com, and then make sure you verify this account.
Once you are done with that, you will then need to contact our Support to enable your account as a __Partner__ account.
Once you have a Partner account within our system, you should then create a new Group which will be the name of your
business which you wish to integrate into the AllPlayers.com ecosystem.

After you have a group created, you can then add a new Application by clicking on your group __Toolbox__ and then
selecting __Create Application__.

![Create Application](https://api.monosnap.com/image/download?id=428oIeX0iJ1D9zH6D54Gs7wVgINCNI)

This will take you to a page where you can then add your application to our system.

![Create Application](https://api.monosnap.com/image/download?id=oWuhtqVjEQWEJl9MiXlFEcxHdIip0J)

Now that you have a new application, the next task is to create an Application Feature.  Click on your __Toolbox__
and select __Create Application Feature__

![Create Application Feature](https://api.monosnap.com/image/download?id=ZC986ajzkVVnwOFgE3qviWAB9anGMq)

From here, you can then choose the name of your Feature and the type (Registration, Checkout, Dashboard, etc). For this
example, lets suppose you wish to inject a product store within our registration.  With this you will have the ability
to provide an __iFrame URL__ which will point to your website that contains the product store.  This iFrame will then
be injected within our registration workflow.  This iframe URL can be an external store on a separate domain, OR the URL
of an AllPlayers.com storefront.

![Create Application Feature](https://api.monosnap.com/image/download?id=jfxT6ZNCZCfmsxJwobdZ4pETuV0ZLJ)

Now that you have created the Application Feature, the next task is to build out your embedded application so that it
works within the registration workflow.

## Developing Partner Applications

Because our partner application rely on iframe's, it is important to include some helper libraries within your
application to both receive communication and send messages to the parent page that will be including your application.

This iframe communication is easily provided from an Open Source library called [Seamless.js](https://github.com/travist/seamless.js).
Please read through the documentation provided from the Seamless.js library to understand how the child page can interact with the
parent page.

To create your page, you will need to add the following code to your application page.

## Include the Seamless.js client JS file in your page.
First you will need to download the Seamless.js library using https://github.com/travist/seamless.js/archive/master.zip and then
include this along with your HTML page like the following.

    <script src="seamless/build/seamless.child.min.js"></script>

### Register the page with the Parent Page.
The next thing you will need to do is register your application page with the Parent page that is including your application.

    <script type="text/javascript">

      // Connect to the parent page.
      var parent = $.seamless.connect({
        url: 'https://www.allplayers.com'
      });
    </script>

### Register for the Registration information.
Now that your application is linked to the parent page, the next thing you will want to do is register an event callback
where the parent page will pass along the registrant information to your application during the registration process.


    <script type="text/javascript">

      // Connect to the parent page.
      var parent = $.seamless.connect({
        url: 'https://www.allplayers.com'
      });

      // Register to get the registration data.
      parent.receive('getRegistration', function(data) {

        // This will log all data from the registration.  You can use this data to submit an AJAX request
        // to your server to display the content you wish to display according to the information you receive.
        console.log(data);
      });
    </script>

### Tell the Registration engine to add products to the registration.
Now lets suppose the user interacts with your application and wishes to buy a product from your widget.  The next thing
you will need to do is tell the registration engine to add your products to the registration process.  You can do this
by sending a message to the parent page called __addProduct__.  This command can include additional data about your product
such as the product uuid (SKU), title, price, and quantity.  Below is a very simple jQuery example of how this would work.


    <head>
      ...
      ...
      <script type="text/javascript">

        // Connect to the parent page.
        var parent = $.seamless.connect({
          url: 'https://www.allplayers.com'
        });

        // Register to get the registration data.
        parent.receive('getRegistration', function(data) {

          // This will log all data from the registration.  You can use this data to submit an AJAX request
          // to your server to display the content you wish to display according to the information you receive.
          console.log(data);
        });

        // Execute when the DOM is fully loaded.
        $(function() {

          // Register the click events on the product links.
          $('a').click(function(event) {

           // Prevent default so it doesn't follow the links.
           event.preventDefault();

           // Send the addProduct message to the parent page.
           parent.send({
             type: 'addProduct',
             data: {
               'product_uuid': $(this).attr('product-uuid'),
               'title': $(this).text(),
               'price': $(this).attr('price'),
               'quantity': 1
             }
           });
          });
        });
      </script>
    </head>
    <body>
      <a href="#" type="button" product-uuid="TSHIRT" price="25">T-Shirt</a>
      <a href="#" type="button" product-uuid="SHORTS" price="15">Shorts</a>
      <a href="#" type="button" product-uuid="SOCKS" price="5">Socks</a>
    </body>


### Conclusion
With this, your products will now be added to the checkout process within the AllPlayers registration engine.  You can
now create a separate Application Feature called 'Checkout' feature that would be able to process these products, but
this system will be described in a separate walkthrough.
