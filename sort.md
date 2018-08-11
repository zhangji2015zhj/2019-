典排序算法在面试中占有很大的比重，也是基础。包括冒泡排序，插入排序，选择排序，希尔排序，归并排序，快速排序，堆排序。希望能帮助到有需要的同学。全部程序采用Java实现。

本篇所有排序实现均默认从小到大。

一、冒泡排序 BubbleSort

介绍：
冒泡排序的原理非常简单，它重复地走访过要排序的数列，一次比较两个元素，如果他们的顺序错误就把他们交换过来。

步骤：
比较相邻的元素。如果第一个比第二个大，就交换他们两个。
对第0个到第n-1个数据做同样的工作。这时，最大的数就“浮”到了数组最后的位置上。
针对所有的元素重复以上的步骤，除了最后一个。
持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。

/**
	 * 冒泡排序算法
	 * 原理是临近的数字两两进行比较,按照从小到大或者从大到小的顺序进行交换,这样一趟过去后,最大或最小的数字被交换到了最后一位,然后再从头开始进行两两比较交换,直到倒数第二位时结束
	 * @param nums 被排序的数组
	 * @param n 数组长度
	 * 最坏情况：O(n2)  如果未优化的冒泡排序，最好情况也是O（n2），优化后最好情况是O（n）
	 */
	public void BubbleSort(int[] nums,int len){
		for(int i=0;i<len-1;i++){ //一趟比较
			for(int j=0;j<<strong>len-1-i</strong>;j++){ //一次比较,每次把最大值放在最后面，所以下一次比较的时候不用对后i个数比较了
				int temp = nums[j];
				if(nums[j] > nums[j+1]){
					nums[j] = nums[j+1];
					nums[j+1] = temp;
				}
			}
		}		system.out.println("冒泡排序：");
		for (int i : nums) {
			System.out.print(i+" ");
		}
	}


不过针对上述代码还有两种优化方案。

优化1：某一趟遍历如果没有数据交换，则说明已经排好序了，因此不用再进行迭代了。用一个标记记录这个状态即可（程序如下）。

优化2：记录某次遍历时最后发生数据交换的位置，这个位置之后的数据显然已经有序，不用再排序了。因此通过记录最后发生数据交换的位置就可以确定下次循环的范围了（上面程序中" j<=len-1-i" 实现）。

public void betterBubbleSort(int[] nums,int len){
		boolean flag;
		flag = true;
		for(int i=0;i<len-1 && flag;i++){ //一趟比较 如果上趟比较一次也没有交换，则说明后面都排好序了，不用再比较了
			flag = false;
			for(int j=0;j<len-1-i;j++){ //一次比较,每次把最大值放在最后面，所以下一次比较的时候不用对后i个数比较了
				int temp = nums[j];
				if(nums[j] > nums[j+1]){
					nums[j] = nums[j+1];
					nums[j+1] = temp;
					flag = true;
				}
			}
		}
		System.out.println("优化后的冒泡排序：");
		for (int i : nums) {
			System.out.print(i+" ");
		}
	}



二、选择排序 SelectionSort

介绍：
选择排序无疑是最简单直观的排序。它的工作原理如下。

步骤：
在未排序序列中找到最小（大）元素，存放到排序序列的起始位置。
再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。
以此类推，直到所有元素均排序完毕。
<span style="font-size:14px;font-weight: normal;">/**
	 * 选择排序算法
	 * 基本思想是：每一趟从待排序的记录中选出关键字最小的记录，顺序放在已排好序的子序列前面，直到全部记录排序完毕。
	 * @param nums 被排序的数组
	 * @param n 数组长度
	 * 最坏情况：O（n2） ，最好情况：O（n2）
	 */
	public void SelectSort(int[] nums,int len){
		for(int i=0;i<len;i++){
			int min = nums[i]; //先把每一趟最小值暂定为nums[i]
			int index = i; //记录最小值所在的索引值
			for(int j=i+1;j<len;j++){ //开始一趟比较：从i+1位置到数组末尾比较，找出最小值并记录位置
				if(nums[j] < min){
					min = nums[j];
					index = j;
				}
			}
			//将nums[i]和最小值交换
			nums[index] = nums[i]; 
			nums[i] = min;
		}
		System.out.println("选择排序：");
		for (int i : nums) {
			System.out.print(i+" ");
		}
	}</span>


三、插入排序 InsertionSort

介绍：
插入排序的工作原理是，对于每个未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。

步骤：
从第一个元素开始，该元素可以认为已经被排序
取出下一个元素，在已经排序的元素序列中从后向前扫描
如果被扫描的元素（已排序）大于新元素，将该元素后移一位
重复步骤3，直到找到已排序的元素小于或者等于新元素的位置
将新元素插入到该位置后
重复步骤2~5

排序演示：


/**
	 * 插入排序算法
	 * @param nums 被排序的数组
	 * @param n 数组长度
	 * 最坏情况：输入数组已反向排序  O（n2）； 最好情况：输入数组已排序  O（n）；平均情况：O（n2）
	 * 由于插入排序其内层循环非常紧凑，对于小规模输入，插入排序是一种非常快的排序算法
	 */
	public void InsertSort(int[] nums,int len){
		int j;
		for(int i=1;i<len;i++){
			int temp = nums[i];
			for(j=i;j>0;j--){
				if(temp < nums[j-1]){
					nums[j] = nums[j-1]; //将所有在nums[i]之前的大于nums[i]的值都往后移一位
				}
				else break; 
			}
			//移完所有大于nums[i]的值后，j刚好指向最靠前一个大于nums[i]的位置
			nums[j] = temp;
		}
		System.out.println("插入排序：");
		for (int i : nums) {
			System.out.print(i+" ");
		}
	}

四、希尔排序 ShellSort

介绍：
希尔排序，也称递减增量排序算法，实质是分组插入排序。由 Donald Shell 于1959年提出。希尔排序是非稳定排序算法。

希尔排序的基本思想是：将数组列在一个表中并对列分别进行插入排序，重复这过程，不过每次用更长的列（步长更长了，列数更少了）来进行。最后整个表就只有一列了。将数组转换至表是为了更好地理解这算法，算法本身还是使用数组进行排序。

例如，假设有这样一组数
[ 13 14 94 33 82 25 59 94 65 23 45 27 73 25 39 10 ]
，如果我们以步长为5开始进行排序，我们可以通过将这列表放在有5列的表中来更好地描述算法，这样他们就应该看起来是这样：

13 14 94 33 82
25 59 94 65 23
45 27 73 25 39
10

然后我们对每列进行排序：

10 14 73 25 23
13 27 94 33 39
25 59 94 65 82
45

将上述四行数字，依序接在一起时我们得到：
[ 10 14 73 25 23 13 27 94 33 39 25 59 94 65 82 45 ]
。这时10已经移至正确位置了，然后再以3为步长进行排序：

10 14 73
25 23 13
27 94 33
39 25 59
94 65 82
45

排序之后变为：

10 14 13
25 23 33
27 25 59
39 65 73
45 94 82
94

最后以1步长进行排序（此时就是简单的插入排序了）。

/**
	 * 希尔排序算法
	 * @param nums 被排序的数组
	 * @param n 数组长度
	 * 最坏情况：O（n2） 使用Hibbard增量的最坏情况：O（n^3/2）
	 */
	public void ShellSort(int[] nums,int len){
		int increment;
		int temp,i,j;
		for(increment = len/2;increment > 0;increment /= 2){ //增量为len/2 len/4 len/8.....1
			for(i=increment;i<len;i++){ //对每个子序列进行插入排序
				temp = nums[i];
				for(j=i;j>=increment;j -= increment){
					if(temp < nums[j-increment]){
						nums[j] = nums[j-increment];
					}
					else
						break;
				}
				nums[j] = temp;
			}
		}
		System.out.println("希尔排序：");
		for (int k : nums) {
			System.out.print(k+" ");
		}
	}

五、归并排序 MergeSort

介绍：
归并排序是采用分治法的一个非常典型的应用。
归并
排序的思想就是先递
归
分解数组，再
合
并数组。

先考虑合并两个有序数组，基本思路是比较两个数组的最前面的数，谁小就先取谁，取了后相应的指针就往后移一位。然后再比较，直至一个数组为空，最后把另一个数组的剩余部分复制过来即可。

再考虑递归分解，基本思路是将数组分解成
left
和
right
，如果这两个数组内部数据是有序的，那么就可以用上面合并数组的方法将这两个数组合并排序。如何让这两个数组内部是有序的？可以再二分，直至分解出的小组只含有一个元素时为止，此时认为该小组内部已有序。然后合并排序相邻二个小组即可。

排序演示：

/**
	 * 归并排序算法
	 * 将待排序序列R[0...n-1]看成是n个长度为1的有序序列，将相邻的有序表成对归并，得到n/2个长度为2的有序表；将这些有序序列再次归并，
	 * 得到n/4个长度为4的有序序列；如此反复进行下去，最后得到一个长度为n的有序序列。
	 * 综上可知：归并排序其实要做两件事：（1）“分解”——将序列每次折半划分。（2）“合并”——将划分后的序列段两两合并后排序。
	 * @param nums
	 * @param len
	 * O(nlogn)
	 */
	public void MergeSort(int[] nums,int len){
		sort(nums, 0, len-1);
		System.out.println("归并排序：");
		for (int k : nums) {
			System.out.print(k+" ");
		}
	}
	//分段 将一个数组分成2个数组
	public void sort(int[] nums,int low,int high){
		int mid = (high+low)/2;
		if(low < high){
			sort(nums, low, mid);
			sort(nums, mid+1, high);
			merge(nums, low, mid, high);
		}
	}
	// 分段排序 再合起来
	public void merge(int[] array,int low,int mid,int high){
		int i=low; //第一段序列下标
		int j=mid+1; //第二段序列下标
		int k=0; //第三段序列下标
		int[] array2 = new int[high - low + 1]; //新序列
		while(i<=mid && j<=high){ //把两个子序列的头元素比较，取较小者进入新序列，然后在旧序列中跳过这个较小值，开始下一次比较
			if(array[i] <= array[j]){
				array2[k++] = array[i++];
			}
			else{
				array2[k++] = array[j++];
			}
		}
		if(i <= mid){ //说明上面是j溢出退出循环，即序列1还未比较完
			while(i<=mid){ //若第一段序列还没扫描完，将其全部复制到合并序列
				array2[k++] = array[i++];
			}
		}
		else if(j <= high){
			while(j<=high){ //若第二段序列还没扫描完，将其全部复制到合并序列
				array2[k++] = array[j++];
			}
		}
		for(k=0;k<array2.length;k++){
			array[k+low] = array2[k];//将分段排序的新数组复制到之前数组
		}
	}

六、快速排序 QuickSort

介绍：
快速排序通常明显比同为Ο(n log n)的其他算法更快，因此常被采用，而且快排采用了分治法的思想，所以在很多笔试面试中能经常看到快排的影子。可见掌握快排的重要性。

步骤：
从数列中挑出一个元素作为基准数。
分区过程，将比基准数大的放到右边，小于或等于它的数都放到左边。
再对左右区间递归执行第二步，直至各区间只有一个数。

排序演示：


/**
	 * 快速排序算法
	 * 快速排序采用的思想是分治思想。快速排序是找出一个元素（理论上可以随便找一个）作为基准(pivot),
	 * 然后对数组进行分区操作,使基准左边元素的值都不大于基准值,基准右边的元素值 都不小于基准值，如此作为基准的元素调整到排序后的正确位置。
	 * 递归快速排序，将其他n-1个元素也调整到排序后的正确位置。最后每个元素都是在排序后的正 确位置，排序完成。
	 * 所以快速排序算法的核心算法是分区操作，即如何调整基准的位置以及调整返回基准的最终位置以便分治递归。
	 * @param nums
	 * @param len
	 * O(NlogN)
	 */
	public void QuickSort(int[] nums,int len){
		Qsort(nums,0,len-1);
		System.out.println("快速排序：");
		for (int k : nums) {
			System.out.print(k+" ");
		}
	}
	public void Qsort(int[] nums, int left, int right) {
		if(left>right) return;
		int pivot = nums[left];
		int i = left;
		int j = right;
		while(i < j){
			while(nums[j] >= pivot && i<j){ //从右往左找比nums[i]小的数
				j--;
			}
			nums[i] = nums[j]; //找到之后交换
			while(nums[i] <= pivot && i<j){ //从左往右找比nums[j]大的数
				i++;
			}
			nums[j]  = nums[i];	 //找到之后交换
		}
		//while执行完后，必然有 i==j 
		nums[i] = pivot; //将基准数归位
		Qsort(nums, left, i-1); //递归处理左边
		Qsort(nums, i+1, right); //递归处理右边
	}

七、堆排序 HeapSort

介绍：
堆排序在 top K 问题中使用比较频繁。堆排序是采用二叉堆的数据结构来实现的，虽然实质上还是一维数组。二叉堆是一个近似完全二叉树 。

二叉堆具有以下性质：
父节点的键值总是大于或等于（小于或等于）任何一个子节点的键值。
每个节点的左右子树都是一个二叉堆（都是最大堆或最小堆）。

步骤：
构造最大堆（Build_Max_Heap）：若数组下标范围为0~n，考虑到单独一个元素是大根堆，则从下标
n/2
开始的元素均为大根堆。于是只要从
n/2-1
开始，向前依次构造大根堆，这样就能保证，构造到某个节点时，它的左右子树都已经是大根堆。


堆排序（HeapSort）：由于堆是用数组模拟的。得到一个大根堆后，数组内部并不是有序的。因此需要将堆化数组有序化。思想是移除根节点，并做最大堆调整的递归运算。第一次将
heap[0]
与
heap[n-1]
交换，再对
heap[0...n-2]
做最大堆调整。第二次将
heap[0]
与
heap[n-2]
交换，再对
heap[0...n-3]
做最大堆调整。重复该操作直至
heap[0]
和
heap[1]
交换。由于每次都是将最大的数并入到后面的有序区间，故操作完后整个数组就是有序的了。


最大堆调整（Max_Heapify）：该方法是提供给上述两个过程调用的。目的是将堆的末端子节点作调整，使得子节点永远小于父节点 。

排序演示：


/**
	 * 堆排序算法(max堆)
	 * @param nums 被排序的数组
	 * @param n 数组长度
	 * 时间复杂度 O（nlogn）
	 * 要先构建最大堆，然后循环删除堆的根节点上的最大值，并将它移到堆末尾，并将堆长度减一，再开始下一次的删除根节点
	 */
	public void HeapSort(int[] nums,int len){
		//构建最大堆
		for(int i=len/2;i>=0;i--){
			percDown(nums,i,len);
		}
		//循环，每次把根节点和最后一个节点调换位置
		for(int i=len-1;i>=1;i--){
			//Swap(nums[0],nums[i])交换nums[0]和nums[i]
			int temp = nums[0];
			nums[0] = nums[i];
			nums[i] = temp;
			percDown(nums,0,i);
		}
		
		System.out.println("堆排序：");
		for (int k : nums) {
			System.out.print(k+" ");
		}
	}
		/**
		 * 堆调整，使其生成最大堆
		 * @param nums
		 * @param i
		 * @param size
		 */
		public void percDown(int[] nums,int i,int size){
			int left = 2*i+1;
			int right = 2*i+2;
			int max = i;
			if(left < size && nums[left] > nums[max]){
				max = left;
			}
			if(right < size && nums[right] > nums[max]){
				max = right;
			}
			if(max != i){
				int temp = nums[i];
				nums[i] = nums[max];
				nums[max] = temp;
				percDown(nums,max,size);
			}
			
		}

总结

下面为七种经典排序算法指标对比情况：



摘选自书圈：https://mp.weixin.qq.com/s/VdSZq4U5pHQQ2LXdeVrO0A