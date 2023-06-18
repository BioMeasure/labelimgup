本项目是Labelimg若干功能的改进版本，主要是为了让标注过程更方便，改进原来某些设计的不合理的地方。  
This project is an improved version of several functions of Labelimg, mainly to make the labeling process more convenient and improve some unreasonable parts of the original design.

原始代码是下载的`1.8.4 (2020-11-04)`版本，参考[HISTORY.rst](https://github.com/tzutalin/labelImg/blob/master/HISTORY.rst)  
The original code is the downloaded `1.8.4 (2020-11-04)` version, refer to [HISTORY.rst](https://github.com/tzutalin/labelImg/blob/master/HISTORY.rst)  

```shell
# 1.安装requirements\requirements-linux-python3.txt中的依赖 
#   Install dependencies in requirements\requirements linux-python3.txt
# 2.对于qt5py3（其它的qt或python版本参考Makefile中具体的命令）
#   For qt5py3 (other qt or python versions refer to the specific commands in the Makefile)
pyrcc5 -o libs/resources.py resources.qrc
# 3.修改data\predefined_classes.txt中的预定义label
#   Modify the predefined labels in data\predefined_classes
# 4.打开软件
#   Open the software
python labelImg.py
```

鼠标划入label清单时高亮提示 Highlight when the mouse is drawn into the label list
---------------------------------------------------------------------

[![](https://github.com/BioMeasure/labelimgup/raw/master/demo/label_list_highlight.gif)
](https://github.com/BioMeasure/labelimgup/blob/master/demo/label_list_highlight.gif)

拖拽鼠标右键快速调整矩形框 Drag the right mouse button to quickly adjust the rectangle
------------------------------------------------------------------------

原始的软件必须要先选中一个顶点然后拖拽修改，当长时间标注数据时，每次先寻找顶点的过程很耗费精力。而右键拖拽时无需先选中某个顶点按钮，直接会将距离鼠标当前位置最近的一个顶点吸附到鼠标。  
The original software had to select a vertex first and then drag and drop to modify it. When labeling data for a long time, the process of finding the vertex every time was very labor-intensive. When right-clicking and dragging, there is no need to select a vertex button first, and the vertex closest to the current position of the mouse will be directly attached to the mouse.[![](https://github.com/BioMeasure/labelimgup/raw/master/demo/drag_rect.gif)
](https://github.com/BioMeasure/labelimgup/blob/master/demo/drag_rect.gif)

目标框叠加在一起时：如果没有选中任何目标框，默认会选择最顶层的目标框激活并吸附最近的顶点。  
When target frames are superimposed: If no target frame is selected, the topmost target frame will be selected by default to activate and absorb the nearest vertex.[![](https://github.com/BioMeasure/labelimgup/raw/master/demo/drag_rect1.gif)
](https://github.com/BioMeasure/labelimgup/blob/master/demo/drag_rect1.gif)

目标框叠加在一起时：如果预先选中了一个特定的目标框，会自动选择被选中的目标框，吸附其最近的顶点，不管其它的目标框。如果遇到一个小框被大框覆盖的情况，只能将大框移开，然后修改小框。通过这个右键拖拽功能，可以先通过高亮提示选中小框，然后直接右键拖拽编辑。  
When target frames are superimposed: If a specific target frame is pre-selected, the selected target frame will be automatically selected, and its nearest vertex will be absorbed, regardless of other target frames. If a small frame is covered by a large frame, you can only remove the large frame and modify the small frame. Through this right-click drag function, you can first select the small box through the highlight prompt, and then directly right-click and drag to edit.[![](https://github.com/BioMeasure/labelimgup/raw/master/demo/drag_rect2.gif)
](https://github.com/BioMeasure/labelimgup/blob/master/demo/drag_rect2.gif)

复制label功能 Copy label function
----------------------------

快捷键：C 如果目前没有选中任何的label，直接复制当前图片的所有label到下一张图片。  
Shortcut key: C If no label is currently selected, directly copy all labels of the current picture to the next picture.[![](https://github.com/BioMeasure/labelimgup/raw/master/demo/copy_all.gif)
](https://github.com/BioMeasure/labelimgup/blob/master/demo/copy_all.gif)

如果目前存在一个选中的label，只会复制这个label到下一张图片，并且继续设置该label为选中状态，以实现连续"C"。  
If there is currently a selected label, it will only copy this label to the next picture, and continue to set the label as selected to achieve continuous "C".[![](https://github.com/BioMeasure/labelimgup/raw/master/demo/copy_one.gif)
](https://github.com/BioMeasure/labelimgup/blob/master/demo/copy_one.gif)

注意，如果前后图片的尺寸不一样，超出图片范围的框的长和宽会被压缩为0。坐标以图片左上角为原点。  
Note that if the sizes of the front and back pictures are different, the length and width of the frame beyond the picture range will be compressed to 0. The coordinates take the upper left corner of the picture as the origin.

修改label的弹窗改进 Modify label pop-up improvement
-------------------------------------------

原来的修改label的弹窗不是很方便，做了一点改进： 快捷键：E （选中目标框并按下后弹出设置窗口）  
The original pop-up window for modifying the label is not very convenient, and a little improvement has been made: Shortcut key: E (select the target box and press it to pop up the setting window)

对于原来的弹窗，如果鼠标位于软件窗口的右侧或下侧，弹窗总会超出软件边界，需要拖拽进来再选择label。现在弹窗的区域直接限制在了整个软件范围之内。  
For the original pop-up window, if the mouse is on the right or bottom side of the software window, the pop-up window will always exceed the boundary of the software, and you need to drag it in and select the label. Now the area of ​​the pop-up window is directly limited to the entire software.[![](https://github.com/BioMeasure/labelimgup/raw/master/demo/label_edit_area.gif)
](https://github.com/BioMeasure/labelimgup/blob/master/demo/label_edit_area.gif)

对于原来的弹窗，必须按下其中的按钮才可以关闭，弹窗打开时，点击其它区域都无响应。现在点击弹窗外的其他区域会自动关闭弹窗，并且不会进行修改label的操作。  
For the original pop-up window, you must press the button in it to close it. When the pop-up window is open, clicking other areas will not respond. Now clicking on other areas outside the pop-up window will automatically close the pop-up window, and the operation of modifying the label will not be performed.[![](https://github.com/BioMeasure/labelimgup/raw/master/demo/label_edit_auto_close.gif)
](https://github.com/BioMeasure/labelimgup/blob/master/demo/label_edit_auto_close.gif)

快捷键改变 shortcut key change
------------------------

*   X：删除当前选中的目标框 X: Delete the currently selected target box

删除的功能 Removed features
---------------------

*   删除了右键菜单功能，因为可能与第二章的右键拖拽功能冲突导致BUG，同时其中的功能都已经设置了快捷键进行实现，见上文。原始的右键菜单如图：  
    Deleted the right-click menu function, because it may conflict with the right-click drag function in Chapter 2 and cause BUG, ​​and the functions in it have been set up with shortcut keys for implementation, see above. The original right-click menu is shown in the figure:[![](https://github.com/BioMeasure/labelimgup/raw/master/demo/menu_original.png)
    ](https://github.com/BioMeasure/labelimgup/blob/master/demo/menu_original.png)
