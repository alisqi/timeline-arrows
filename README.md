# Timeline-arrows

Following the issue of vis https://github.com/almende/vis/issues/1699, and thanks to the comments of @frboyer and @JimmyCheng, I have created a class to easily draw lines to connect items in the vis Timeline module.

![CapturaTime](https://user-images.githubusercontent.com/36993404/59111595-9d830600-8941-11e9-8cb8-8d7b72701a71.JPG)


## Install & initialize

1 - Download the package

```bash
npm install timeline-arrows
```

2 - Import the class `Arrows` from `arrows.js` in your project


3 - Create your timeline as usual (see [vis-timeline docs](https://visjs.github.io/vis-timeline/docs/timeline/)).

For instance:

```bash
const myTimeline = new vis.Timeline(container, items, groups, options);
```


4 - Create your arrows as an array of objects. These objets must have, at least, the following properties:
* id
* item1Id (id of one timeline's items)
* item2Id (id of the other timeline's items that you want to connect with)

And optionally:
* title (insert a text and it will show a title if you hover the mouse in the arrow)

For instance:

```javascript
var arrowsSpecs = [
    { id: 2, item1Id: 1, item2Id: 2 },
    { id: 5, item1Id: 3, item2Id: 5, title:'Hello!!!' },
    { id: 7, item1Id: 6, item2Id: 7 },
    { id: 10, item1Id: 3, item2Id: 8, title:'I am a title!!!' }
];
```

5 - Create your Arrows instance for your timeline and your arrows.

For instance:

```javascript
const myArrows = new Arrows(myTimeline, arrowsSpecs);
```

That's it :)

## Options

Options can be used to customize the arrows. Options are defined as a JSON object. All options are optional.

```javascript
const options = {
    followRelationships: true,
    color: "#039E00",
    tooltipConfig: (el, title) => {
        // tooltip initialization
    },
};

const myArrows = new Arrows(myTimeline, arrowsSpecs, options);
```

**followRelationships** - defaults to false.
If true, arrows can point backwards and will follow the relationships set in the data. If false, arrows will only follow the timeline direction (left to right).

**color** - defaults to "#9c0000".
Sets the arrows color.

**strokeWidth** - defaults to 3 (px).
Sets the arrows width in pixels.

**tooltipConfig** - if arrows have a `title` property, the default behavior will add a title attribute that shows on hover. However, you might not want to use the title attribute, but instead your own tooltip configuration.
This method takes two arguments, `el` - the arrow - and `title` - the content of the `title` property set in the arrow data.

## Methods

I have created the following methods:

**getArrow ( *arrow id* )**  Returns the arrow whith this arrow_id.

For instance:

```javascript
myArrows.getArrow(2);
```

**addArrow ( *arrow object* )**  Inserts a new arrow.

For instance:

```javascript
myArrows.addArrow({ id: 13, item1Id: 15, item2Id: 16 });
```

**removeArrow ( *arrow_Id* )**   Removes the arrows with this arrow_Id.

For instance:

```javascript
myArrows.removeArrow( 10 );
```

**removeItemArrows ( *item_Id* )**   Removes the arrows connected with Items with this item_Id. Returns an array with the id's of the removed arrows.

For instance:

```javascript
myArrows.removeItemArrows( 23 );
```

## Examples

You can see some working examples here:

https://javdome.github.io/timeline-arrows/index.html

... or by running following command:

```shell
npm run serve
```

## Changes

### Changes in 5.0.0 (breaking changes from 4.1.0)

Class `Arrow` was renamed to `Arrows`, becuase that is what it represents.
It is also no longer the default export, so this is easier to consume in more modern JavaScript.

The arrow spec fields were renamed from the snake_case notation `id_item_1` and `id_item_2`
to the JavaScript standard `item1Id` and `item2Id`.

File `arrows.js` was renamed to `arrows.js`, which makes more sense in the import statement.

`arrows.d.ts` is generated from JSDoc using Typescript transpiler.
