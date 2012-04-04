# Backbone

Version: 0.9.2

## API

### Backbone.Model

* extend(properties, [classProperties])
  * properties
    * initialize
    * instanceMethods
    * idAttribute
    * validate
    * defaults
    * urlRoot
    * url
    * parse
* constructor/initialize([attributes])
* get(attribute)
* set(attributes, [options])
  * Options:
    * silent - prevent change event and validations
    * error - callback for validation errors
  * Events:
    * change
    * change:[attribute]
    * error - when validations fail (if present)
* set(attribute, value)
* escape(attribute) - HTML escaped attribute
* has(attribute)
* unset(attribute, [options])
  * Options:
    * silent - prevent change event
* clear([options])
  * Options:
    * silent - prevent change event
* id
* idAttribute
* cid
* attributes - use #set to update
* changed - use #set and #change to update
* defults or defaults()
* toJSON()
* fetch([options])
  * Options
    * success - callback fn(model,response)
    * error - callback  fn(model,response)
  * Events
    * change
* save([attributes], [options])
  * Options
    * wait - do not update model until server responds
    * success - callback, fn(model,response)
    * error - callback, fn(model, response)
  * Events
    * change - immediately
    * sync - after server acknowledges
* save(attribute, value)
* destroy([options])
  * Options
    * wait - do not delete model until server responds
    * success - callback, fn(model,response)
    * error - callback, fn(model, response)
  * Events
    * destroy - immediately
    * sync - after server acknowledges
* validate(attributes) - overridable
  * Events
    * error
* isValid()
* url() - string or function; overridable
  * /[collection.url]/[id]
  * /[urlRoot]/id
* urlRoot() - used if model outside collection
* parse(response) - overridable
* clone()
* isNew
* change
  * Events
    * change
    * change:[attribute]
* hasChanged([attribute]) - during a 'change' event
* changedAttributes([attributes]) - during a 'change' event
* previous(attribute) - during a 'change' event
* previousAttributes() - during a 'change' event

### Backbone.Collection

Events:
* change[:attribute]
* add
* remove
* fetch

* extend(properties, [classProperties])
  * properties
    * model
    * url
    * parse
* model
* constructor/initialize([models], [options])
  * models - initial array of models
  * Options
    * comparator
* toJSON()
* add(models, [options])
  * models - model or array of models. If #model is defined, accepts raw attribute objects
  * Options
    * silent - prevent 'add' event
    * at - splice model at specified __index__
  * Events
    * add
* remove(models, [options])
  * Options
    * silent - prevent 'remove' event
  * Events
    * remove
* get(id)
* getByCid(cid)
* at(index)
* push(model, [options])
  * Options - same as #add
* pop([options])
  * Options - same as #remove
* unshift(model, [options])
  * Options - same as #add
* shift(model, [options])
  * Options - same as #remove
* length
* comparator
  * sortBy - single argument, returns numeric string value
  * sort - two arguments, return -1, 0 or 1
* sort([options])
  * Options
    * silent - prevent 'remove' event
  * Events
    * reset
* pluck(attribute)
* where(attributes) - simple filter
* url - string or function
* parse(response) - overridable
* fetch
  * Options
    * add - if true, appends to collection instead of replacing
    * jQuery.ajax options
    * success - callback fn(collection,response)
    * error - callback  fn(collection,response)
  * Events
    * reset
* reset(models, [options]) - useful for bootstrapping collection at load
  * models - array of models or attribute hashes (if #model is set). With no arguments, empties the collection
  * Options
    * silent - prevent 'reset' event
  * Events
    * reset
* create(attributes, [options])
  * attributes - attribute has or unsaved model
  * Options
    * wait - do not update model until server responds before adding model to collection
  * Events
    * add
    * sync

#### Underscore methods

forEach (each), map, reduce (foldl, inject), reduceRight (foldr), find (detect),
filter (select), reject, every (all), some (any), include, invoke, max, min,
sortBy, groupBy, sortedIndex, shuffle, toArray, size, first, initial, rest,
last, without, indexOf, lastIndexOf, isEmpty, chain

### Backbone.Router

During load, call Backbone.history.start() or Backbone.history.start({pushState: true})

* extend(properties, [classProperties])
  * properties
    * routes - hash map, avoid leading slash in definitions
      * key - URL
      * value - routing function
        * :param
        * \*splat
      * Events
        * route:[routingFunction]
    * [routeHandlers]
* constructor/initialize([options])
* route(route, name, [callback]) - create routes manually
  * route - string or regex
  * name - event to trigger when route is matched
  * callback - function to execute when route is matched. If not provided, will call router[name] instead
* navigate(fragment, [options])
  * Options
    * trigger - if true, call the route function as well
    * replace - if true, update URL without creating history entry

### Backbone.history

pushState requires server changes to support the modified URLs

* start([options]) - call after Routers have been created and configured
  * Options
    * pushState - if true, enable HTML5 pushState support
    * root - if application not served from rool url of domain
    * silent - if true, do not trigger initial route

### Backbone.sync

Override to use non-server persistance (WebSockets, XML, LocalStorage)

* sync(method, model, [options])
  * method - create, read, update, delete
  * model - model to be saved or collection to be read
  * Options
    * success - callback
    * error - callback
    * jQuery request options
  * Override globally as Backbone.sync or adding #sync to collections or models
* emulateHTTP - send HTTP verb in X-HTTP-Method-Override
* emulateJSON - submit request as application/x-www-form-urlencoded

### Backbone.View

* extend(properties, [classProperties])
  * properties
    * render
    * events
    * tagName
    * className
    * id
* constructor/initialize([options])
  * Options - attached to view as __this.options__
    * model
    * collection
    * el - if view references an element already in the DOM
    * id
    * className
    * tagName
    * attributes
* el - created from View's tagname, className, id and attributes, otherwise an empty div
* $el
* setElement(element)
* attributes
* $(selector)
* render() - by convention, return __this__ for chaining
* remove()
* make(tagName, [attributes], [content])
* delegateEvents([events])
  * events - hash map. If not provided, uses __this.events__. Can also be a function
    * key - event selector
    * value - callback. Can be a string for a method name or a function
* undelegateEvents()

### Utility Functions

* Backbone.noConflict()
* Backbone.setDomLibrary(jQueryNew)

## Event Catalog

* add(model, collection0
* remove(model, collection)
* reset(collection)
* change(model, options)
* change:\[attribute\](model, value, options)
* destroy(model, collection)
* sync(model, collection)
* error(model, collection)
* route:\[name\](router)
* all
