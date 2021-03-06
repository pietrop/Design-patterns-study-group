## The Prototype Pattern

## Intent

Implements a prototype interface which tells to create a shallow clone of the current object.

\[Through a prototypical interface it specifies the kinds of object to create, and creates new objects by copying this prototype.\]

## Motivation

One use case could be when performing an extensive database operation to crate object that will be used in other part of the application.

If another process needs it, rather than perform this db operation it's more convenient to clone the previous created object.

In general it can be used to reduce the number of classes.

By instantiating the prototype interface, through the inheritance properties and methods are afterwards extended by the instances that use it.

## Applicability

> Use the Prototype pattern when a system should be independent of how its products are created, composed, and represented

## Structure

_A graphical representation of the classes in the pattern using a notation based on the Unified Modeling Language \(UML\).  
We also use interaction diagrams to illustrate sequences of requests and collaborations between objects._

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

The repo is here: [https://github.com/andrixb/js\_design\_patterns/tree/CREATIONAL-DP/Prototype](https://github.com/andrixb/js_design_patterns/tree/CREATIONAL-DP/Prototype)

```js
(function () {
    var imgElement = document.querySelector('.image__element');
    var IMG_URL = 'http://placehold.it/350x150';
    var newObj = null;

    function MainObject(url) {
        this.url = url;
    }

    MainObject.prototype = {
        assignSrc: function (element) {
            element.setAttribute('src', this.url);
        }
    };

    newObj = new MainObject(IMG_URL);
    newObj.assignSrc(imgElement);
})();
```

## Known Uses

_Examples of the pattern found in real systems.  
We include at least two examples from different domains._

## Related Patterns

* _What design patterns are closely related to this one?_
* _What are the important differences?_
* _With which other patterns should this one be used?_



