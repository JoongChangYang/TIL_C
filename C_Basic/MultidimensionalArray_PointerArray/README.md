# 다차원 배열과 포인터 배열

> 다양한 차원의 배열을 표현하는 방법을 학습
>
> 포인터를 이용해 2차원 배열을 다루는 방법을 학습



## Contents

- [다차원 배열](#다차원-배열)
- [포인터 배열](#포인터-배열)



### 다차원 배열

#### 2차원 배열

- 행렬 데이터를 표현할때, 그래프 알고리즘을 처리할 때, 다수의 실생활 데이터를 처리할때 등 사용함

- 흔히 우리가 보는 표 구조가 2차원 배열과 흡사함

  |  이름  | 영어 성적 | 수학 성적 | 국어 성적 |
  | :----: | :-------: | :-------: | :-------: |
  | 홍길동 |    85     |    97     |    79     |
  | 유관순 |    100    |    89     |    98     |
  | 이순신 |    99     |    77     |    99     |
  | 장보고 |    89     |    70     |    98     |

- 2차원 배열의 초기화

  - 2차원 배열은 1차원 배열이 중첩되었다는 의미로 `[]`를 두번 연속하여 쓴다

    `Type` `name` `[columnSize]` `[rowSize]` = `{ {value, value}, {value, value} }`

  - 2차원 배열 또한 기본적으로 인덱스 0부터 시작한다

    | 열(row)\행(column) |     0     |     1     |     2     |
    | :----------------: | :-------: | :-------: | :-------: |
    |         0          | `A[0][0]` | `A[0][1]` | `A[0][2]` |
    |         1          | `A[1][0]` | `A[1][1]` | `A[1][2]` |
    |         2          | `A[2][0]` | `A[2][1]` | `A[2][2]` |
    |         3          | `A[3][0]` | `A[3][1]` | `A[3][2]` |

- 기본 예제 코드

  ``` c
  #include <stdio.h>
  
  int arr[3][3] = { {1, 2, 3}, {4, 5, 6}, {7, 8, 9} };
  
  int main(void) {
  
  	int i, j;
  
  	for (i = 0; i < 3; i++) {
  		for (j = 0; j < 3; j++) {
  			printf("%d ", arr[i][j]);
  		}
  		printf("\n");
  	}
  	/*
  	실행 결과
  	1 2 3
  	4 5 6
  	7 8 9
  	*/
  	system("pause");
  	return 0;
  }
  ```



#### 3차원 배열

- 3차원 배열 이상의 다차원 배열 또한 사용할 수 있다

    ``` c
    int arr[2][3][3] =
    {
        { {1, 2, 3}, {4, 5, 6}, {7, 8, 9} },
        { {1, 2, 3}, {4, 5, 6}, {7, 8, 9} }
    };

    int main(void) {

        int i, j, k;

        for (i = 0; i < 2; i++) {

            for (j = 0; j < 3; j++) {

                for (k = 0; k < 3; k++) {
                    printf("%d ", arr[i][j][k]);
                }
                printf("\n");
            }
            printf("\n");
        }

        /*
        실행 결과
        1 2 3
        4 5 6
        7 8 9

        1 2 3
        4 5 6
        7 8 9
        */
        system("pause");
        return 0;
    }
    ```



### 포인터 배열

- **배열**은 **포인터**와 동일한 방식으로 동작한다

- **배열**의 이름은 **배열**의 원소의 첫번째 **주소**가 된다

  ``` c
  int array[5] = { 1, 2, 3, 4, 5 }; // array는 배열의 주소를 가짐
  int *pointerArray = array; // 포인터 변수에 array 할당
  
  printf("array 값: %d\n", array);
  printf("array 주소 값: %d\n", &array);
  printf("array[0] 주소 값: %d\n", &array[0]);
  printf("========================\n");
  printf("pointerArray 값: %d\n", pointerArray);
  printf("pointerArray 주소 값: %d\n", &pointerArray);
  
  /*
  실행 결과
  array 값: 7339692
  array 주소 값: 7339692
  array[0] 주소 값: 7339692 -> 배열의 주소값은 배열 원소의 첫번째 주소이기 때문에 array의 주소와 array[0]의 주소가 동일함
  ========================
  pointerArray 값: 7339692 -> pointerArray가 array와 동일한 주소를 가리킴
  pointerArray 주소 값: 7339680
  */
  ```
  
- 유일한 차이점이라고 하면, **포인터**는 **변수**이고 **배열**의 이름은 **상수**이다

  - 잘못된 예시

      ``` c
      int someNumber = 10;
      int array[10]; // array = &someNumber; Error: 식이 수정할 수 있는 lavalue여야 합니다.
      /*
      배열은 상수이기 때문에 변경이 불가능하다
      */
      ```
    
  - 올바른 예시
  
      ``` c
      int array[5] = { 1, 2, 3, 4, 5 };
      
      int *pointerArray = array; // 포인터 변수에 array주소를 할당
      
      printf("%d\n", pointerArray[2]); // 포인터가 가리키는 array로 접근하여 해당 index의 값을 반환
      
      /*
      실행 결과
      3
      */
      ```

- 포인터는 연산을 통해 **자료형의 크기만큼** 이동한다

  ``` c
  int array[5] = { 1, 2, 3, 4, 5 };
  	
  int i;
  
  for (i = 0; i < 5; i++) {
      // (int)형 포인터는 4바이트(Byte)씩 이동한다
      
      printf("array[%d] 주소 값: %d\n", i, array + i);
      printf("포인터로 접근한array[%d] 값: %d\n", i, *(array + i));
      printf("배열로 접근한 arry[%d] 값: %d\n\n", i, array[i]);
  }
  
  /*
  실행 결과
  array[0] 주소 값: 9304152
  포인터로 접근한array[0] 값: 1
  배열로 접근한 arry[0] 값: 1
  
  array[1] 주소 값: 9304156
  포인터로 접근한array[1] 값: 2
  배열로 접근한 arry[1] 값: 2
  
  array[2] 주소 값: 9304160
  포인터로 접근한array[2] 값: 3
  배열로 접근한 arry[2] 값: 3
  
  array[3] 주소 값: 9304164
  포인터로 접근한array[3] 값: 4
  배열로 접근한 arry[3] 값: 4
  
  array[4] 주소 값: 9304168
  포인터로 접근한array[4] 값: 5
  배열로 접근한 arry[4] 값: 5
  
  주소값은 4Byte씩 이동하였고 해당 주소값에 위치한 값은 배열의 원소 값과 같음 
  */
  ```

  

  

