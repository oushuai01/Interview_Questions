# Interview_Questions

***********************************************************
`C++ 板块`
------- 
题目（1）：`C++用户空间内存分区有哪些？作用是什么？`

- **代码区**：存放程序代码，不允许修改，编译后的二进制文件存放在这里。
- **静态数据区**: 在编译器进行编译的时候就为该变量分配的内存,即全局变量和静态变量(用static声明的变量），存放在这个区的数据程序全部执行结束后系统自动释放，声明周期贯穿于整个程序执行过程。全局变量和静态变量的存储是放在一块的，初始化的全局变量和静态变量在一块区域(.data)，未初始化的全局变量和未初始化的静态变量在相邻的另一块区域(.bss)。
- **堆区**：这部分存储空间完全由程序员自己负责管理，它的分配和释放都由程序员自己负责。这个区是唯一一个可以由程序员自己决定变量生存 期的区间。可以用malloc,new申请对内存，并通过free和delete释放空间。如果程序员自己在堆区申请了空间，又忘记将这片内存释放掉，就会造成内存泄露的问题，导致后面一直无法访问这片存储区域。但程序退出后，系统自动回收资源。
- **栈区**：存放函数的形式参数和局部变量，由编译器分配和自动释放，函数执行完后，局部变量和形参占用的空间会自动被释放。效率比较高，但是分配的容量很有限。
- **常量区**：存放常量的区间，如字符串常量等，注意在常量区存放的数据一旦经初始化后就不能被修改。 程序结束后由系统释放。 

题目（2）：`C++ static关键字有哪些作用？`

- **全局静态变量**：位于静态存储区，程序运行期间一直存在，对外部文件不可见。（表明一个全局变量只对定义在同一文件中的函数可见。）

- **局部静态变量**：位于静态存储区，在局部作用域可以访问，离开局部作用域之后static变量仍存在，但无法访问。（表明该变量的值不会因为函数终止而丢失。）

- **静态函数**：即在函数定义前加static，函数默认情况下为extern，即可导出的。加了static就不能为外部类访问。注意不要在头文件声明static函数，因为static只对本文件有效。（表明该函数只在同一文件中调用。）

- **类的静态成员**：可以实现多个不同的类实例之间的数据共享，且不破坏隐藏规则，不需要类名就可以访问。类的静态存储变量是可以修改的。可以通过<对象名>::<静态成员>进行访问。（表明对该类所有对象这个数据成员都只有一个实例。即该实例归所有对象共有。）

- **类的静态函数**：不能调用非静态成员，只可以通过对象名调用<对象名>::<静态成员函数>（意味着一个静态成员函数只能访问它的参数、类的静态数据成员和全局变量）

题目（3）：`指针常量和常量指针的区别？`

- **指针常量**：是指定义了一个指针，这个指针只能定义时初始化，其他地方不能改变。

- **常量指针**：是指定义了一个指针，这个指针指向一个只读对象的值。

            指针常量强调的是指针的不可改变性，而常量指针强调的是指针对其所指对象的不可改变性。
            无论是指针常量还是常量指针，其最大的用途就是作为函数的形式参数，保证实参在被调用函数中不可改变特性。

题目（4）：`动态库和静态库的区别？`

            静态库和动态库最本质的区别是：该库是否被编译进目标程序内部。
- **静态库**：一般扩展名为（.a或.lib），这类库在编译的时候会直接整合到目标程序中，所以利用静态函数库编译的文件会比较大，这类函数库最大的优点就是编译成功的可执行文件可以独立运行，不再需要向外部函数要求读取函数库的内容，但是从升级难易程度来看，明显没有优势，如果函数库更新，需要重新编译。
- **动态库**：一般扩展名为（.so或.dll），与静态函数库被整个捕捉到程序中不同，动态函数库在编译的时候，在程序里只有一个指向的位置而已，也就是当可执行文件需要使用到函数库机制的时候，程序才会读取函数库使用，也就是说可执行文件无法单独运行。这样从产品升级角度方便升级，只要替换对应动态库即可，不必重新编译整个可执行文件。
- **总结**：从产品化的角度，发布的算法库或功能库尽量使用动态库，这样方便更新和升级，不必重新编译整个可执行文件，只需要新版本动态库替换掉旧的动态库即可。从函数库集成的角度，若要将发布的所有子库集成为一个动态库向外提供接口，那么就需要将所有子库编译成一个静态库，这样所有子库就可以全部编译进动态库中，由最终的一个集成库向外提供功能。

题目（5） ：`Struct 和 Class 的区别？`

- struct 是值类型，class 是对象类型。
- struct 不能被继承，class 可以被继承。
- struct 默认的访问权限是public,而class 默认的访问权限是private。
- struct的new和class的new是不同的。struct的new就是执行一下构造函数创建一个新实例再对所有的字段进行Copy。而class则是在堆上分配一块内存然后再执行构造函数，struct的内存并不是在new的时候分配的，而是在定义的时候分配

题目（6） ：`vertor 和 deque 的区别？`

- deque 两端都能快速安插和删除元素。
- 元素的存取和迭代器的动作比vector稍慢。
- 迭代器需要在不同区块间跳转，所以它非一般指针。
- 因为deque使用不止一块内存（而vector必须使用一块连续内存），所以deque的max_size()可能更大。
- deque的内存区块不再被使用时，会自动被释放。deque的内存大小是可自动缩减的。

题目（7）：`queue 和 stack 的异同？`

- 都是线性结构。
- 插入操作都是限定在表尾进行。
- 都可以通过顺序结构和链式结构实现。
- 删除数据元素的位置不同，栈的删除操作在表尾进行，队列的删除操作在表头进行。

题目（8）：`list 的优缺点`

***优点***：

- 采用动态存储分配，不会造成内存浪费和溢出。
- 链表执行插入和删除操作十分方便，修改指针即可，不需要移动大量元素。

***缺点***：

- 链表灵活，但是空间(指针域) 和 时间（遍历）额外耗费较大。


题目（9）：`指针与引用有什么区别？`

- 指针会占用内存，引用不占用内存。

- 引用在定义时必须初始化。

- 没有空的引用，但是有空的指针。

题目（10）：`数组与链表的区别是什么？`

- 数组在内存中是连续的，链表在内存中是不连续的，靠指针连接。

- 数组占用的总内存相对链表要小，因为链表除了要保存数据外，还要保存用于连接的指针。

- 数组方便排序和查找，但不方便删除和插入；而链表则方便删除和插入，不方便排序和查找。

**题目（11）：`头文件中的ifndef/define/endif有什么作用？`**

这是C++预编译头文件保护符，保证即使文件被多次包含，头文件也只定义一次。

**题目（12）：`请描述进程和线程的区别`**

（1）进程是程序的一次执行，线程是进程中的执行单元；

（2）进程间是独立的，这表现在内存空间、上下文环境上，线程运行在进程中；

（3）一般来讲，进程无法突破进程边界存取其他进程内的存储空间；而同一进程所产生的线程共享内存空间；

（4）同一进程中的两段代码不能同时执行，除非引入多线程。

**********************************************************
`SLAM板块`
------- 
题目（1）：`视觉和IMU融合有哪些优势？`

IMU可以对短时间内的快速运动可以做出较好的估计，但是存在零偏问题，导致长时间的积分会产生飘逸甚至发散。视觉slam直接测量旋转与平移，不会产生飘逸，但是在相机快速运动时特征点容易丢失，无法进行匹配，同时容易受图像遮挡、动态障碍物无法判断等问题。IMU和视觉两者的优劣势互补，可以有效解决各自存在的问题。

题目（2）：`slam中为什么要引入李群李代数？`

在进行最小二乘的优化问题时，对于复杂的函数，通常采用迭代的方法，需要对函数进行求导进而得到一个增量，不断更新当前的优化变量。 问题在于，旋转矩阵更新的方式是不断左乘新的旋转变量而不是加，即SO(3)上没有加法，它的导数无法按照导数的定义进行计算。因此，我们可以将其映射为李代数，化乘为加，通过李代数求得增量，再通过指数映射将其映射回SO(3)进行当前估计值的更新。                                                                                            




**********************************************************
`路径规划板块`
------- 

题目（1）：`路径规划与轨迹生成常用的方法有哪些？`

基于搜索的路径规划有两项，分别是Dijkstra和A*算法；
基于采样的路径规划有三项，分别是RRT、RRT*和Informed RRT*算法；
基于智能算法的路径规划两项，分别是遗传算法和蚁群算法。

轨迹生成常用的有两种方法，分别是多项式曲线和贝塞尔曲线；
轨迹优化目标有两种方法，分别是最小化snap和轨迹长度；
轨迹约束有两种方法，分别是软约束和硬约束。

题目（2）：`路径规划中常用的地图种类有哪些？`

Occupancy grid map（栅格地图），包括了二维栅格地图与三维珊格地图，会消耗大量的时间去寻找路径，不适合作为全局的地图格式来存储；
Octo-map（八叉数地图），可以看作是栅格地图的改进后的地图，以正方体举例子，先分为8份，对于有障碍物的再分，没有障碍物的大栅格就不再区分；
Point cloud map（点云地图），可以尽可能地保留原始环境信息，有益于三维重建，但需要在环境模型中存储大量无序的三维数据点；
ESDF（可以看作珊格地图优化版本），显示障碍物的位置，并带有距离、方向信息，有利于后期做局部路径规划算法。

题目（3）：`软约束与硬约束分别是什么？`

通常轨迹优化问题通常会有目标函数，然后我们会为决策变量设置一些约束条件，这些约束条件缩小了可行域的范围，约束条件会存在以下几种可能性：约束合适，简化了目标函数的求解，去掉了鞍点留下来最值点（正常约束）；约束过多，发现不可能满足所有的约束条件，可行域为空集（过约束）；约束不足，发现可行域太大，搜索算法很费时（欠约束）。

硬约束即是给地图划分出绝对安全的空间，并在空间交界处放置必经点，将路径约束在安全空间内。

软约束则是通过构建惩罚函数，利用类似于场的原理使得障碍物原理，在任何一点处的位置都由周围环境的惩罚函数决定，生成局部路径比较快。

题目（4）：`已经有了后端的轨迹优化为什么还要有符合动力学的路径规划算法？`

传统的路径规划算法被明显地分为前端路径点生成和后端轨迹优化两部分，传统的路径点生成方法生成的路径在具有比较多动力学模型约束的时候可能无法生成符合动力学的轨迹，导致花费大量的资源重新进行搜索。前期考虑了动力学模型后就只需要在原有的轨迹上进行优化（可以通过OPVB或者minimum-snap/minimum-jerk）就可以得到一条可以运行的轨迹。

符合动力学模型的路径生成方法可分为两类，离散状态量与离散控制量，离散控制量是从根部出发衍生，而离散状态量则是每一个点画出轨迹后连接。

题目（5）：`凸优化问题的优势？`

凸优化问题的局部最优解就是全局最优解

很多非凸问题都可以被等价转化为凸优化问题或者被近似为凸优化问题

凸优化问题的研究较为成熟，当一个具体被归为一个凸优化问题，基本可以确定该问题是可被求解的

题目（6）：`轨迹优化中为什么是minimum snap， minimum jerk或其它？？`

nap是位置的四阶导数。由于四旋翼的微分平坦特性，snap对应的是角加速度，也就是力矩层面。力矩层面又和电机转速是直接相关的，因此最小化这个指标可以获得理论上最节省能量的轨迹。
（对一些存在平坦输出的非线性系统，如果可以找到一组系统输出，使得所有状态变量和输入变量都可以由这组输出及其有限阶微分进行表示，那么该系统即为微分平坦系统）

当然也可以优化不同阶数的导数，minimum jerk就对应角速度，也可以优化加速度，甚至是速度，只是在不同意义下得到的最优。
上面说的对应可以理解为，假如我们完全开环控制四旋翼无人机。也就说根据设计的的轨迹，直接设计力矩（或者是电机转速指令，这个是通过常数矩阵映射的）发送给无人机，让他跟踪上轨迹。那么就对应需要轨迹四阶导数的信息（也可以说这是微分平坦理论告诉我们的）。

**********************************************************
`控制板块`
------- 
题目（1）：`MPC与LQR的区别有哪些？`

- 1) 控制对象：mpc可对线性和非线性进行控制        LQR只对线性系统

- 2) 求解目标函数方法。MPC：一般转化为二次规划问题，利用求解器进行求解，生成控制序列 。LQR：一般采用变分法，通过求解黎卡提方程进行逼近，最终获取控制序列。

- 3) 工作时域。两者的工作时域不同，mpc在有限控制时域求解，LQR在无限时域里求解。MPC：是求解预测时间段Np内的控制序列 ，并在下个周期后进行滚动优化，每次只需控制序列的第一个值作为控制的输入。为了提高速度，可只计算控制时间段Nc 内的控制序列，时间段（Np-Nc）内的控制量均取Nc-1处的值即可。LQR：求解预测时间段内的控制序列，只求解一次，每个周期下取对应的控制量即可，而不考虑之前周期下实际与规划的误差。

- 4) LQR不滚动优化，预测时间段内的控制序列只求解一次，没有考虑实际与规划的误差。

- 5) 有无约束。mpc可以很好的处理约束问题；LQR要求无约束，假设对控制量无约束。

题目（2）：`MPC与PID的区别有？`

- mpc是基于模型进行预测控制的，依赖模型；而pid是基于反馈的，不需要模型。

- pid不适用于非线性系统；mpc适用与非线性系统。

题目（3）：`在mpc算法中，获得的最优控制序列一定可以使系统稳定吗？`

- 不一定。直观理解：该算法是在有限时域内作优化求解控制序列，在有限时域里的优化只反映局部信息，而不是整个时域里的最优解，没有反映系统的真正性能。要使系统稳定，则需在目标函数里对终端误差控制矩阵进行设计。换句话说，也就是将作优化的时域设置成无限时域。

题目（4）：`带约束线性mpc保证稳定性的方式主要有哪几种？`

- 主要有四种，终端等式约束，无穷时域，终端不等式约束，终端代价。其中终端等式约束可以选取，x(N|k)=0。



