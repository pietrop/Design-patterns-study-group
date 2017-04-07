# The Publisher + Subscriber

## Intent

This pattern is a variation of the observer pattern. The idea here is to avoid dependencies between the subscriber and publisher

It uses events to put in communication the objects. A publisher triggers an event and the subscribers capture it.

## Also Known As

_Other well-known names for the pattern, if any._

## Motivation

_A scenario that illustrates a design problem and how the class and object structures in the pattern solve the problem.  
The scenario will help you understand the more abstract description of the pattern that follows._

## Applicability

* _What are the situations in which the design pattern can be applied?_
* _What are examples of poor designs that the pattern can address?_
* _How can you recognise these situations?_

## Structure

_A graphical representation of the classes in the pattern using a notation based on the Unified Modeling Language \(UML\).  
We also use interaction diagrams to illustrate sequences of requests and collaborations between objects._

_You can use ArgoUML as a free software to create UML class diagrams \(_[_http://argouml.tigris.org/\_](http://argouml.tigris.org/%29_\) or give a look at this list _\[\__[https://en.wikipedia.org/wiki/List\_of\_Unified\_Modeling\_Language\_tools](https://en.wikipedia.org/wiki/List_of_Unified_Modeling_Language_tools)\]\([https://en.wikipedia.org/wiki/List\_of\_Unified\_Modeling\_Language\_tools](https://en.wikipedia.org/wiki/List_of_Unified_Modeling_Language_tools)\)

## Participants

_The classes and/or objects participating in the design pattern and their responsibilities._

## Collaborations

_How the participants collaborate to carry out their responsibilities._

## Consequences \(aka Pros and Cons\)

* _How does the pattern support its objectives?_
* _What are the trade-offs and results of using the pattern?_
* _What aspect of system structure does it let you vary independently?_

## Implementation

* _What pitfalls, hints, or techniques should you be aware of when implementing the pattern?_
* _Are there language-specific issues?_

## Sample Code

The repo is here: [https://github.com/andrixb/js\_design\_patterns/tree/BEHAVIORAL-DP/PublishSubscribe](https://github.com/andrixb/js_design_patterns/tree/BEHAVIORAL-DP/PublishSubscribe)

`publisher`

```js
(function() {
    var APP_NAMESPACE = 'appNamespace';
    var MODULE_NAME = 'publisher';

    window[APP_NAMESPACE] = window[APP_NAMESPACE] || {};
    window[APP_NAMESPACE][MODULE_NAME] = function() {
        var _$ = {};
        var _config = {
            btn: '.' + MODULE_NAME + '__btn',
            msg: '.' + MODULE_NAME + '__containerBtn'
        };

        function _setBtn() {
            _$.btn = _$.element.querySelector(_config.btn);
        }

        // get the attribute which contains a message
        function _getInfoToSend() {
            _$.infoMsg = _$.element.querySelector(_config.msg)
                                   .getAttribute('data-message');
        }

        // create custom event and dispatch the message to listeners
        function _notifyEvent() {
            var sharedCustomEvent = document.createEvent('CustomEvent');
            sharedCustomEvent.initCustomEvent('notify', true, true, _$.infoMsg);
            document.dispatchEvent(sharedCustomEvent);
        }

        // add event listener to button and dispatch the event
        function _addEvents() {
            _$.btn.addEventListener('click', function(event) {
                event.preventDefault();
                _getInfoToSend();
                _notifyEvent(event);
            })
        }

        return {
            init: function(element) {
                _$.element = element;
                _setBtn();
                _addEvents();
            },
            destroy: function() {
                _$.element = null;
            }
        }
    };
})();
```

`subscriber`

```js
(function() {
    var APP_NAMESPACE = 'appNamespace';
    var MODULE_NAME = 'subscriber';

    window[APP_NAMESPACE] = window[APP_NAMESPACE] || {};
    window[APP_NAMESPACE][MODULE_NAME] = function() {
        var _$ = {};
        var _config = {
            textElement: '.' + MODULE_NAME + '__msg'
        };

        function _getTextElement() {
            _$.text = _$.element.querySelector(_config.textElement);
        }
        
        // Listen to the custom event
        function _addEvent() {
            document.addEventListener('notify', function(event) {
                _$.text.innerHTML = event.detail;
            }, false);
        }

        return {
            init: function(element) {
                _$.element = element;
                _getTextElement();
                _addEvent();
            },
            destroy: function() {
                _$.element = null;
            }
        }
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



