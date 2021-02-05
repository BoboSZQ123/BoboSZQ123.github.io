# JaMoskeeto的three.js博客，第一天
## 安装和基本三大组建的创建和配置
```
安装（2种方法）
1. https://cdn.staticfile.org/three.js/r{version}/three.js
   在同目录下创建一个HTML文件，里面包括<script src="https://cdn.staticfile.org/three.js/r{version}/three.js"></script>来引用three.js
   version是版本，现在有125了
   可以在HTML里面的script里面写代码，也可以引用外部js代码
2. https://github.com/mrdoob/three.js/releases/tag/r125
   github里下载，在这个页面滚动到底，就可以看到一个
   Source code(zip)
   Source code(tar.gz)
   第一个是zip格式
   第二个是gz格式

创建一个场景
var scene=new THREE.Scene()
可以创建一个场景

创建一个透视相机
var camera=new THREE.PerspectiveCamera(fov,aspect,near,far)
创建一个透视相机，fov代表视角（参数越大，场景的模型越小），aspect表示横纵比，一般设置成window.innerWidth / window.innerHeight表示窗口宽高比，near表示近平面（近处的裁面距离），far（远处的裁面距离），near和far不能为负值
一般可以设置成
var camera=new THREE.PerspectiveCamera(75,window.innerWidth / window.innerHeight,1,1000)

设置相机的位置
camera.position.dir=val
dir可以是x、y或z，表示相机的位置需要在dir所对应的轴上移动到val
x：相机向右移动到val（场景向左移动）
y：相机向上移动到val（场景向下移动）
z：相机向后移动到val（场景向前移动）        
默认值x，y，z都是0，在原点

设置相机快门的方向
camera.up.dir=val
dir可以是x、y或z，val只能是0，-1或1，表示相机的上方
x：val是1表示相机的快门以x轴为上方，-1为下方
y：val是1表示相机的快门以y轴为上方（默认），-1为下方
z：val是1表示相机的快门以z轴为上方，-1为下方
注意：值有camera.up不够，需要配合下面的camera.lookAt()来生效
camera.up.set(x,y,z)可以一步设置camera.up

设置相机的焦点位置
camera.lookAt(new THREE.Vector3(x,y,z))
相机看向的焦点
看向的点要和快门方向垂直，不然会有问题

创建一个渲染器
var renderer=new THREE.WebGLRenderer()
在括号里添加{antialias:true}可以抗锯齿，画线段时更平滑

调整需要渲染大小
renderer.setSize(width,height)
一般可以设置成
renderer.setSize(window.innerWidth,window.innerHeight)

在body中加入渲染器
document.body.appendChild(renderer.domElement)
添加当作DOM元素类型的渲染器

开始渲染
创建render函数
   function render(){
   ...
   }
需要执行的指令写在函数最前面，以下是渲染函数
renderer.clear()
初始化渲染器
renderer.render(scene,camera)
进行渲染器渲染场景和相机
requestAnimationFrame(render)
调用render函数，重复渲染

在函数外调用render函数
render()

清除背景
因为默认背景是黑的，所以我们需要
renderer.setClearColor('')
来把背景设定成color色（颜色名）
```
