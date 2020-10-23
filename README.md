# JxCode.PSExporter
 PhotoShop资源导出工具，自动裁剪与命名，导出图层位置与图层关系、对象层属性等数据，可用于资源导出与UI制作的自动化。

## 该工具的应用范围
按照对图层与组的属性设置自动裁剪缩放并导出图片。  
导出图片的同时导出该图像的坐标，大小，不透明度等信息。  
图层对象导出对象信息，如文本层的字体，大小，颜色，对齐方式等。

除了图片外还会导出一个xml文档，记录的图片的多种信息。
在此基础之上的二次开发，用于如UI的自动拼接与生成代码等工作。

## 图层命名规则：  
#### 普通图层命名：
* 图层1  
* 图层2.png  
#### 导出的图层命名：
* @图层1.png  
* @图层2.png;  
#### 带有属性的图层命名：（除@外的属性顺序可以随意）  
* @图层1.png;|$9  
* @图层2.png;#元数据;|64x64   

属性符号|参数|参数默认值|导出时必选|说明
--|--|--|--|--
@|文件名|无|二选一|标记图层导出图片文件和数据，参数是导出的文件名，支持png/jpg/jpeg/bmp/tga格式，如后面有其他属性，使用';'来结束。
~|图片名|无|二选一|标记图层为一个外部文件，仅导出图层数据，如后面有其他属性，使用';'来结束。
\||64x64|按照图层边缘最小裁剪|否|该图层将被裁剪。
\#|自定义字符串|无|否|一个TAG，原封不动的导出至xml，使用;来结束，如有内容中有;字符则需要使用\\来转义。
$|0~9|5|否|图片导出质量，省略属性与省略参数都会使用参数默认值。  
?|类型名|无|否|该图片的类型，原封不动的导出至xml，使用;来结束，如有内容中有;字符则需要使用\\来转义。
<||无|否|图层向上合并，使用本图层名作为合并后图层名。（2级预处理）
\>||无|否|图层向下合并，使用本图鞥名作为合并后图层名。（2级预处理）
另外，该属性设置并非仅对图层生效，同时也对组生效，当为组设置导出属性时，组会自动将组内可视图层合并，变为一个普通的图层。  
如果没有对组设置属性，那么这个组就会变成一个节点，成为子图层的父对象，该数据会被导出至xml。