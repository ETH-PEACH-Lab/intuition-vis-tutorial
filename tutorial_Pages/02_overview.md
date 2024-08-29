## Overview

In this section, we will have a overview of the whole system and see how it works. We will use a easy example to show its work flow. 

### Create an intuition for Fibonacci number

#### problem description 

The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. That is,
```
F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2), for n > 1.
```
Now let's make the intution for Fibonacci!
#### Code myDSL to make templates
Now, we will make the first page of our intuition visualization. Let's input some data in `Code Editor` to describe the data structure of Fabonacci array. We also input some attributes such as `color`, `arrow` to describe the style of Fabonacci array.
<!-- ![alt text](/pictures/overview_codeEditor1.png)  -->
<img src="/pictures/overview_codeEditor1.png" width="500">  
  
After enter input of `Code Editor`, the `Mermaid Editor` below `Code Editor` will generate mermaid code automatically. Compared to myDSL, Mermaid Code is a low-level domain specific language to directly render SVG image.

#### Interact with GUI-tool to adjust unit  
Good! We just make the first page of our Fibonacci intuition. Now, let's make it more vivid. Let's color certain units on it to show how a new Fibonacci number is produced. The 4th Fibonacci number `3` is produced by `3 = 1 + 2`. Let's color it and add an arrow to hightlight `3` is just produced.  
Click on unit `3`, the GUI tool will appear. Let's change the `unit color` and `arrow label` with red and current, then click `update`.

<!-- ![alt text](/pictures/overview_gui.png)   -->
<img src="/pictures/overview_gui.png" width="500">  
  
Now the unit `3` is updated as our input! Let's also update `1` and `2` likewise.
  
#### Add and delete page  
Great! We have 5 pages now, and we want to add a new page to generate the next Fabonacci number. Let's click `Add a page` button on the right-top of GUI-tool to copy the last page.  

<!-- ![alt text](/pictures/overview_addPage.png)   -->
<img src="/pictures/overview_addPage.png" width="500"> 

#### Modify mermaid code when necessary  
Mermaid code is generated from myDSL automatically. But you can also edit it to make more detailed style-control when necessary.
<!-- ![alt text](/pictures/overview_mermaid.png)   -->
<img src="/pictures/overview_mermaid.png" width="500"> 

#### Save your output  
Great! Now we have a nice Fibonacci intuion visualization. Let's click `save` or `export` button to save the svg animation for further use.
<!-- ![alt text](/pictures/overview_save.png)   -->
<img src="/pictures/overview_save.png" width="500"> 