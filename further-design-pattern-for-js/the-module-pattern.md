## The Module Pattern

## Intent

This pattern is used to allow loose coupling having particular piece of code independent from other components.

## Motivation

The **module pattern **is used to implement the concept of [software module](https://en.wiktionary.org/wiki/Software_module), defined by [modular programming](https://en.wikipedia.org/wiki/Modular_programming), in a [programming language](https://en.wikipedia.org/wiki/Programming_language) with incomplete direct support for the concept.

Having an application organized like so it is very useful for scalability.

## Applicability

Offering _encapsulation_ it avoids that states and behaviour of the classes that implement it could be accessed from the outside. Furthermore it can be used to avoid pollution of the global namespace.

## Structure

A graphical representation of the classes in the pattern using a notation based on the Unified Modeling Language \(UML\).  
We also use interaction diagrams to illustrate sequences of requests and collaborations between objects.

## Participants

The classes and/or objects participating in the design pattern and their responsibilities.

## Collaborations

How the participants collaborate to carry out their responsibilities.

## Consequences \(aka Pros and Cons\)

* How does the pattern support its objectives?
* What are the trade-offs and results of using the pattern?
* What aspect of system structure does it let you vary independently?

## Implementation

* What pitfalls, hints, or techniques should you be aware of when implementing the pattern?
* Are there language-specific issues?

## Sample Code

The repo is at https://github.com/andrixb/js\_design\_patterns/tree/FURTHER-DP-FOR-JS/Module

```js
(function() {
    'use strict';

    var MODULE_NAME = 'modulePattern',
        APP_NAMESPACE = 'appNamespace';

    window[APP_NAMESPACE] = window[APP_NAMESPACE] || {};

    window[APP_NAMESPACE][MODULE_NAME] = function() {
        // It hosts module states
        var _$ = {};

        // Initial module configuration
        var _config = {
            text: '.' + MODULE_NAME + '__text'
        };

        function _changeTextContent() {
            _$.text = _$.element.querySelector(_config.text);
            _$.text.innerHTML = _$.newText;
        };

        return {
            init: function(element) {
                _$.element = element;
            },
            newTextToChange: function(newText) {
                _$.newText = newText;
                _changeTextContent();
            },
            destroy: function() {
                _$.element = null;
            }
        };
    };
})();

```

## Known Uses

Examples of the pattern found in real systems.  
We include at least two examples from different domains.

## Related Patterns

* What design patterns are closely related to this one?
* What are the important differences?
* With which other patterns should this one be used?



