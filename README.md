# author:梁彦
## 3
全场定位的原理大概是：

1.每隔一个tick获取sampleTime

2.读取陀螺仪的数据，确定目机器的朝向

3.读取马达的数据，确定左右轮走过的角度，确定滤波前行走的速度（默认轮子旋转在1个tick的时间内不超过一圈）

4.通过前向差分法与速度的滤波确定左右轮预估的速度

5.通过正交分解确定自身坐标系上X轴与Y轴的速度

6.通过2中陀螺仪获取的数据跟5中自身坐标系上的速度的整合得到世界坐标系上（初始设定的X与Y轴）上X轴与Y轴机器的速度

7.通过1中获取的sample time(ms)与6中的速度根据之前的坐标迭代更新当前在世界坐标系中机器的X轴与Y轴的坐标

8.输出X轴与Y轴坐标及实时速度

## 5
修改的步骤如下：

1.在robot-config.cpp/.h中创建一个新的电机motor_extra

2.仿照```intakerControl()```与```baseStopControl()```函数在usercontrol.cpp中创建```motorControl()```函数

3.模仿```moveIntaker()```函数在basic-functions.h/cpp中创建```moveMotor()```函数