# Three.js（2.1.2开始）
## 语法
* `scene.traverse()`  
我们可以将一个方法作为参数传递给traverse()方法，这个传递来的方法将会在每一个子对象上执行。for循环和forEach遍历可达到同样的效果
* `scene.fog = new THREE.Fog(0xffffff, 10, 100);`  
雾化效果（颜色，近端，远端），雾的浓度线性增长
* `scene.fog = new THREE.FogExp2(0xffffff, 0.01);`  
雾化效果（颜色，浓度），雾的浓度随距离呈指数增长
* ```javascript
  scene.overrideMaterial = new THREE.MeshLambertMaterial({
        color: 0xffffff
  });
  ```  
  场景中所有的物体都会使用该属性指向的材质，即使物体本身也设置了材质。当某一个场景中所有物体都共享同一个材质时，使用该属性可以通过减少Three.js管理的材质数量来提高运行效率，但是实际应用中，该属性通常并不非常实用。
* THREE.Scene中常用方法及属性
![scene 属性](C:\Users\arasmt\Pictures\threejs\2023_6_13.jpg)

***
## 注意
* 雾化效果：离摄像机越远越模糊
* threejs会将camera自动添加，但手动添加要更好一点，尤其是有多个摄像机的时候
* 场景：在渲染时你想使用的所有物体、光源的容器
* 