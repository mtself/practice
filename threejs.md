# Three.js（2.1.2开始）
## 语法
#### THREE.Scene中常用方法及属性
* `scene.add(object)`  
向场景中添加对象，该方法还可以创建对象组
* `scene.children`  
返回一个场景中所有对象的列表（包括摄像机和光源）
* `scene.getObjectByName(name,recursive)`  
创建对象时可指定唯一标识name，该方法可查找特定名字的对象。  
recursive设置为false时，在调用者子元素上查找；设置为true时，在所有后代对象中查找
* `scene.remove(object)`  
将对象从场景中移除
* `scene.traverse(function)`  
  ```javascript
  scene.traverse(function (e) {
            if (e instanceof THREE.Mesh && e != plane) {
                e.rotation.x += controls.rotationSpeed;
            }
        });
  ```  
  我们可以将一个方法作为参数传递给traverse()方法，这个传递来的方法将会在每一个子对象上执行。for循环和forEach遍历可达到同样的效果
* `scene.fog = new THREE.Fog(0xffffff, 10, 100);`  
雾化效果（颜色，近端，远端），雾的浓度线性增长  
 `scene.fog = new THREE.FogExp2(0xffffff, 0.01);`  
雾化效果（颜色，浓度），雾的浓度随距离呈指数增长
* ```javascript
  scene.overrideMaterial = new THREE.MeshLambertMaterial({
        color: 0xffffff
  });  
  ```  
  场景中所有的物体都会使用该属性指向的材质，即使物体本身也设置了材质。当某一个场景中所有物体都共享同一个材质时，使用该属性可以通过减少Three.js管理的材质数量来提高运行效率，但是实际应用中，该属性通常并不非常实用。  
#### 几何体和网格
* 创建步骤
  ```javascript
  //定义物体形状
  var cubeGeometry = new THREE.BoxGeometry(4, 4, 4);
  //定义物体材质
  var cubeMaterial = new THREE.MeshLambertMaterial({ color: 0xff0000 });
  //形状和材质合并成能加进场景的mesh
  var cube = new THREE.Mesh(cubeGeometry, cubeMaterial);
  //开启阴影
  cube.castShadow = true;
  //修改物体的位置，大小，角度
  cube.position.x = -4;
  // 添加到场景中
  scene.add(cube);
  ```
* 使用顶点和面自己建几何体  
  ```javascript
  var vertices = [
    new THREE.Vector3(1,3,1),
    new THREE.Vector3(1,3,-1),
    new THREE.Vector3(1,-1,1),
    new THREE.Vector3(1,-1,-1),
    new THREE.Vector3(-1,3,-1),
    new THREE.Vector3(-1,3,1),
    new THREE.Vector3(1,3,1),
    new THREE.Vector3(-1,-1,-1),
    new THREE.Vector3(-1,-1,1)
  ];

  var faces = [
    new THREE.Face3(0,2,1);
    new THREE.Face3(2,3,1);
    new THREE.Face3(4,6,5);
    new THREE.Face3(6,7,5);
    new THREE.Face3(4,5,1);
    new THREE.Face3(5,0,1);
    new THREE.Face3(7,6,2);
    new THREE.Face3(6,3,2);
    new THREE.Face3(5,7,0);
    new THREE.Face3(7,2,0);
    new THREE.Face3(1,3,4);
    new THREE.Face3(3,6,4);
  ];
  
  var geom = new THREE.Geometry();
  geom.vertices = vertices;
  geom.faces = faces;
  geom.computeFaceNormals();



***
## 注意
* 雾化效果：离摄像机越远越模糊
* threejs会将camera自动添加，但手动添加要更好一点，尤其是有多个摄像机的时候
* 场景：在渲染时你想使用的所有物体、光源的容器
* 自己用vertices和faces创建面的时候要注意顶点的顺序，面向摄像机的按顺时针顺序，背向镜头的用逆时针顺序