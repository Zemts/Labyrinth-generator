
# Labyrinths generator. #



## What does it do : ##
Generate structure of labyrinths (returns structure for 'comfortable' rendering).
Used scripts are located in 'src' folder.



## How to use it (short description) : ##
1.  Call `core.createWorkingSet(elementsGenerator, sizes [, additionalActions])`.
2.  Call `algorithms.generate(workingSet, algorithmName)`.
3.  Render result.



## How to use it (more detailed description) : ##
1.  Call `core.createWorkingSet(elementsGenerator, sizes [, additionalActions])` and save result into variable.

    * Arguments:

        **elementsGenerator** - function that return new element (entity of cell that will be displayed in the document).

        Example:

        ```javascript
        function(){
            return document.createElement('div');
        }
        ```

        **sizes** - object with 2 properties, rows - number of rows, columns - number of columns.

        Note, 'sizes' must consist of odd numbers (because part of elements are used as 'walls').

        Example:

        ```javascript
        {
            'rows' : 21,
            'columns' : 21
        }
        ```

        **additionalAction** - object with actions that will be used like callbacks in standart methods.
        
        Note that at this moment only 'setPath' and 'setWall' actions are used.
        
        Example:

        ```javascript
        {
            'setPath' : function(element){
                element.style.backgroundColor = 'purple';
            },
            'setWall' : function(element){
                element.style.backgroundColor = 'pink';
            }
        }
        ```

    * Return value: 2d array.

2.  Call `algrorithms.generate(workingSet, algorithmName)`.
    
    * Arguments:

        **workingSet** - object returned by executing core.createWorkingSet(...)

        **algorithmName** - string with name of algorithm.

        Note that at this moment only 'simple' and 'Eller' names are available.

        Example:

        ```javascript
        'simple'
        ```

    * Warning: this function modify 'workingSet' argument !

    * Return value: undefined.

3.  Render each element of 2d array from step 1 (Your part of code).

    Example:
    
    ```javascript
    let line;
    for(let i = 0; i < workingSet.length; i++){
        line = createElement('div');
        for(let j = 0; j < workingSet[i].length; j++){
            line.appendChild(workingSet[i][j].element);  // .element - result of 'elementsGenerator' function
        }
        document.body.appendChild(line);
    }
    ```



## Full example: ##

```html
<html>
    <head>
        <script src='src/core.js'></script>
        <script src='src/algorithms.js'></script>
    <head>
    <body></body>
    <script>
        function elementsGenerator(){
            var div = document.createElement('div');
            div.style.height = '10px';
            div.style.width = '10px';
            div.style.display = 'inline-block';
            div.style.position = 'relative';
            return div;
        }
        var actions = {
            'setWall' : function(el){
                el.style.backgroundColor = 'black'; // for visual clarity
            }
        }
        var ws = core.createWorkingSet(elementsGenerator, { 'rows' : 15, 'columns' : 15 }, actions);
        algorithms.generate(ws, 'Eller');
        let row;
        for(let i = 0; i < ws.length; i++){
            row = document.createElement('div');
            for(let j = 0; j < ws[i].length; j++){
                row.appendChild(ws[i][j].element);
            }
            document.body.appendChild(row);
        }
    </script>
</html>
```



## More colorful example: ##
For see it, download index.html file, 'src' and 'example' folders



## Browser supports (for scripts from 'src' folder): ##
1.  IE : 9+
2.  Chrome : 1+
3.  Firefox : 1.5+
