- 标签结构

  ```html
  <div class="grid">
  
      <div class="item"> <!--用于计算位置-->
          <div class="item-content">  <!--用于显示/隐藏-->
              <!-- Safe zone, enter your custom markup -->
              This can be anything.
              <!-- Safe zone ends -->
          </div>
      </div>
  
      <div class="item">
          <div class="item-content">
              <!-- Safe zone, enter your custom markup -->
              <div class="my-custom-content">
                  Yippee!
              </div>
              <!-- Safe zone ends -->
          </div>
      </div>
  
  </div>
  ```
 
- 以下方式只会渲染页面第一个该类的标签
    
    ```javascript
    var grid = new Muuri('.grid', {})
    ```
- 拖拽的元素不一定要在容器标签内，可以初始化的适合通过配置项传入
    
    ```javascript
    var grid = new Muuri('.grid', {
            items:document.querySelectorAll('.item'),
    })
    ```
- 可以给配置layout传递一个函数，进行自定义布局
 
    ```javascript
    var grid = new Muuri('.grid', {
            layout: function (items, gridWidth, gridHeight) { //所有可拖拽元素的对象数组，整个容器的宽度、高度
                        console.log("layout",items, gridWidth, gridHeight)
                        // The layout data object. Muuri will read this data and position the items
                        // based on it.
                        var layout = {
                            // The layout's item slots (left/top coordinates).
                            slots: [],
                            // The layout's total width.
                            width: 0,
                            // The layout's total height.
                            height: 0,
                            // Should Muuri set the grid's width after layout?
                            setWidth: true,
                            // Should Muuri set the grid's height after layout?
                            setHeight: true
                        };
            
                        // Calculate the slots.
                        var item;
                        var m;
                        var x = 0;
                        var y = 0;
                        var w = 0;
                        var h = 0;
                        for (var i = 0; i < items.length; i++) {
                            item = items[i];
                            x += w;
                            y += h;
                            m = item.getMargin();
                            w = item.getWidth() + m.left + m.right;
                            h = item.getHeight() + m.top + m.bottom;
                            layout.slots.push(x, y);
                        }
            
                        // Calculate the layout's total width and height.
                        layout.width = x + w;
                        layout.height = y + h;
            
                        return layout;
            }
    })
    
    ```
- 不管如何拖拽调整元素位置，实际的dom的顺序是不变的（即初始时的顺序）,通过设置top和left来实现视觉上的编排
- 可以在任何时候手动获取排序的数据，
  
    ```javascript
    grid.refreshSortData();  //获取排序后的数据
    ```
    
