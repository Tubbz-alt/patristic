<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### Table of Contents

-   [version][1]
    -   [Examples][2]
-   [Branch][3]
    -   [Parameters][4]
    -   [addChild][5]
        -   [Parameters][6]
    -   [addParent][7]
        -   [Parameters][8]
    -   [ancestors][9]
    -   [clone][10]
    -   [consolidate][11]
    -   [copy][12]
    -   [count][13]
    -   [descendants][14]
    -   [depthOf][15]
        -   [Parameters][16]
    -   [distanceBetween][17]
        -   [Parameters][18]
    -   [distanceTo][19]
        -   [Parameters][20]
    -   [each][21]
        -   [Parameters][22]
    -   [eachAfter][23]
        -   [Parameters][24]
    -   [eachBefore][25]
        -   [Parameters][26]
    -   [eachChild][27]
        -   [Parameters][28]
    -   [excise][29]
    -   [fixDistances][30]
    -   [fixParenthood][31]
        -   [Parameters][32]
    -   [flip][33]
    -   [getAncestors][34]
        -   [Parameters][35]
    -   [getChild][36]
        -   [Parameters][37]
    -   [getDescendant][38]
        -   [Parameters][39]
    -   [getDescendants][40]
        -   [Parameters][41]
    -   [getLeafs][42]
    -   [getLeaves][43]
    -   [getMRCA][44]
        -   [Parameters][45]
    -   [getRoot][46]
    -   [hasChild][47]
        -   [Parameters][48]
    -   [hasDescendant][49]
        -   [Parameters][50]
    -   [hasLeaf][51]
        -   [Parameters][52]
    -   [invert][53]
    -   [isChildOf][54]
        -   [Parameters][55]
    -   [isConsistent][56]
    -   [isDescendantOf][57]
        -   [Parameters][58]
    -   [isLeaf][59]
    -   [isolate][60]
    -   [isRoot][61]
    -   [leafs][62]
    -   [leaves][63]
    -   [links][64]
    -   [normalize][65]
        -   [Parameters][66]
        -   [Examples][67]
    -   [path][68]
        -   [Parameters][69]
    -   [remove][70]
    -   [replace][71]
        -   [Parameters][72]
    -   [reroot][73]
        -   [Examples][74]
    -   [rotate][75]
        -   [Parameters][76]
    -   [setLength][77]
        -   [Parameters][78]
    -   [setParent][79]
        -   [Parameters][80]
    -   [simplify][81]
    -   [sort][82]
        -   [Parameters][83]
    -   [sources][84]
        -   [Parameters][85]
    -   [sum][86]
        -   [Parameters][87]
    -   [targets][88]
        -   [Parameters][89]
    -   [toJSON][90]
    -   [toMatrix][91]
    -   [toNewick][92]
        -   [Parameters][93]
    -   [toObject][94]
    -   [toString][95]
        -   [Parameters][96]
-   [parseJSON][97]
    -   [Parameters][98]
-   [parseMatrix][99]
    -   [Parameters][100]
-   [parseNewick][101]
    -   [Parameters][102]

## version

The [SemVer][103] version string of the patristic library

Type: [String][104]

### Examples

```javascript
console.log(patristic.version);
```

## Branch

A class for representing Branches in trees.
It's written predominantly for phylogenetic trees (hence the
[Newick parser][105],
[neighbor-joining implementation][106], etc.), but could
conceivably be useful for representing other types of trees as well.

### Parameters

-   `data` **[Object][107]?** An object containing data you wish to assign to
    this Branch object. In particular, intended to overwrite the default
    attributes of a Branch, namely `id`, `parent`, `length`, and `children`.
-   `children`  

### addChild

Adds a new child to this Branch

#### Parameters

-   `data` **([Branch][108] \| [Object][107])** The new Branch, or data to attach to it. (optional, default `{}`)

Returns **[Branch][108]** The (possibly new) child Branch

### addParent

Adds a new parent to this Branch. This is a bit esoteric and generally not
recommended.

#### Parameters

-   `data` **([Branch][108] \| [Object][107])** A Branch object, or the data to attach to one (optional, default `{}`)
-   `siblings` **[Array][109]** An array of Branches to be the children of the new parent Branch (i.e. siblings of this Branch) (optional, default `[]`)

Returns **[Branch][108]** The Branch on which this was called

### ancestors

Returns an array of Branches from this Branch to the root.
[d3-hierarchy compatibility method.][110]

Type: [Array][109]

### clone

Returns a deep clone of the Branch on which it is called. Note that this does
not clone all descendants, rather than providing references to the existing
descendant Branches.

Returns **[Branch][108]** A clone of the Branch on which it is called.

### consolidate

All descendant Branches with near-zero length are excised

Returns **[Branch][108]** The Branch on which this method was called.

### copy

Returns a clone of the Branch on which it is called. Note that this also
clones all descendants, rather than providing references to the existing
descendant Branches. (For a shallow clone, see [Branch.clone][10].
Finally, the cloned Branch will become the root of the cloned tree, having a
parent of `null`.
[d3-hierarchy compatibility method.][111]

Returns **[Branch][108]** A clone of the Branch on which it is called.

### count

Sets the values of all nodes to be equal to the number of their descendants.

Returns **[Branch][108]** The Branch on which it was called

### descendants

Returns an array pf descendants, starting with this Branch.
[d3-hierarchy compatibility method.][112]

Type: [Array][109]

### depthOf

Returns the depth of a given child, relative to the Branch on which it is
called.

#### Parameters

-   `descendant` **([Branch][108] \| [String][104])** A descendant Branch (or `id` string
    thereof)

Returns **[Number][113]** The sum of the lengths of all Branches between the Branch on
which it is called and `descendant`. Throws an error if `descendant` is not a
descendant of this Branch.

### distanceBetween

Computes the patristic distance between `descendantA` and `descendantB`.

#### Parameters

-   `descendantA` **[Branch][108]** The Branch from which you wish to compute
    distance
-   `descendantB` **[Branch][108]** The Branch to which you wish to compute distance

Returns **[number][113]** The patristic distance between the given descendants.

### distanceTo

Computes the patristic distance between `cousin` and the Branch on which
this method is called.

#### Parameters

-   `cousin` **[Branch][108]** The Branch to which you wish to compute distance

Returns **[number][113]** The patristic distance between `cousin` and the Branch on
this method is called.

### each

Visits each Branch descended from the Branch on which it is called in
[Breadth First Search][114]
order and returns the Branch on which it was called.

#### Parameters

-   `callback` **[Function][115]** The function to be run on each Branch

Returns **[Branch][108]** The Branch on which it was called.

### eachAfter

Visits each Branch descended from the Branch on which it is called in
[post-traversal order][116]
and returns the Branch on which it was called.

#### Parameters

-   `callback` **[Function][115]** Function to run on each Branch

Returns **[Branch][108]** The Branch on which it was called

### eachBefore

Visits each Branch descended from the Branch on which it is called in
[pre-traversal order][117]
and returns the Branch on which it was called.

#### Parameters

-   `callback` **[Function][115]** [description]

Returns **\[type]** [description]

### eachChild

Runs a function on each child of the Branch on which it is called.

#### Parameters

-   `callback` **[Function][115]** The function to run on each child.

Returns **[Branch][108]** The Branch on which it was called.

### excise

Excises the Branch on which it is called and updates its parent and children.

Returns **[Branch][108]** The parent of the excised Branch.

### fixDistances

Sets the distance values (height and depth) for each Branch

Returns **[Branch][108]** The Branch on which it is called.

### fixParenthood

Repairs incorrect links by recurively confirming that children reference
their parents, and correcting those references if they do not.

If you need to call this, something has messed up the state of your tree
and you should be concerned about that. Just FYI. ¯\\_(ツ)_/¯

#### Parameters

-   `nonrecursive` **[Boolean][118]** Should this just fix the children of the
    Branch on which it is called, or all descendants?

Returns **[Branch][108]** The Branch on which it was called.

### flip

Reverses the order of (all of) the descendants of the Branch.

Returns **[Branch][108]** The Branch on which this was called.

### getAncestors

Returns an Array of all the ancestors of the Branch on which it is called.
Note that this does not include itself. For all ancestors and itself, see
[Branch.ancestors][9]

#### Parameters

-   `includeSelf` **[Boolean][118]** Should the Branch on which this is called be
    included in the results?

Returns **[Array][109]** Every Ancestor of the Branch on which it was called.

### getChild

Given an `childID`, returns the child with that id (or `undefined` if no such
child is present).

#### Parameters

-   `childID` **[String][104]** the ID of the child to return.

Returns **([Branch][108] \| [undefined][119])** The desired child Branch, or `undefined` if the
child doesn't exist.

### getDescendant

Given an id string, returns the descendant Branch with that ID, or
`undefined` if it doesn't exist.

#### Parameters

-   `id` **[String][104]** The id string of the Branch to find

Returns **([Branch][108] \| [undefined][119])** The descendant Branch, or `undefined` if it
doesn't exist

### getDescendants

Returns an array of all Branches which are descendants of this Branch

#### Parameters

-   `includeSelf` **[Boolean][118]?** Is this not the Branch on which the user
    called the function? This is used internally and should be ignored.

Returns **[Array][109]** An array of all Branches descended from this Branch

### getLeafs

Returns an array of all leaves which are descendants of this Branch.
Alias of [getLeaves][120] for people whose strong suit isn't spelling.

Returns **[Array][109]** An array of all leaves descended from this Branch

### getLeaves

Returns an array of all leaves which are descendants of this Branch
See also: [getLeafs][121]

Returns **[Array][109]** An array of all leaves descended from this Branch

### getMRCA

Traverses the tree upward until it finds the Most Recent Common Ancestor
(i.e. the first Branch for which both the Branch on which it was called and
`cousin` are descendants).

#### Parameters

-   `cousin`  

Returns **[Branch][108]** The Most Recent Common Ancestor of both the Branch on
which it was called and the `cousin`.

### getRoot

Traverses the tree upward until it finds the root Branch, and returns the
root.

Returns **[Branch][108]** The root Branch of the tree

### hasChild

Determines if a given Branch (or ID) is a child of this Branch

#### Parameters

-   `child` **([Branch][108] \| [String][104])** The Branch (or the id thereof) to check for

Returns **[Boolean][118]** 

### hasDescendant

Checks to see if `descendant` is a descendant of the Branch on which this
method is called.

#### Parameters

-   `descendant` **([Branch][108] \| [String][104])** Either the descendant Branch or its'
    `id`.

Returns **[Boolean][118]** True if `descendant` is descended from the Branch from
which this is called, otherwise false.

### hasLeaf

Checks to see if a Branch has a descendant leaf.

#### Parameters

-   `leaf`  

Returns **[Boolean][118]** True if leaf is both a leaf and a descendant of the
Branch on which this method is called, False otherwise.

### invert

Swaps the branch on which it is called with its parent. This method is
probably only useful as an internal component of [Branch.reroot][73].

Returns **[Branch][108]** The Branch object on which it was called.

### isChildOf

Returns whether the Branch on which it is called is a child of a given parent
(or parent ID).

#### Parameters

-   `parent` **([Branch][108] \| [String][104])** A Branch (or ID thereof) to test for
    paternity of this Branch.

Returns **[Boolean][118]** True is `parent` is the parent of this Branch, false
otherwise.

### isConsistent

Tests whether this and each descendant Branch holds correct links to both
its parent and its children.

Returns **[Boolean][118]** True if consistent, otherwise false

### isDescendantOf

Returns whether a given Branch is an ancestor of the Branch on which this
method is called. Uses recursive tree-climbing.

#### Parameters

-   `ancestor` **[Branch][108]** The Branch to check for ancestorhood

Returns **[Boolean][118]** If this Branch is descended from `ancestor`

### isLeaf

Returns a boolean indicating if this Branch is a leaf (i.e. has no
children).

Returns **[Boolean][118]** True is this Branch is a leaf, otherwise false.

### isolate

Returns a boolean indicating whether or not this Branch is olate.

...Just kidding!

Isolates a Branch and its subtree (i.e. removes everything above it, making
it the root Branch). Similar to [Branch.remove][70], only it returns
the Branch on which it is called.

Returns **[Branch][108]** The Branch object on which it was called.

### isRoot

Returns a boolean indicating if this Branch is the root of a tree (i.e. has
no parents).

Returns **[Boolean][118]** True if this Branch is the root, otherwise false.

### leafs

Returns the array of leaf nodes in traversal order; leaves are nodes with no
children. Alias of [Branch.getLeaves][120] \`cuz spelling is hard.

Type: [Array][109]

### leaves

Returns the array of leaf nodes in traversal order; leaves are nodes with no
children. Alias of [Branch.getLeaves][120].
[d3-hierarchy compatibility method.][122]

Type: [Array][109]

### links

Returns an Array of links, which are plain javascript objects containing a
`source` attribute (which is a reference to the parent Branch) and a `target`
attribute (which is a reference to the child Branch).
[d3-hierarchy compatibility method][123]

Returns **[Array][109]** An array of plain Javascript objects

### normalize

Normalizes this and all descendant Branches `value` attributes to between
`newmin` and `newmax`. Note that normalize can function as its own inverse
when passed an original range. For example:

#### Parameters

-   `newmin` **[Number][113]** The desired minimum value.
-   `newmax` **[Number][113]** The desired maximum value.

#### Examples

```javascript
tree.normalize().normalize(1, tree.getDescendants().length + 1);
```

Returns **[Branch][108]** The Branch on which it was called.

### path

Gets the path from this Branch to `target`. If this Branch and `target` are
the same, returns an array containing only the Branch on which it is called.

#### Parameters

-   `target` **[Branch][108]** A Branch object

Returns **[Array][109]** An ordered Array of Branches following the path between this
Branch and `target`

### remove

Removes a Branch and its subtree from the tree. Similar to
[Branch.isolate][60], only it returns the root Branch of the tree
from which this Branch is removed.

Returns **[Branch][108]** The root of the remaining tree.

### replace

Removes a Branch and its subtree from the tree, and replaces it.

#### Parameters

-   `replacement` **[Branch][108]** The branch to replace the branch on which the
    method is called.

Returns **[Branch][108]** The root of the modified tree.

### reroot

Reroots a tree on this Branch. Use with caution, this returns the new root,
which should typically supplant the existing root Branch object, but does
not replace that root automatically.

#### Examples

```javascript
tree = tree.children[0].children[0].reroot();
```

Returns **[Branch][108]** The new root Branch, which is the Branch on which this was
called

### rotate

Reverses the order of the children of the branch on which it is called.

#### Parameters

-   `recursive`  

Returns **[Branch][108]** The Branch on which this was called.

### setLength

Set the length of a Branch

#### Parameters

-   `length` **[number][113]** The new length to assign to the Branch

Returns **[Branch][108]** The Branch object on which this was called

### setParent

Sets the parent of the Branch on which it is called.

#### Parameters

-   `parent` **[Branch][108]** The Branch to set as parent

Returns **[Branch][108]** The Branch on which this method was called.

### simplify

Collapses each descendant Branch with exactly one child into a single
continuous branch.

Returns **[Branch][108]** The Branch on which this method was called.

### sort

Sorts the Tree from the branch on which it is called downward.

#### Parameters

-   `comparator` **[Function][115]?** A Function taking two Branches and returning
    a numberic value. For details, see [MDN Array.sort][124]

Returns **[Branch][108]** The Branch on which it was called

### sources

Determines whether this Branch is likelier to be a source of `cousin`, or
if `cousin` is a source of this Branch.

#### Parameters

-   `cousin` **[Branch][108]** The other Branch to test

Returns **[Boolean][118]** True if this might be the source of cousin, otherwise
false.

### sum

Computes the value of each Branch according to some valuator function

#### Parameters

-   `value` **[Function][115]** A Function taking a Branch and returning a
    (numeric?) value.

Returns **[Branch][108]** The Branch on which it was called.

### targets

Determines whether this Branch is likelier to be a target of `cousin`, or
if `cousin` is a target of this Branch.

#### Parameters

-   `cousin` **[Branch][108]** The other Branch to test

Returns **[Boolean][118]** True if this might be the target of cousin, otherwise
false.

### toJSON

toJSON is an alias for [toObject][125], enabling the safe use of
`JSON.stringify` on Branch objects (in spite of their circular references).

Type: [Function][115]

Returns **[Object][107]** A serializable Object

### toMatrix

Computes a matrix of all patristic distances between all leaves which are
descendants of the Branch on which this method is called.

Returns **[Object][107]** An Object containing a matrix (an Array of Arrays) and
Array of `id`s corresponding to the rows (and columns) of the matrix.

### toNewick

Returns the Newick representation of this Branch and its descendants.

#### Parameters

-   `nonterminus` **[Boolean][118]** Is this not the terminus of the
    Newick Tree? This should be falsy when called by a user (i.e. you). It's
    used internally to decide whether or not in include a semicolon in the
    returned string. (optional, default `falsy`)

Returns **[String][104]** The [Newick][126]
representation of the Branch.

### toObject

Returns a simple Javascript object version of this Branch and its
descendants. This is useful in cases where you want to serialize the tree
(e.g. `JSON.stringify(tree)`) but can't because the tree contains circular
references (for simplicity, elegance, and performance reasons, each Branch
tracks both its children and its parent).

Returns **[Object][107]** A serializable bare Javascript Object representing this
Branch and its descendants.

### toString

Returns a valid JSON-string version of this Branch and its descendants.

#### Parameters

-   `replacer` **[Function][115]** A replacer function to [pass to `JSON.stringify`][127].
-   `width`  
-   `space` **([Number][113] \| [String][104])** A string or number of spaces to use for
    indenting the output. See [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify#Parameters][127]
    for additional details.

Returns **[Object][107]** A valid JSON string representing this Branch and its
descendants.

## parseJSON

Parses a hierarchical JSON string (or Object) as a Branch object.

### Parameters

-   `json` **([String][104] \| [Object][107])** A json string (or Javascript Object)
    representing hierarchical data.
-   `idLabel` **[String][104]** The key used in the objects of `json` to
    indicate their identifiers. (optional, default `"id"`)
-   `lengthLabel` **[String][104]** The key used in the objects of `json`
    to indicate their length. (optional, default `'length'`)
-   `childrenLabel` **[String][104]** The key used in the objects of
    `json` to indicate their children. (optional, default `` `children` ``)

Returns **[Branch][108]** The Branch representing the root of the hierarchy
represented by `json`.

## parseMatrix

Parses a matrix of distances and returns the root Branch of the output tree.
This is adapted from Maciej Korzepa's [neighbor-joining][128],
which is released for modification under the [MIT License][129].

### Parameters

-   `matrix` **[Array][109]** An array of `n` arrays of length `n`
-   `labels` **[Array][109]** An array of `n` strings, each corresponding to the
    values in `matrix`.

Returns **[Branch][108]** A Branch object representing the root Branch of the tree
inferred by neighbor joining on `matrix`.

## parseNewick

Parses a Newick String and returns a Branch object representing the root
of the output Tree.
This is adapted Jason Davies' [newick.js][130],
which is released for modification under [the MIT License][129].

### Parameters

-   `newick` **[string][104]** A Newick String

Returns **[Branch][108]** A Branch representing the root of the output tree

[1]: #version

[2]: #examples

[3]: #branch

[4]: #parameters

[5]: #addchild

[6]: #parameters-1

[7]: #addparent

[8]: #parameters-2

[9]: #ancestors

[10]: #clone

[11]: #consolidate

[12]: #copy

[13]: #count

[14]: #descendants

[15]: #depthof

[16]: #parameters-3

[17]: #distancebetween

[18]: #parameters-4

[19]: #distanceto

[20]: #parameters-5

[21]: #each

[22]: #parameters-6

[23]: #eachafter

[24]: #parameters-7

[25]: #eachbefore

[26]: #parameters-8

[27]: #eachchild

[28]: #parameters-9

[29]: #excise

[30]: #fixdistances

[31]: #fixparenthood

[32]: #parameters-10

[33]: #flip

[34]: #getancestors

[35]: #parameters-11

[36]: #getchild

[37]: #parameters-12

[38]: #getdescendant

[39]: #parameters-13

[40]: #getdescendants

[41]: #parameters-14

[42]: #getleafs

[43]: #getleaves

[44]: #getmrca

[45]: #parameters-15

[46]: #getroot

[47]: #haschild

[48]: #parameters-16

[49]: #hasdescendant

[50]: #parameters-17

[51]: #hasleaf

[52]: #parameters-18

[53]: #invert

[54]: #ischildof

[55]: #parameters-19

[56]: #isconsistent

[57]: #isdescendantof

[58]: #parameters-20

[59]: #isleaf

[60]: #isolate

[61]: #isroot

[62]: #leafs

[63]: #leaves

[64]: #links

[65]: #normalize

[66]: #parameters-21

[67]: #examples-1

[68]: #path

[69]: #parameters-22

[70]: #remove

[71]: #replace

[72]: #parameters-23

[73]: #reroot

[74]: #examples-2

[75]: #rotate

[76]: #parameters-24

[77]: #setlength

[78]: #parameters-25

[79]: #setparent

[80]: #parameters-26

[81]: #simplify

[82]: #sort

[83]: #parameters-27

[84]: #sources

[85]: #parameters-28

[86]: #sum

[87]: #parameters-29

[88]: #targets

[89]: #parameters-30

[90]: #tojson

[91]: #tomatrix

[92]: #tonewick

[93]: #parameters-31

[94]: #toobject

[95]: #tostring

[96]: #parameters-32

[97]: #parsejson

[98]: #parameters-33

[99]: #parsematrix

[100]: #parameters-34

[101]: #parsenewick

[102]: #parameters-35

[103]: https://semver.org/

[104]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String

[105]: #parseNewick

[106]: #parseMatrix

[107]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object

[108]: #branch

[109]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array

[110]: https://github.com/d3/d3-hierarchy#node_ancestors

[111]: https://github.com/d3/d3-hierarchy#node_copy

[112]: https://github.com/d3/d3-hierarchy#node_descendants

[113]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number

[114]: https://en.wikipedia.org/wiki/Breadth-first_search

[115]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function

[116]: https://en.wikipedia.org/wiki/Tree_traversal#Post-order

[117]: https://en.wikipedia.org/wiki/Tree_traversal#Pre-order

[118]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean

[119]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/undefined

[120]: #getLeaves

[121]: #getLeafs

[122]: https://github.com/d3/d3-hierarchy#node_leaves

[123]: https://github.com/d3/d3-hierarchy#node_links

[124]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort#Description

[125]: #toObject

[126]: https://en.wikipedia.org/wiki/Newick_format

[127]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify#Parameters

[128]: https://github.com/biosustain/neighbor-joining

[129]: https://opensource.org/licenses/MIT

[130]: https://github.com/jasondavies/newick.js/blob/master/src/newick.js
