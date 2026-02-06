In the last class, we talked about sorting algorithms, including the ever-famous bubble sort (yes, the one that bubbles its way slowly to success 🫧).
I then mentioned an alternative approach that works like this:

Find the smallest element in unsorted_list
Move that poor little element into sorted_list
Mark its original spot with a very large number (500) so it never gets picked again
Print both arrays after each pass so we can watch the drama unfold
I went ahead and implemented this logic in C++, because… well… that’s my go-to language.
This does not mean I don’t know Java 😌
It simply means I’m lazy and C++ lets me write fewer lines to do the same thing. Productivity, right?
Since you’re taking an intermediate Java course, I’m sharing this C++ code with you and asking you to translate the logic into Java. Think of it as a language workout—same brain, different syntax muscles 💪

This will be an exciting exercise for those who:

love programming ❤️
have free time ⏳
or have absolutely nothing better to do than write code 😄
Give it an honest try.
And if you really struggle (or start questioning your life choices), don’t worry—I’ll share the ready-made Java version later.
Until then… happy coding ☕👨‍💻👩‍💻

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
