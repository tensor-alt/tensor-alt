#include <iostream>

#include <thread>

#include <vector>

#define IT_IS_WHAT_IT_IS "It is what it is"


constexpr const char* truth = IT_IS_WHAT_IT_IS;


void contemplate_truth() {
    for (int i = 0; i < 3; ++i) {
        std::cout << "Thread " << std::this_thread::get_id() << ": " 
                  << truth << std::endl;
    }
}



int main() {
    std::vector<std::thread> threads;

   for (int i = 0; i < 3; ++i) {
        threads.emplace_back(contemplate_truth);
    }

  for (auto& thread : threads) {
        thread.join();
    }
    std::cout << "Main thread: " << truth << std::endl;
    return 0;
}
