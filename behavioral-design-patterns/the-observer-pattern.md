# The Observer Pattern

## Intent

> Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

## Also Known As

Dependents, Publish-Subscribe

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

_You can use ArgoUML as a free software to create UML class diagrams \(_[_http://argouml.tigris.org/\_](http://argouml.tigris.org/%29\)_ or give a look at this list _[_https://en.wikipedia.org/wiki/List\_of\_Unified\_Modeling\_Language\_tools_](https://en.wikipedia.org/wiki/List_of_Unified_Modeling_Language_tools)

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

The repo is here: https://github.com/andrixb/js\_design\_patterns/tree/BEHAVIORAL-DP/Observer

```js
(function () {
    var subjectEl = document.querySelector('.subject__container');
    var observers = document.querySelectorAll('.observer__container');
    var totObservers = [];

    var Observer = function (element) {
        var _$ = {
            element: element
        };

        var _config = {
            msg: '.observer__msg'
        }

        return {
            notify: function (index) {
                _$.msg = _$.element.querySelector(_config.msg);
                _$.msg.innerHTML = 'Observer ' + index + ' is notified!';
            }
        };
    };

    var Subject = function (element) {
        var _$ = {
            observers: [],
            element: element
        };

        function _getBtn() {
            _$.btn = _$.element.querySelector('.subject__btn');
        }
        function _addEvent() {
            _$.btn.addEventListener('click', function(event) {
                for (var i = 0; i < _$.observers.length; i++) {
                    _$.observers[i].notify(i);
                }
            }, false);
        }

        return {
            init: function() {
                _getBtn();
                _addEvent();
            },
            subscribeObserver: function (observer) {
                if (_$.observers !== null) {
                    _$.observers.push(observer);
                } else {
                    _$.observers = [];
                }

            },
            unsubscribeObserver: function (observer) {
                var index = _$.observers.indexOf(observer);
                if (index > -1) {
                    _$.observers.splice(index, 1);
                }
            },
            notifyObserver: function (observer) {
                var index = _$.observers.indexOf(observer);
                if (index > -1) {
                    _$.observers[index].notify(index);
                }
            },
            notifyAllObservers: function () {
                for (var i = 0; i < _$.observers.length; i++) {
                    _$.observers[i].notify(i);
                }
            }
        };
    };

    var subject = new Subject(subjectEl);

    for (var i = 0; i < observers.length; i++) {
        totObservers.push(new Observer(observers[i]));
    }

    for (var i = 0; i < observers.length; i++) {
        subject.subscribeObserver(totObservers[i]);
    }

    subject.init();

})();
```

## Known Uses

_Examples of the pattern found in real systems.  
We include at least two examples from different domains._

## Related Patterns

* _What design patterns are closely related to this one?_
* _What are the important differences?_
* _With which other patterns should this one be used?_



