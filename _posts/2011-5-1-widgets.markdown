---
layout: default
title: Widgets
---
<script src="https://www.allplayers.com/sites/all/libraries/allplayers.js/bin/allplayers.embed.client.min.js" type="text/javascript"></script>
# Widgets

## Group Registration

The Group Registration widget allows users to easily sign up for groups/teams on AllPlayers.com.
The widget is a simple iframe that you can drop into your page.
When not logged into AllPlayers, users will be prompted for their username and password or they
can register for a new account.

## Example

<script type="text/javascript">
  $(function() {
    $('#group_registration').allplayers_client({
      group: 'apciapi'
    });
  });
</script>
<div id="group_registration"></div>

## Usage

One of the goals when having widgets embedded in your application/web site is to have a seamless
integration so that the user has a better experience, to embed a registration within your own
website, you can use the simple jQuery plugin.

### 1. Include the AllPlayers.com embedded registration source in your header.

    <script src="https://www.allplayers.com/sites/all/libraries/allplayers.js/bin/allplayers.embed.client.min.js" type="text/javascript"></script>

### 2. Now add an empty DIV tag where you would like to embed the registration.

    <div id="group_registration"></div>


### 3. Next, add the jQuery widget code to turn on your registration within the page.

    <script type="text/javascript">
      $(function() {
        $('#group_registration').allplayers_client({
          group: 'apciapi'
        });
      });
    </script>
