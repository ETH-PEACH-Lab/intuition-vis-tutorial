## myDSL   
In this section, we will introduce myDSL grammar and show how to use myDSL to generate intuition visulization.  

### Basic Concepts
There are 3 basic concepts: `unit`, `component` and `page`. `Unit` is the smallest part that can be manipulated, such as each node in a `tree` diagram. `Units` form `components`. Currently, our editor supports 6 types of components: `array`, `linkedlist`, `tree`, `stack`, `matrix` and `graph`. Several `components` make up a `page`, and a complete intuition visualization usually has multiple `pages`.  

<img src="/pictures/myDSL_concepts.png" width="500"> 

### myDSL Grammar

#### Fabonacci Array Examble
```javascript

data:
array arr1 = {
  structure:[[1],[1,1],[1,1,2],[1,1,2,3],[1,1,2,3,5],[1,1,2,3,5,8]]
  value:[[1],[1,1],[1,1,2],[1,1,2,3],[1,1,2,3]]
  color:[[null],[null,null],[null,null,null],[null,null,null,null],[null,null,null,null]]
  arrow:[[null],[null,null],[null,null,null],[null,null,null,null],[null,null,null,null]]
  hidden:[[false],[false,false],[false,false,false],[false,false,false,false],[false,false,false,false]]
}
draw:
page p:=[0,5] {
show arr1[p]
}
```  
In `data` part, user describe each component's `structure` and other attributes fo several pages. For instance, `[1]` is the value in page 1, `[1,1]` is the value in page 2.  
In `draw` part, user choose to render which component they describe in `data` part.

#### Grammar of Different Components  
##### Value Type  
`ID`, `Number` and `Boolean` type are 3 type accepted as input. They are defined by:
```javascript
// only consists of numeric digits
Number -> [0-9]:+ 

// must start with alphabet, consists of alphabet and numeric digits 
ID -> [a-zA-Z0-9\/\\<>#@$&|]:+ 

// be false or true
Boolean -> false || true
```


##### Array
```javascript
array array_component_name = {
structure:[[ID || Number]] //required
value:[[ID]] // optional, when ther is no value, will copy strucrure value 
color:[[ID]] // optional
arrow:[[ID]] // optional
hidden:[[Boolean]] // optional
}
```
Here is an example of array component:
```javascript
array arr1 = {
  structure:[[1],[1,1],[1,1,2]]
  value:[[1],[1,1]]
  color:[[null]]
  arrow:[[null]]
}
```

##### Stack  
```javascript
stack stack_component_name = {
structure:[[ID || Number]] //required
value:[[ID]] // optional, when ther is no value, will copy strucrure value 
color:[[ID]] // optional
arrow:[[ID]] // optional
hidden:[[Boolean]] // optional
}
```
Here is an example of stack component:
```javascript
stack stk1 = {
  structure:[[1],[1,1],[1,1,2]]
  value:[[1],[1,1]]
}
```

##### Tree  
```javascript
tree tree_component_name = {
structure:[[ID]] //required
value:[[ID]] // optional, when ther is no value, will copy strucrure value 
color:[[ID]] // optional
arrow:[[ID]] // optional
hidden:[[Boolean]] // optional
}
```
Here is an example of tree component:
```javascript
tree tr1 = {
  structure:[[n1],[n1,n2],[n1,n2,n3]]
  value:[[1],[1,2],[1,2,3]]
  color:[[null]]
  arrow:[[null]]
}
```

##### Linkedlist  
```javascript
linkedlist linkedlist_component_name = {
structure:[[ID]] //required
value:[[ID]] // optional, when ther is no value, will copy strucrure value 
color:[[ID]] // optional
arrow:[[ID]] // optional
hidden:[[Boolean]] // optional
}
```
Here is an example of linkedlist component:  
```javascript
linkedlist li1 = {
  structure:[[n1],[n1,n2],[n1,n2,n3]]
  value:[[1],[1,2],[1,2,3]]
  color:[[null]]
  arrow:[[null]]
}
```

##### Matrix
```javascript
linkedlist linkedlist_component_name = {
structure:[[[ID || Number]]] //required
value:[[[ID]]] // optional, when ther is no value, will copy strucrure value 
color:[[[ID]]] // optional
arrow:[[[ID]]] // optional
hidden:[[[Boolean]]] // optional
}
```
Here is an example of matrix component:
```javascript
matrix mr1 = {
  structure:[[[1,2],[3,4]],[[1,2,3],[3,4]]]
}
```

##### Graph 
```javascript
graph graph_component_name = {
id:[[ID]] //required
edge:[[(ID,ID)]] // required
color:[[ID]] // optional
arrow:[[ID]] // optional
hidden:[[ID]] // optional
}
```
Here is an example of graph component:
```javascript
graph dfs = {
  id:[[n1,n2,n3,n4,n5,n6,n7,n8]]
  edge:[[(n1,n2),(n4,n8)]]
  value:[[n1,n2,n3,n4,n5,n6,n7,n8]]
  color:[[red,null,null,null,null,null,null,null]]
}
```
##### Notice
- `null` is a reserved key word for `arrow` attribute, it means no arrow on this unit.
- `empty` is a reserved key word for `arrow` attribute, it means a arrow without label.
  <img src="/pictures/myDSL_empty_arrow.png" width="300">

#### Grammar of Draw  
For each page, user need to explicitely decide which component to be rendered on this page. 
First, user needs to choose page range by `page page_index := [Number1, Number2]`. The range starts with 0 and includes the start and end.  
Then, user needs to choose to render which component using `show component_name[page_index]`. Here user can also use expression with `page_index` to choose component.
```javascript
page page_index := [Number, Number] {
show component_name[page_index]
}
```
This is a example of full draw part:
```javascript
draw:
page p = [0,1] {
show component_name_1[p + 1]
show component_name_2[p]
}
page i = [2,3] {
show component_name_1[i - 1]
show component_name_2[i]
}
```
##### Notice
For `page_index expression`, only simple ones such as `p + 2` , `p - 1` is supported now. Always keep the coefficient before `page_index` as 1. Such as `1 - p `, `2 * p` are not supported so far.