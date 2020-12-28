####Creating mock class:
- Let us assume we want to mock the following methods of class Operate:
	- int Operate::Add(int a, int b);
	- void Operate::Take(int a);

class Operate{
public:
  MOCK_METHOD2(Add, int(int a, int b));
  MOCK_METHOD1(Take, void(int a));
 }