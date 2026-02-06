In the last class, I have discussed sorting algorithms like bubble sort. Furthermore I have mentioned the following approach:

1) Finding the smallest element in unsorted_list  
2) Adding that element to sorted_list  
3) Marking the selected element in unsorted_list with a large value (500) so it won’t be chosen again  
4) Printing both arrays after each pass

I have written this code in C++. This is my goto language. This does not mean that I dont know Java but rather lazy to write long written lines of code. Since you are taking an intermediate Java, I am sharing this code in C++. You are going to transform this logic using Java. This will be an exiciting exercise for those who have nothing to do except programming. Try this and if you really struggle, I will share the ready made version in Java.

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> unsorted_list = {11, 10, 2, 15, 9, 1};
    vector<int> sorted_list;
    int min;
    int num = -1;

    for (int outer_loop = 0; outer_loop < unsorted_list.size(); outer_loop++) {
        min = unsorted_list[++num];
        for (int i = 0; i < unsorted_list.size(); i++) {
            if (min < unsorted_list[i]) {
                continue;
            } else {
                min = unsorted_list[i];
            }
        }
        sorted_list.push_back(min);
        //Linear search
        for (int i = 0; i < unsorted_list.size(); i++) {
            if (min == unsorted_list[i]) {
                unsorted_list[i] = 500;
            }
        }

        for (int i: unsorted_list) {
            cout << i << ' ';
        }
        cout << endl;

        cout << "Sorted Array: ";
        for (int i: sorted_list) {
            cout << i << " ";
        };
        cout << endl;
    }
    return 0;
}

```
