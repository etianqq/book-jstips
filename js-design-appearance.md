# 外观模式


通过把常用方法包装到一个新方法中，从而提供一个更为便利的API。


var myEvent={
  //...
  stop: function(){
    if(typeof e.preventDefault === 'function'){
      e.preventDefault();
    }
    
    if(typeof e.stopPropagation === 'function'){
      e.stopPropagation();
    }
    
    if(typeof e.returnValue === 'boolean'){
      e.returnValue = false;
    }
    
    if(typeof e.cancelBubble === 'boolean'){
      e.cancelBubble = true;
    }
  }
}