finding the max element in an array
#leetcode

```cpp
int find_max_element(int arr[]){
	
	int size_arr = sizeof(arr) / sizeof(arr[0]);
	int start = arr[0]; // we intiailize 0 because thats our start
	int max_e {}; // we initialize a max to store the elements

	for(int i = 0; i < size_arr; ++i){
		if(arr[i] > start){
			max_e = arr[i];
		}
	} 
	return max_e
}

int main(){
	
	int arr[] = {1,2,5,4,7};
	int max_e = find_max_element(arr); 
}
```