# what is Segmentation Tree?
- An efficient data structure that allows:
- 1. Efficient Querying of Intervals/range.
- 2. Efficient Updating of Intervals/range.

# where we can use?
- Range queries to find SUM,MIN,MAX,etc...

# Representation
- Balanced Binary Tree.
- Height = log(n) (base 2).(n--> size of array)
- Every non-leaf node contains 2-childrens.
- leaf node : represents a single element in the array.
- Root node : represents entire array(eg.sum of all the elements of array).
- other nodes : represents an interval or range of an array.

# Constructing/Building the segmentation tree.
- Tree is represented in the form of array.
- ```js
    // node is at index (i),then its left child is at index (2*i+1) and right at (2*i+2).
- we create an segtree array of size 2*n.
- code for construction.
- ```js
    segtree=new int[2*n];
    // given array nums.
    BT(i,l,r){//i=0 initailly,l=0 and r=size of array.
    //Base case
        if(l==r){
            segtree[i]=nums[l];//we can use nums[r] --> l==r.
            return;
        }
        int mid=(l+r)/2;
        BT(2*i+1,l,mid);//calling for left child.
        BT(2*i+2,mid+1,r);//calling for right child.
        segtree[i]=segtree[2*i+1]+segtree[2*i+2];
        return;
    }
    // TC = O(n);
    // SC = O(n);

# operations on segmentation tree.
# 1.updating a value in SegTree.
- ```js 
    void update(idx,val,i,l,r){
        //idx=index at which we want to change with value=val,i=0 from root,l and r are (0,size of arr-1);
        if(l==r){
            segtree[i]=val;
            return;
        }
        int mid=(l+r)/2;
        if(idx<= mid){
            //search in left tree
            update(idx,val,2*i+1,l,mid);
        }else{
            //search in right tree
            update(idx,val,2*i+2,mid+1,r);
        }
        segtree[i]=segtree[2*i+1]+segtree[2*i+2];
    }
    // TC = O(log(n))

# Range sum query.
- To the sum in range(start,end)
- start with root node (0,n).(here l=0,r=n)
- There are three possible cases for any node (l,r):
- 1.(l,r) is out of bound for (start,end).
- 2.(l,r) is in the range of (start,end).
- 3.(l,r) is overlapped but not completely part of (start,end).
- code:
- ```js
    int query(start,end,i,l,r){
        if(l>end || r<start) {
            return 0;
        }else if(l>=start && r<=end){
            return segtree[i];
        }
        int mid=(l+r)/2;
        return query(start,end,2*i+1,l,mid) + query(start,end,2*i+2,mid+1,r);
    }
    // TC = O(log(n))
- problem in gfg :https://www.geeksforgeeks.org/problems/range-sum-queries2353/1