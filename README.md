
# Vue Smooth Height
A Vue mixin that answers the question, "How do I transition height: auto?"

This mixin is primarily for container elements that have a dynamic number of children, e.g. lists, however it will work on any element whose height changes due to data changes.  When the container's data is changed, its current height will smoothly transition to the new height, instead of instantly resizing.


Note that this library has no overlap with Vue's built in transition components.

## Demo
https://jsfiddle.net/axfwg1L0/14/

## Installation

Using npm:
```shell
$ npm install vue-smooth-height
```

In a browser:
```html
<script src="vue-smooth-height.min.js"></script>
```

## Usage


```javascript
<template>
    <div>
        <div class="container" ref="container">
            <!-- children created with v-for -->
        </div>
    </div>
</template>

<script>
import smoothHeight from 'vue-smooth-height';

export default {
    mixins:[smoothHeight],
    mounted(){
        //use nextTick if necessary
        this.$registerSmoothElement({
            el: this.$refs.container,
        })
    },
}
</script>
```

Browser:

Same as above, use the global `SmoothHeight`

## CSS
This mixin uses css transitions, meaning you can define whatever css transitions you want for the registered element. If the mixin does not detect any transitions on the element, it will apply `transition: 1s` to it.

## API
### $registerSmoothElement(options)
#### options: Object | Array

Can be a single options object,
or an array of options objects.

Enables smooth height transition on an element.


**Option**|**Types**|**Default**|**Description**
-----|-----|-----|-----
el|Element, String|null|Required. A reference to the element, or a selector string. Use a selector string if the element is not rendered initially. If selector string is a class, the first query match will be registered
hideOverflow|Boolean|false|If the element has a scrollbar, ugly reflow flickers can occur when children create/destroy a new row (think flexbox). Set true to disable overflow during the transition.


### $unregisterSmoothElement(options)
#### options: Object | Array

Can be a single options object,
or an array of options objects.

Disables smooth height behavior on an element. Registered elements that have the same `el` as the passed in options will be unregistered. 

Examples:


```javascript

mounted(){
    // Registering with element reference
    this.$registerSmoothElement({
        el: this.$refs.container,
    })

    
    // If the element reference is a vue object, make sure to pass in its "$el" property.
    this.$registerSmoothElement({
        el: this.$refs.container.$el,
    })

    // Unregistering with class name
    this.$unregisterSmoothElement({
        el: '.container',
    })

},

```