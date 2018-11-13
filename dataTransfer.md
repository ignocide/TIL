# dataTransfer

## 개요

 데이터에 값을 보존 할 때 쓰이며 주로 드래그 앤 드랍에 응용할 떄 주로 쓰인다.

 ## setData

 ```javascript
 const setData = function(event){
   event.dataTransfer.setData('data','item!')
 }
 ```

 ## getData

 ```javascript
 const getData = function(event){
   const data = event.dataTransfer.getData('data')
   //data = "item!"
 }
 ```
