# event.js
dom2级监听器，event事件，冒泡，阻止默认行为兼容IE的写法

    var eventUtil={
             	// 添加监听器
             	addHandler:function(element,type,handler){
                   if(element.addEventListener){
                     element.addEventListener(type,handler,false);
                   }else if(element.attachEvent){
                     element.attachEvent('on'+type,handler);
                   }else{
                     element['on'+type]=handler;
                   }
             	},
             	// 删除监听器
             	removeHandler:function(element,type,handler){
                   if(element.removeEventListener){
                     element.removeEventListener(type,handler,false);
                   }else if(element.detachEvent){
                     element.detachEvent('on'+type,handler);
                   }else{
                     element['on'+type]=null;
                   }
             	},
    
              //调用event对象（兼容IE）
              getEvent:function(event){
                return event?event:window.event;
              },
              //event.type
              getType:function(event){
                return event.type;
              },
              //event.target
              getElement:function(event){
                return event.target || event.srcElement;
              },
              //阻止默认事件
              preventDefault:function(event){
                if(event.preventDefault){
                  event.preventDefault();
                }else{
                  event.returnValue=false;
                }
              },
              //阻止冒泡
             stopPropagation:function(event){
               if(event.stopPropagation){
                 event.stopPropagation();
               }else{
                 event.cancelBubble=true;
               }
             }
      }
