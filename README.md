# MOT-fasterRCNN-sort
使用gluoncv预训练模型实现多目标检测，使用sort算法实现多目标追踪
## 1.代码原理
	该程序逐个读取帧图片，并对帧图片逐个进行多行人检测、多目标追踪。该方法是在线方法，将逐个读取帧图片改为逐帧读取视频即可实现在线处理视频。
	1.1 多行人检测。
		使用gluoncv中的预训练模型faster_rcnn_fpn_bn_resnet50_v1b_coco实现多行人检测，这一步骤见detect.py。
	1.2 多目标追踪。
		使用sort算法实现多目标追踪，详见https://github.com/abewley/sort。
## 2.代码部署
	2.1 配置环境。
		安装python==3.6，安装requirements.txt中要求的库（代码运行实际用到的库可能少于该文件，因此建议根据代码安装所需要的库）。
	2.2 准备数据。
		有两种方法准备数据：
		2.2.1 将A-data文件夹放入当前目录，A-data文件夹中为Track1 Track2等子文件夹，每个子文件夹中存有.jpg帧图片。
		2.2.2 修改run.py的第97行，将input_folder改为A-data文件夹所在路径。
	2.3 运行程序run.py。
	2.4 程序输出。
		程序运行时会打印处理进度及估计的剩余时间。
		程序运行完成后，会在当前目录下生成output文件夹，文件夹中存有Track1 Track2等数据集对应的检测结果，.avi文件用于观察检测追踪效果，.txt文件是用于提交的文本文件。
## 3.调参
	3.1 多目标检测模型的选择。
		修改detect.py第10行(YOLO.__init__)即可，可选模型及其名称、效果详见gluoncv官网
	3.2 sort算法参数的修改。
		run.py第34行，参数含义见sort.py。
	3.3 将sort改为deepsort。
		详见https://github.com/nwojke/deep_sort。
		TODO：经尝试，经deep_sort处理后的检测框位置有变形、偏移现象，待解决。
	3.4 输入输出路径见run.__main__
	
