
##Maintain Scroll Position

###Maintain Scroll Position Script
This will set same scroll position before/after you submit form data.

```javascript
 <!--
    function MaintainPositionGetCoords() {
       var scrollX, scrollY;
       
       if (document.all) {
          if (!document.documentElement.scrollLeft)
             scrollX = document.body.scrollLeft;
          else
             scrollX = document.documentElement.scrollLeft;
                
          if (!document.documentElement.scrollTop)
             scrollY = document.body.scrollTop;
          else
             scrollY = document.documentElement.scrollTop;
       }   
       else {
          scrollX = window.pageXOffset;
          scrollY = window.pageYOffset;
       }
    
       document.forms[formID].xCoordHolder.value = scrollX;
       document.forms[formID].yCoordHolder.value = scrollY;
    }
    
    function MaintainPositionScroll() {
       var x = document.forms[formID].xCoordHolder.value;
       var y = document.formsformID].yCoordHolder.value;
       window.scrollTo(x, y);
    }
    
    window.onload = MaintainPositionScroll;
    window.onscroll = MaintainPositionGetCoords;
    window.onkeypress = MaintainPositionGetCoords;
    window.onclick = MaintainPositionGetCoords;
 // -->
 <script>
 
 ```



