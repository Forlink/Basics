##数据结构
###线性表
***
<p>线性表（List）:零个或多个数据元素的有限序列</p>
<p>
<p>ADT线性表(List)</p>
<p>
Data
	<p>
	线性表的数据对象集合为{a1,a2……an},每个元素的类型均为DataType.其中，除第一个元素a1外，每一个元素有且只有一个直接前驱元素，除了最后一个元素an外，每一个元素有且只有一个直接后既元素。数据元素之间的关系是一对一的关系。
	</p>
	<p>
	Operation
	<p>IniList(*L);			初始化操作，建立一个空的线性表L.</p>
	<p>ListEmpty(L);		若线性表为空，返回true,否则返回false</p>
	<p>ClearList(*L);		将线性表清空</p>
	<p>GetElem(L,i,*e);		将线性表L中的第i个位置元素值返回给e</p>
	<p>LocateElem(L,e); 	将线性表L中查找与给定值e相等的元素，如果查找成功，返回该元素在表中序号表示成功；否则，返回0表示失败。</p>
	<p>ListInsert(*L,i,e);  在线性表L中的第i个位置插入新元素e</p>
	<p>ListDelete(*L,i,e);  删除线性表L中第i个位置元素，并用e返回其值</p>
	<p>ListLength(L);	    返回线性表L的元素个数</p>
	endADT
	</p>
</p>
</p>
####线性表的顺序存储结构
#####顺序存储定义
<p>
线性表的顺序存储结构，指得是用一段地址连续的存储单元依次存储线性表的数据元素。
</p>
#####顺序存储方式
	#define MAXSIZE 20 					/*存储空间初始分配量*/
	typedef int ElemType;				/*ElenType类型根据实际情况而定，这里假设为int*/
	typedef struct
	{
		ElemType data[MAXSIZE];			/*数组存储数据元素，最大值为MAXSIZE*/
		int length;						/*线性表当前长度*/
	}SqList;
<p>
顺序存储结构需要三个属性：
<ul>
<li>存储空间的起始位置：数组data,它的存储位置就是存储空间的存储位置</li>
<li>线性表的最大存储容量：数组长度MaxSize</li>
<li>线性表的当前长度：length</li>
</ul>
</p>
#####数据长度与线性表长度区别
<p>线性表的长度是线性表中数据元素的个数，随着线性表插入和删除操作的进行，这个量是变化的</p>
<p>在任意时刻，线性表的长度应该小于等于数组的长度</p>
#####地址计算方法
<p>用数组存储顺序意味着要分配固定长度的数组空间，由于线性表可以进行插入和删除操作，因此分配的数组空间要大于等于当前线性表的长度</p>
<p>存储器中的每个存储单元都有自己的编号，这个编号称为地址</p>
#####插入算法的思路
<ul>
<li>如果插入位置不合理，抛出异常</li>
<li>如果线性表长度大于等于数组长度，则抛出异常或动态增加常量</li>
<li>从最后一个元素开始向前遍历到第i个位置，分别将它们都向后移动一个位置</li>
<li>将要插入元素填入位置i处</li>
<li>表长加1</li>
</ul>
#####删除算法的思路
<ul>
<li>如果删除位置不合理，抛出异常</li>
<li>取出删除元素</li>
<li>从删除元素位置开始遍历到最后一个元素位置，分别将它们都向前移动一个位置</li>
<li>表长减1</li>
</ul>
#####线性表顺序存储结构的优缺点
<p>
优点：
<p>无须为表示表中元素之间的逻辑关系而增加额外的存储空间</p>
<p>可以快速地存取表中任一位置的元素</p>
</p>
<p>
缺点：
<p>插入和删除操作需要移动大量元素</p>
<p>当线性表长度变化较大时，难以确定存储空间的容量</p>
<p>造成存储空间的“碎片”</p>
</p>
####线性表的链示存储结构
#####顺序存储结构不足的解决办法
<p>
所有的元素都不考虑相邻位置，哪有空位就到哪里，而只是让每个元素知道它下一个元素的位置在哪里，这样，我们可以在第一个元素时，就知道第二个元素的位置（内存地址），而找的它；在第二个元素时，再找到第三元素的位置（内存地址）。这样所有的元素就能通过遍历而找到。
</p>
#####线性表链示存储结构定义
<p>
线性表的链示存储结构的特点是用一组任意的存储单元存储线性表的数据元素，这组存储单元可以是连续的，也可以是不连续的。这就意味着，这些数据元素可以存在内存未被占用的任意位置。
</p>
<p>
	<p>
	为了表示每个数据元素ai与其直接后继数据元素ai+1之间的逻辑关系，对数据元素ai来说，除了存储其本身的信息之外，还需存储一个指示其直接后继的信息（即直接后继的存储位置）。我们把存储数据元素信息的域称为数据域，把存储直接后继位置的域称为指针域。指针域中存储的信息称作指针或链。这两部分信息组成数据元素ai的存储映像，称为节点（Node）。
	</p>
	<p>
	n个结点（ai的存储映像）链结成一个链表，即为线性表(a1,a2……,an)的链式存储结构，因为此链表的每个结点中只包含一个指针域，所以叫做单链表。
	</p>
	<p>
	链表中第一个结点的存储位置叫做头指针。
	</p>
	<p>
	单链表的第一个结点前附设一个结点，称为头结点。
	</p>
</p>
#####头指针与头结点的异同
<p>
头指针
	<p>头指针是指链表指向第一个结点的指针，若链表有头结点，则是指向头结点的指针。</p>
	<p>头指针具有标识作用，所以常用头指针冠以链表的名字</p>
	<p>无论链表是否为空，头指针均不为空。头指针是链表的必要元素</p>
</p>
<p>
头结点
	<p>头结点是为了操作的统一和方便而设立的，放在第一元素的结点之前，其数据域一般无意义（也可存放链表的长度）</p>
	<p>有了头结点，对在第一元素结点前插入结点和删除第一结点，其操作与其它结点的操作就统一了</p>
	<p>头结点不一定是链表必须要素</p>
</p>
#####线性表链式存储结构代码描述
	/*线性表的单链表存储结构*/
	typedef struct Node
	{
		ElemType data;
		struct Node *next;
	}Node;
	typedef struct Node *LinkList;	/*定义 LinkList*/
<p>结点由存放数据元素的数据域存放后继结点地址的指针域组成</p>
#####单链表的整表创建
<p>
单链表整表创建的算法思路：
<p>1.声明一结点P和计数器变量i</p>
<p>2.初始化一空链表L</p>
<p>3.让L的头结点的指针指向NULL，即建立一个带头结点的单链表；</p>
<p>
4.循环：
<ul>
<li>生成一新结点赋值给P</li>
<li>随机生成一数字赋值给P的数据域p->data</li>
<li>将P插入到头结点与前一新结点之间</li>
</ul>
</p>
</p>
#####单链表的整表删除
<p>
单链表整表删除的算法思路：
<p>1.声明一结点P和计q</p>
<p>2.将第一个结点赋值给P</p>
</p>
<p>
3.循环：
<ul>
<li>将下一结点赋值给q</li>
<li>释放p</li>
<li>将q赋值给p</li>
</ul>
</p>
</p>
#####单链表结构与顺序存储结构优缺点
<ul>
存储分配方式
<li>顺序存储结构用一段连续的存储单元依次存储线性表的数据元素</li>
<li>单链表采用链式存储结构，用一组任意的存储单元存放线性表的元素</li>
</ul>
<ul>
时间性能
<ul>
查找
<li>顺序存储结构0(1)</li>
<li>单链表0(n)</li>
</ul>
<ul>
插入和删除
<li>顺序存储结构需要平均移动表长一半的元素，时间为0(n)</li>
<li>单链表在线出某位置的指针后，插入和删除时间仅为0(1)</li>
</ul>
</ul>
<ul>
空间性能
<li>顺序存储结构需要预分配存储空间，分大了，浪费，分小了易发生上溢</li>
<li>单链表不需要分配存储空间，只要有就可以分配，元素个数也不受限制</li>
</ul>
####静态链表优缺点
<p>
优点：
	<p>
	在插入和删除操作时，只需要修改游标，不需要移动元素，从而改进了在顺序存储结构中的插入和删除操作需要移动大量元素的缺点。
	</p>
</p>
<p>
缺点：
	<p>
	没有解决连续存储分配带来的表长难以确定的问题
	</p>
	<p>
	失去了顺序存储结构随机存取的特性
	</p>
</p>
####循环链表
<p>
将单链表中终端结点的指针端由空指针改为指向头结点，就使整个单链表形成一个环，这种头尾相接的单链表称为单循环链表，简称循环链表。
</p>
####双向链表
<p>
双向链表是在单链表的每个结点中，再设置一个指向其前驱结点的指针域。
</p>
###栈与队列
***
####栈的定义
<p>
栈(stack)是限定仅在表尾进行插入和删除操作的线性表。
</p>
<p>
我们把允许插入和删除的一端称为栈顶(top)，另一端称为栈底(bottom)，不含任何数据元素的栈称为空栈。栈又称为后进先出的线性表，简称LIFO结构。
</p>
<p>
理解栈的定义需要注意：
	<p>
	首先它是一个线性表，也就是说，栈元素具有线性关系，即前驱后继关系。只不过它是一种特殊的线性表而已。定义中说是在线性的表尾进行插入和删除操作，这里表尾是指栈顶，而不是栈底。
	</p>
	<p>
	它的特殊之处就在于限制了这个线性表的插入和删除位置，它始终只在栈顶进行。这也就使得：栈底是固定的，最先进栈的只能在栈底。
	</p>
	<p>
	栈的插入操作，叫作进栈，也称压栈、入栈。
	</p>
	<p>
	栈的删除操作，叫作出栈，也有的叫作弹栈。
	</p>
</p>
####队列的定义
<p>
队列(queue)是只允许在一端进行插入操作，而在另一端进行删除操作的线性表。
</p>
<p>
队列是一种先进先出(First In First Out)的线性表，简称FIFO。允许插入的一端称为对尾，允许删除的一端称为队头。
</p>
####总结回顾
<p>
对于栈来说，如果是两个相同数据类型的栈，则可以用数组的两端作栈底的方法来让两个栈共享数据，这就可以最大化地利用数组的空间。
</p>
<p>
对于队列来说，为了避免数组插入和删除时需要移动数据，于是就引入了循环队列，使得队头和队尾可以在数组中循环变化。解决了移动数据的时间损耗，使得本来插入和删除时0(n)的时间复杂变成了0(1)。
</p>
###串
***
<p>
串（string）是由零个或多个字符组成的有限序列，又名叫字符串。
</p>
####串的存储结构
<p>
	串的顺序存储结构是用一组地址连续的存储单元来存储串中的字符序列的。按照预定义的大小，为每个定义的串变量分配一个固定长度的存储区。一般是用定长数组来定义。
</p>
#####串的链式存储结构
<p>
对于串的链式存储结构，与线性表的相似的，但由于串结构的特殊性，结构中的每个元素数据是一个字符，如果也简单的应用链表存储串值，一个结点对应一个字符，就会存在很大的空间浪费。因此，一个结点可以存放一个字符，也可以考虑存放多个字符，最后一个结点若是未被占满时，可以用“#”或其他非串值字符补全。
</p>
####朴素的模式匹配算法
<p>
子串的定位操作通常称作串的模式匹配
</p>
	/*返回子串T在主串第pos个字符之后的位置。若不存在，则函数返回值为0*/
	/*T非空，1≤pos≤StrLength(s)*/
	int Index(String S, String T, int pos)
	{
		int i = pos;		/*i用于主串S中当前位置下标，若pos不为1*/
							/*则从pos位置开始匹配*/
		int j = 1;			/*j用于子串T中当前位置下标值*/
		while (i <= S[0] && j <= T[0])		/*若i小于S长度且j小于T的长度时循环*/
		{
			if (S[i] == T[j])	/*两字母相等则继续*/
			{
				++i;
				++j;
			}else{				/*指针后退重新开始匹配*/
				i = i-j+2;		/*i 退回到上次匹配首位的下一位*/
				j = 1;			/*j退回到子串T的首位*/
			}
		}
		if (j > T[0])
			return i-T[0];
		else
			return 0;
	}
####KMP模式匹配算法实现
	/* 通过计算返回子串T的next数值*/
	void get_next (String T, int *next)
	{
		int i,j;
		i=1;
		j=0;
		next[1]=0;
		while (i<T[0])		/* 此处T[0]表示串T的长度*/
		{
			if (j==0 || T[i]==T[j])		/* T[i]表示后缀的单个字符*/
										/* T[j]表示前缀的单个字符*/
			{
				++i;
				++j;
				next[i] = j;
			}else{
				j = next[j];			/*若字符不相同，则j值回溯*/
			}
		}
	}
###树
***
<p>
树(Tree)是n(n≥0)个结点的有限集。n=0时称为空树。在任意一颗非空树中：（1）有且仅有一个特定的称为根（Root）的结点；（2）当n>1时，其余结点可分为m(m>0)个互不相交的有限集T1、T2、……、Tm,其中每一个集合本身又是一棵树，并且称为根的子树(SubTree)。
</p>
<p>
对于树的定义还需要强调两点：
	<p>
	1、n>0时根节点是唯一的，不可能存在多个结点，别和现实中的大树混在一起，现实中的树有很多根须，那是真是的树，数据结构中的树只能有一个根结点。
	</p>
	<p>
	2、m>0时，子树的个数没有限制，但它们一定是互不相交的。
	</p>
</p>
#####结点分类
<p>
	结点拥有的子树称为结点的度(Degree)。度为0的结点称为叶结点(Leaf)或终端结点；度不为0的结点称为非终端结点或分支结点。除根结点之外，分支结点之外，分支结点也称为内部结点。树的度是树内各结点的度的最大值。
</p>
#####结点间关系
<p>
	结点的子树的根称为该结点的孩子(Child)，相应地，该结点称为孩子的双亲。
</p>
<p>
	同一个双亲的孩子之间互称兄弟(Sibling)。结点的祖先是从根到该结点所经分支上的所有结点。
</p>
#####树的其他相关概念
<p>
	结点的层次(Level)从根开始定义起，根为第一层，根的孩子为第二层。若某结点在第1层，则其子树的根就在第l+1层。其双亲在同一层的结点互为堂兄弟。树中结点的最大层次称为树的深度(Depth)或高度。
</p>
<p>
	如果将树中结点的各子树看成从左至右是有次序的，不能互换的，则称该树为有序树，否则称为无序树。
</p>
<p>
线性结构
	<p>
	第一个数据元素：无前驱
	</p>
	<p>
	最后一个数据元素：无后继
	</p>
	<p>
	中间元素：一个前驱一个后继
	</p>
</p>
<p>
树结构
	<p>
	根结点：无双亲，唯一
	</p>
	<p>
	叶结点：无孩子，可以多个
	</p>
	<p>
	中间结点：一个双亲多个孩子
	</p>
</p>
####树的存储结构
***
#####双亲表示法
<p>
在每个结点中，附设一个指示器指示其双亲结点到链表中的位置。
</p>
	/* 树的双亲表示法结点结构定义 */
	#define MAX_TREE_SIZE 100
	typedef int TElemType;	/*树结点的数据类型，目前暂定为整型*/
	typedef struct PTNode	/*结点结构*/
	{
		TElemType data;		/*结点数据*/
		int parent;			/*双亲位置*/
	} PTNode;
	
	typedef struct			/*树结构*/
	{
		PTNode nodes[MAX_TREE_SIZE];	/*结点数组*/
		int r,n;			/*根的位置和结点数*/
	} PTree;
#####孩子表示法
<p>
由于树中每个结点可能有多棵子树，可以考虑用多重链表，即每个结点有多个指针域，其中每个指针指向一颗子树的根结点，我们把这种方法叫做多重链表表示法。
</p>
<p>
孩子表示法：把每个结点的孩子结点排列起来，以单链表作存储结构，则n个结点有n个孩子链表，如果是叶子结点则此单链表为空。然后n个头指针又组成一个线性表，采用顺序存储结构，存放进一个一维数组中。
</p>
	/* 树的孩子表示法结构定义 */
	#define MAX_TREE_SIZE 100
	typedef struct CTNode	/*孩子结点*/
	{
		int child;
		struct CTNode *next;
	} *ChildPtr;
	typedef struct	/*表头结构*/
	{
		TElemType data;
		ChildPtr firstchild;
	} CTBox;
	typedef struct 	/*树结构*/
	{
		CTBox nodes[MAX_TREE_SIZE];		/*结点数组*/
		int r,n;		/*根的位置和结点数*/
	} CTree;
#####孩子兄弟表示法
<p>
任意一棵树，它的结点的第一个孩子如果存在就是唯一的，它的右兄弟如果存在也是唯一的 。因此，我们设置两个指针，分别指向结点的第一个孩子和此结点的右兄弟。
</p>
	/* 树的孩子兄弟表示法结构定义 */
	typedef struct CSNode
	{
		TElemType data;
		struct CSNode *firstchild,*rightsib;
	} CSNode,*CSTree;
####二叉树的定义
***
<p>
二叉树(B树)是n(n≥0)个结点的有限集合，该集合或者为空集(称为空二叉树)，或者由一个根结点和两颗互不相交的、分别称为根结点的左树和右子树的二叉树组成。
</p>
#####二叉树特点
<p>
二叉树的特点有：
	<p>
		每个结点最多有两棵子树，所以二叉树中不存在度大于2的结点。注意不是只有两棵子树，而是最多有。没有字树或者有一棵子树都是可以的。
	</p>
	<p>
		左子树和右子树是有顺序的，次序不能任意颠倒。
	</p>
	<p>
		即使树中某结点只有一棵子树，也要区分它是左子树还是右子树。
	</p>
</p>
<p>
二叉树具有五种基本形态：
	<p>
	1、空二叉树。	
	</p>	
	<p>
	2、只有一个根结点
	</p>
	<p>
	3、根结点只有左子树
	</p>
	<p>
	4、根结点只有右子树
	</p>
	<p>
	5、根结点既有左子树又有右子树
	</p>
</p>
#####特殊二叉树
<p>
1、斜树
	<p>
	所有的结点都只有左子树的二叉树叫左斜树。所有结点都只有右子树的二叉树叫右斜树。这两者统称为斜树。	
	</p>	
</p>
<p>
2、满二叉树
	<p>
	在一棵二叉树，如果所有分支结点都存在左子树和右子树，并且所有叶子都在同一层上，这样的二叉树称为满二叉树。	
	</p>	
</p>
<p>
3、完全二叉树
	<p>
	对一棵具有n个结点的二叉树按层序编号，如果编号为i (1≤i≤n)的结点与同样深度的满二叉树中编号为i的结点在二叉树中位置完全相同，则这棵二叉树称为完全二叉树。
	</p>
完全二叉树的特点：
	<p>
	1、叶子结点只能出现在最下两层。
	</p>
	<p>
	2、最下层的叶子一定集中在左部连续位置。
	</p>
	<p>
	3、倒数二层，若有叶子结点，一定都在右部连续位置。
	</p>
	<p>
	4、如果结点度为1，则该结点只有左孩子，即不存在只有右子树的情况。
	</p>
	<p>
	5、同样结点数的二叉树，完全二叉树的深度最小。
	</p>
</p>
####遍历二叉树
<p>
	二叉树的遍历是指从根结点出发，按照某种次序依次访问二叉树中所有结点，使得每个结点被访问一次且仅被访问一次。	
</p>
###图
***
####图的定义
<p>
	图是由顶点的有穷非穷空集合和顶点之间的集合组成，通常表示为：G(V,E),其中，G表示一个图，V是图G中顶点的集合，E是图G中边的集合。
</p>
<p>
矩阵啥的都忘干净啦。算了，放弃治疗啦。图略过了。	
</p>
###查找
***
<p>
查找就是根据给定的某个值，在查找表中确定一个其关键字等于给定值得数据元素(或记录)。
</p>
<p>
顺序表查找优化算法：	
</p>
	/*顺序查找，a为数组，n为要查找的数组个数，key为要查找的关键字 有哨兵顺序查找*/
	int Sequential_Search(int *a, int n, int key)
	{
		int i;
		a[0] = key;		/*设置a[0]为关键字值，我们称之为“哨兵”*/
		i=n;			/*循环从数组尾部开始*/
		while(a[i]!=key)
		{
			i--;
		}
		return 1;		/*返回0则说明查找失败*/
	}
<p>
二分查找（折半查找）：	
</p>
	int Binary_Search(int *a, int n, int key)
	{
		int low,high,mid;
		low=1;		/*定义最低标为记录首位*/
		high=n;		/*定义最高下标为记录末尾*/
		while(low<=high)
		{
			mid = (low+high)/2;			/*折半*/
			if (key<a[mid])				/*若查找值比中值小*/
				high=mid-1;				/*最高下标调整到中位下标小一位*/
			else if (key>a[mid])		/*若查找值比中值大*/
				low=mid+1;				/*最低下标调整到中位下标大一位*/
			else
				return mid;				/*若相等则说明mid即为查找到位置*/
		}
		return 0;
	}
<p>
斐波那契查找：
</p>
	int Fibonacci_Search(int *a, int n, int key)
	{
		int low,high,mid,i,k;
		low=1;							/*定义最低下标为记录首位*/
		high=n;							/*定义最高下标为记录末位*/
		k=0;
		while (n>F[k]-1)				/*计算n位于斐波那契数列的位置*/
			k++;
		for (i=n;i<F[k]-1;i++)			/*将不满的数值补全*/
			a[i]=a[n];
		
		while (low<=high)
		{
			mid=low+F[k-1]-1;			/*计算当前分隔的下标*/
			if (key<a[mid])				/*若查找记录小于当前分隔记录*/
			{
				high=mid-1;				/*最高下标调整到分隔下标mid-1处*/
				k=k-1;					/*斐波那契数列下标减一位*/
			}
			else if (key>a[mid])		/*若查找记录大于当前分隔记录*/
			{
				low=mid+1;				/*最低下标调整到分隔下标mid+1处*/
				k=k-2;					/*斐波那契数列下标减两位*/
			}
			else
			{
				if (mid<n)
					return mid;			/*若相等则说明mid即为查找到的位置*/
				else
					return n;			/*若mid>n说明是补全数值，返回n*/
			}
		}
		return 0；
	}
<p>
二叉排序树查找操作：
</p>
	/*递归查找二叉排序树T中是否存在key*/
	/*指针f指向T的双亲，其初始调用值为NULL*/
	/*若查找成功，则指针p指向该数据元素结点，并返回TRUE*/
	/*否则指针p指向查找路径上访问的最后一个结点并返回FALSE*/
	status SearchBST(BiTree T, int key, BiTree f, BiTree *p)
	{
		if (!T)						/*查找不成功*/
		{
			*p = f;
			return FALSE;	
		}
		else if (key==T->data)		/*查找成功*/
		{
			*p = T;
			return TRUE;	
		}
		else if (key<T->data)
		{
			return SearchBST(T->lchild, key, T, p);		/*在左子树继续查找*/
		}
		else
			return SearchBST(T->rchild, key, T, p);		/*在右子树继续查找*/
	}
<p>
	平衡二叉树，是一种二叉排序树，其中每一个节点的左子树和右子树的高度差至多等于1。
</p>
<p>
	将二叉树上结点的左子树深度减去右子树深度的值称为平衡因子BF，那么平衡二叉树上所有结点的平衡因子只可能是-1,0，1。只要二叉树上有一个结点的平衡因子的绝对值大于1，则该二叉树就是不平衡的。
</p>
<p>
	距离插入结点最近的，且平衡因子的绝对值大于1的结点为根的子树，我们称为最小不平衡子树。
</p>
<p>
	平衡二叉树构建的基本思想就是在构建二叉树排序树的过程中，每当插入一个结点时，先检查是否因插入而破坏了树的平衡性，若是，则找出最小不平衡树。在保持二叉排序树特性的前提下，调整最小不平衡子树中各结点之间的链接关系，进行相应的旋转，使之成为新的平衡子树。
</p>
<p>
平衡二叉树实现算法：
</p>
	/* 二叉树的二叉链表结点结构定义 */
	typedef struct BiTNode					/*结点结构*/
	{
		int data;							/*结点数据*/
		int bf;								/*结点的平衡因子*/
		struct BiTNode *lchild, *rchild;	/*左右孩子指针*/
	} BiTNode, *BiTree;

	/* 对以p为根的二叉树排序树作右旋处理 */
	/* 处理之后p指向新的树根结点，即旋转处理之前的左子树的根结点 */
	void R_Rotate(BiTree *p)
	{
		BiTree L;
		L=(*p)->lchild;				/*L指向p的左子树根结点*/
		(*p)->lchild=L->rchild;		/*L的右子树挂接为p的左子树*/
		L->rchild=(*p);			
		*p=L;						/*p指向新的根结点*/
	}
<p>
	此函数代码的意思是说，当传入一个二叉排序树P，将它的左孩子结点定义为L，将L的右子树变成P的左子树，再将P改为L的右子树，最后将L替换P成为根结点。这样就完成了一次右旋操作。
</p>
	/* 对以p为根的二叉排序树作左旋处理 */
	/* 处理之后P指向新的树根结点，即旋转处理之前的右子树的根结点0 */
	void L_Rotate(BiTree *p)
	{
		BiTree R;
		R=(*p)->rchild;				/*R指向p的右子树根结点*/、
		(*p)->rchild=R->lchild;		/*R的左子树挂接为p的右子树*/
		R->lchild=(*p);		
		*p=R;						/*p指向新的根结点*/
	}
<p>
	左平衡旋转处理的函数代码：
</p>
	#define LH +1	/*左高*/
	#define EH 0	/*等高*/
	#define	RH -1	/*右高*/
	/* 对以指针T所指结点为根的二叉树作左平衡旋转处理 */
	/* 本算法结束时，指针T指向新的根结点 */
	void LeftBalance(BiTree *T)
	{
		BiTree L,Lr;
		L=(*T)->lchild;				/*L指向T的左子树根结点*/
		switch(L->bf)
		{	/*检查T的左子树的平衡度，并作相应平衡处理*/
			case LH:	/*新结点插入在T的左子树上，要作单右旋处理*/
				(*T)->bf=L->bf=EH;
				R_Rotate(T);
				break;
			case RH:	/*新结点插入在T的左孩子的右子树上，要作双旋处理*/
				Lr=L->rchild;		/*Lr指向T的左孩子的右子树根*/
				switch(Lr->bf)		/*修改T及其左孩子的平衡因子*/
				{
					case LH: (*T)->bf=RH;
							L->bf=EH;
							break;
					case EH: (*T)->bf=L->bf=EH;
							break;
					case RH: (*T)->bf=EH;
							L->bf=LH;
							break;
				}
				Lr->bf=EH;
				L_Rotate(&(*T)->lchild);	/*对T的左子树作左旋平衡处理*/
				R_Rotate(T);				/*对T作右旋平衡处理*/
		}
	}
<p>
主函数：
</p>
	/* 若在平衡的二叉树排序树T中不存在和e有相同关键的结点，则插入一个 */
	/* 数据元素为e的新结点并返回1，否则返回0.若因插入而使二叉排序树 */
	/* 失去平衡，则作平衡旋转处理，布尔变量taller反映T长度与否 */
	Status InsertAVL(BiTree *T, int e, Status *taller)
	{
		if(!*T)
		{	/*插入新结点，树“长高”，置taller为TRUE*/
			*T=(BiTree)malloc(sizeof(BiTNode));
			(*T)->data=e;
			(*T)->lchild=(*T)->rchild=NULL:
			(*T)->bf=EH;
			*taller=TRUE;			
		}
		else
		{
			if (e==(*T)->data)
			{	/* 树中已存在和e有相同关键字的结点则不再输入 */
				*taller=FALSE;
				return FALES;
			}
			if (taller)		/* 已插入到T的左子树中且左子树“长高” */
			{
				switch((*T)->bf)	/*检查T的平衡度*/
				{
					case LH:	/*原本左子树比右子树，需要作平衡处理*/
							LeftBalance(T);
							*taller=FALSE;
							break;
					case EH:	/*原本左右子树等高，现因左子树增高而树增高*/
							(*T)->bf=LH;
							*taller=TRUE;
							break;
					case RH:	/*原本右子树比左子树高，现左右子树等高*/
							(*T)->bf=EH;
							*taller=FALSE;
							break;
				}
			}
		}
		else
		{	/*应继续在T的右子树中进行搜索*/
			if(!InsertAVL(&(*T)->rchild,e,taller))	/*未插入*/
				return FALSE;
			if(*taller)		/*已插入到T的右子树且右子树“长高”*/
			{
				switch((*T)->bf)	/*检查T的平衡度*/
				{
					case LH:	/*原本左子树比右子树高，现左、右子树等高*/
							(*T)->bf=EH;
							*taller=FALSE;
							break;
					case EH:	/*原本左右子树等高，现因右子树增高而树增高*/
							(*T)->bf=RH;
							*taller=TRUE;
							break;
					case RH:	/*原本右子树比左子树高，需要作右平衡处理*/
							RightBalance(T);
							*taller=FALSE;
							break;
				}
			}
		}
		return TRUE;
	}
####多路查找树（B树）
***