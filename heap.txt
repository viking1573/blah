#include<iostream>
using namespace std;
class Heap{
	int *arr;
	
	public:
		int n;
		Heap(){
			cout<<"Enter size of tree: ";
			cin>>n;
			arr=new int(n);
		}
		void create();
		void swap(int[],int,int);
		void max_heapify(int,int);
		void heapsort(int);
		void display();
};

void Heap::swap(int arr[],int a,int b){
	int temp;
	temp=arr[a];
	arr[a]=arr[b];
	arr[b]=temp;
}

void Heap::create(){
	int i=0;
	while(i<n)
	{
		cout<<"Enter array element: ";
		cin>>arr[i];
		i++;
	}
}

void Heap::max_heapify(int i,int n){
	int left=2*i+1;
	int right=2*i+2;
	int largest;
	if(left<n && arr[left]>arr[i]){
		largest=left;
	}
	else{
	 	largest=i;
	}
	if(right<n && arr[right]>arr[largest]){
		largest=right;
	}
	if(largest!=i){
		swap(arr,i,largest);
		max_heapify(largest,n);
	}
}

void Heap::heapsort(int n){
	for(int i=(n/2)-1;i>=0;i--){
		max_heapify(i,n);
	}
	for(int i=n-1;i>=0;i--){
		swap(arr,0,i);
		max_heapify(0,i);
	}
}

void Heap::display(){
	cout<<"Sorted array is: ";
	for(int i=0;i<n;i++){
		cout<<arr[i]<<" ";
	}
}

int main(){
	Heap obj;
	obj.create();
	obj.heapsort(obj.n);
	obj.display();
}
