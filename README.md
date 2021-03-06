# DSeL

You can use DSeL (pronounced _Diesel_ -- best I could do) to:

* Safely interact with any object as if you were operating within it.
    * No need to keep typing `obj.*` to work on `obj`.
* Unsafely re-open (almost) any object like you re-open a `Class` and mess about it there.
* Define clean APIs for 3rd party functionality via a DSL.
    * Documentation can be generated dynamically using API tree data.
* Access APIs via a DSL.
    * Allows for scripting etc.
* Create custom DSLs.

**Currently an unstable work in progress, touch at own risk.**

## Description

It is:

* A generic DSL (`DSeL::DSL::Nodes::Base`) supporting:
    * Proxy (`DSeL::DSL::Nodes::Proxy`) environments for safe interaction with any given object.
        * Method calls are forwarded.
        * Internal state not affected nor accessible.
    * Direct (`DSeL::DSL::Nodes::Direct`) environments, 
        where the DSL context is the actual object instance.
    * Preserved contexts:
        * Re-entrant.
        * Re-usable.
        * Per object instance.
        * Shared variables across environment nodes.
        * Tree environment structure, with traversal helpers:
            * `Root`
            * `Parent`
* An API specification framework (`DSeL::API::Node`).
    * Specify call:
        * Description 
        * Type
        * Object/catch-call
        * Arguments and &block.
        * Handler
    * Tree structure for sections.
* An API specification language (`DSeL::DSL::APIBuilder`).
    * `import` external API spec files.
    * Define and describe sections (children).
* An API runner.
    * Providing a specialised DSL (`DSeL::DSL::Nodes::API`) for API nodes (`DSeL::API::Node`).

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'dsel', github: 'qadron/dsel'
```

And then execute:

    $ bundle

## Examples

See: [examples/](https://github.com/qadron/dsel/tree/master/examples/)

### API

Include the API specification:

```ruby
require_relative 'examples/api/my_api'
```

Use via a DSL script:

```ruby
MyAPI.run 'examples/api/my_api_dsl.rb'
```

Use via a Ruby script:

```ruby
require 'examples/api/my_api_ruby'
````

See: [examples/api/](https://github.com/qadron/dsel/tree/master/examples/api/)

### DSL

See: [examples/dsl/object.rb](https://github.com/qadron/dsel/tree/master/examples/dsl/object.rb)

#### Proxy

The safe way to get a DSL is to run the object inside a _Proxy_ context and
just proxy methods, thus allowing the user to interact with the object as if 
operating within it semantically but without access to non-public methods or its 
state.

See: [examples/dsl/proxy.rb](https://github.com/qadron/dsel/tree/master/examples/dsl/proxy.rb)

#### Direct

The direct way means not having the object inside the environment, but the 
environment inside the object, thus allowing you to truly operate within it and 
make a general mess of things or do some pretty cool stuff.

See: [examples/dsl/direct.rb](https://github.com/qadron/dsel/tree/master/examples/dsl/direct.rb)

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/qadron/dsel.

## License

Please see the `LICENSE.md` file.
