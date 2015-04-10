SpreeAddOns
===========

This gem provides the ability to create custom addons for line_items. For example a product can have gift wrapping and/or packaging.

A line item can have any number of add ons as long as they are defined on the product and active. In the event an add on is deleted the line_item and order are marked invalid
 and appropriate errors are applied.

To create a line item or update one with add ons POST/PATCH with options as follows:
<pre>
```
{
    line_item: {
    ...
    options: {
            add_on_ids: [1,3]
        }
    }
}
```
</pre>
To remove all add ons or a specific one DELETE with options to /api/orders/:number/line_item/:line_item_id/remove_add_ons
<pre>
```
{
    line_item: {
    ...
    options: {
            add_on_ids: [1] // Removes add on 1
        }
    }
}
```
</pre>
<br>or omit options to remove all add ons<br>
<pre>
```
{
    line_item: {
    ...
    }
}
```
</pre>
To create a new add on simply create a file simply inherit from ```Spree::AddOn```
<pre>
```
    class Spree::OtherAddOn < Spree::AddOn
        # what is shown when selecting the type in admin
        def self.display_name
            'Other Add On'
        end
    end
```
</pre>

This ```Spree::OtherAddOn``` will then be available in /admin when creating a new add_on.

```Spree::LineItem``` json has been extended to include
<pre>
```
// add_ons currently attached to the line_item
add_ons: [
    {
        id: 1,
        name: Some Add on
        ...
    }
],
// add_ons that can be added to this line_item
available_add_ons: [
    {
        id: 1,
        name: Some add on
        ...
    },
    {
        id: 4,
        name: Some Other add on
        ...
    }
]
```
</pre>

Installation
------------

Add spree_add_ons to your Gemfile:

```ruby
gem 'spree_add_ons'
```

Bundle your dependencies and run the installation generator:

```shell
bundle
bundle exec rails g spree_add_ons:install
```

Testing
-------

First bundle your dependencies, then run `rake`. `rake` will default to building the dummy app if it does not exist, then it will run specs. The dummy app can be regenerated by using `rake test_app`.

```shell
bundle
bundle exec rake
```

When testing your applications integration with this extension you may use it's factories.
Simply add this require statement to your spec_helper:

```ruby
require 'spree_add_ons/factories'
```

Copyright (c) 2015 [name of extension creator], released under the New BSD License
