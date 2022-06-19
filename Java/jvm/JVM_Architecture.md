# JVM 메모리 구조
자바 메모리 구조에 대해 다뤄 봅니다.

- JVM이 무엇인지
- JVM 메모리 영역의 역할과 이해

## JVM(Java Virtual Machine)
JVM은 운영체제에 독립적입니다. 다른 운영체제를 사용하는 컴퓨터 마다 JVM이 존재하고, 사용자는 .class 파일을 운영체제에 제출하기만 하면, JVM이 바이트 코드를 기계 수준으로 해석하여 실행합니다.

따라서 JVM은 운영체제에 독립적이며, 자바 가상 머신으로 자바 바이트 코드를 실행할 수 있는 런타임 환경을 제공하는 사양입니다.

## JVM Architecture
![jvmArchitecture.png](JVM_Architecture.png)

### 1) Class Loader
클래스 로더는 JVM 안으로 클래스 파일들을 읽어들이는 역할을 하는 시스템입니다.

### JVM Memory
JVM Memory는 JVM이 프로그램을 수행하기 위해 운영체제로부터 할당받는 메모리 영역입니다. 각각의 목적에 따라 5개의 영역으로 나누어져 있습니다.
Runtime Data Area라고도 불립니다.

#### 2) Method Area
프로그램 실행 중 클래스가 사용되면 JVM은 해당 클래스 파일을 분석하여 클래스의 클래스 변수, 인스턴스 변수, 메서드, 생성자 등을 Method Area에 저장합니다. 

#### 3) Heap
new 키워드로 생성된 객체와 관련 인스턴스 변수 및 배열은 Heap Area에 저장됩니다.

Heap Area의 자원은 모든 쓰레드에 공유되어 쓰레드에 안전하지 않습니다.  
Heap Area은 Garbage Collection의 대상이 되는 영역입니다.


#### 4) JVM Language Stack
스레드 제어를 위해 사용되는 메모리 영역입니다. 스레드가 생성될 때마다 각 스레드는 스레드마다 하나의 스택을 할당 받습니다.

메서드가 호출될 때마다 스택 안에서는 각각의 스택 프레임(해당 메서드만을 위한 고유한 공간)이 생성됩니다.
스택 프레임은 FILO(First In Last Out) 구조로 되어 있고, 해당 메서드 안에서 사용되는 지역변수들을 담고 있으며, 메서드 수행이 끝나면 프레임 별로 삭제됩니다. 


#### 5) PC Registers
각 스레드에는 별도의 PC Register가 존재하며, PC Register는 현재 실행 중인 JVM 명령어의 주소를 저장합니다. 

#### 6) Native Method Stacks
자바 외 언어에서 제공하는 메서드의 정보가 저장되는 공간입니다. JNI(Java Native Interface)을 통해 표준에 가까운 방식으로 구현이 가능합니다.

#### 7) Execution Engine
클래스 로더를 통해 JVM Memory에 배치된 자바 바이트 코드들을 명령어 단위로 읽어서 실행하는 모듈입니다.

#### 8) Native Method Interface
Native Applications(하드웨어와 운영체제에 종속된 프로그램), C, C++ 등의 다른 언어들로 작성된 라이브러리들을 호출하거나 호출되는 것을 가능하게 하는 프로그래밍 프레임워크입니다. 


#### 9) Native Method Libraries
Execution Engine에 필요한  Native Libraries(C, C++) 모음입니다.







# Reference
- https://www.guru99.com/java-virtual-machine-jvm.html
- https://hyoje420.tistory.com/2
- https://www.holaxprogramming.com/2013/07/16/java-jvm-runtime-data-area/