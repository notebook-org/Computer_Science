## std::thread within a class with parameters

	#include <iostream>
	#include <thread>
	include <unistd.h>

	class T{
	public:
	  T(){
	    _t = new std::thread(&T::Callback, this, 5, 's');
	  }
	private:
	  void Callback(int num, char ch){
	    while(true){
	      std::cout<<ch<<num<<std::endl;
	      usleep(1000000);
	    }
	  }
	  std::thread* _t;
	};
	
	int main(){
	  T t;
	  while(true){}
	  return 0;
	} 