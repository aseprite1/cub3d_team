>05/21 파싱 완성 (아마도..?)
>
* **헤더파일 미완성 + 틀린 부분 수정 필요.**

* 로직 에러시 종료할 때 exit_process호출로 모두 적절하게 free & release 가능.
	- mlx destroy 부분 등 수정 필요할 수 있음.

* **맵 파싱 더 다양한 예외케이스 넣어봐야 함.**

* **헤더 면 c파일 norm에러 부분은 추후에 고쳐야 함.**
	(나중에 까먹지 않도록 일부러 에러 낸 것)
	- 헤더는 leaks 처리 완벽하게 한 이후 나중에 주석만 제거하면 됨.
	- init_s_info.c의 경우 아직 헤더 미완성이라 추후에 나누기.
	- exit_process.c의 경우 test code의 leaks_check와 의존.
	- main.c 역시 test code와 의존.

* **info_init()과 exit_process()는 구조체가 바뀔 때마다 주의깊게 고쳐야 함**

* **TESTCODE.c 파일은 완성 단계에서 반드시 지울 것!**
	(Makefile과 헤더, c파일 모두!)

* mlx함수 및 dda알고리즘 공부!
	(선을 만들어보자..)



>05/22
>
TO_DO : mlx, raycasting(dda algorithm) 공부 및 연습
	TESTCODE.c와 main.c에 작성하였음(지워야 함)

* ~rgb를 종합해서 int형으로 바꿀 수 있음. 미리 연산해서 구조체에 넣어두고 지금 있는 변수들 없애야 함.~



>05/23
>
* ft_split 대신  ft_rectangle_split을 새로 만들어 사용하였음.
	(그러나 미니맵을 띄울 경우 최대 사이즈인 str 맨 끝에 ' '가 포함된 경우에 대한 처리가 필요할 수 있음)

* **충돌은 구현하지 않더라도, 맵의 최대 범위나 최소 범위 벗어난 것에 대한 예외처리는 해야 세그폴트 막을 수 있을 듯.**

* rgb값을 하나의 int형으로 바꿔주는 연산 처리함. (t_info구조체 바뀜)
**** 구조체가 바뀔 때마다 init_info가 제대로 처리되었는지 확인해야 함!!(까먹지 말자)



>05/24
>
* mlx_ptr, mlx_win, mlx`s imgs 초기화 정리하였음.

* **rotate 방향벡터는 변환하나, 아직 camera_plane 벡터는 변환되지 않음. 이에 대한 변수명도 바꿔줘야 함. 벡터임. (또한 회전이 미세하게 어긋나는 부분이 있음. 다 만들어보고 문제가 있다고 판단되면 바꾸기)**

* 미니맵을 안 그린다는 가정 하에 단 하나의 스크린 이미지만 계속 업데이트하며 사용하는 최적화에 대한 이야기 나눔. 이 방향으로 구현하자.

* **game()의 mlx_loop_hook()의 loop_hook부분에 주석처리된 부분만 작성하면 완성될 것으로 예상됨.**

* **다 만들면 printf()로 찍어보면서 변수 체킹하는 부분, 미니맵 등 모두 꼼꼼하게 확인하고 지우기**
	**(중요! 'textures/'에서도 xpm파일과 png파일 지워줘야 함!!!!!!!!!)**

>05/24
>
* 회전 미세하게 어긋나는 부분 고침. old direction vector를 저장해놓고, 그것을 기준으로 각도 연산을 하는 방식. 부동소수점에 대한 거듭된 연산으로 인해 어긋나는 부분 fix.

* rotate에 plain_dir_vector 연산도 추가. 나중에 레이케스팅할 땐 뒤에 곱연산을 plain으로 하면 됨.

>05/25, 05/26
>
* 레이캐스트 적용 및 이동과 회전 수정

* 등등..

>05/27

* 스페이스 공간 포함한 섬맵 에러띄워야하는데 valid하게 취급됨. 수정해야함!


...what more?

###Q & A

Q. info->first_person.pov는 'East'기준 0, 반시계방향 'North' 90, ...이 맞을까..?
A. 벡터 기반 레이캐스팅으로 하기로 함.

Q. info->first_person.pos.의 double형 x와 y의 초기 시작 위치 좌표는 정수형으로 맞아떨어져야 할까, 아니면 0.5여야 할까..?
A. 맞음.

Q. x11event와 mask값 모두 필요할까..? (일단 필요해보이는 거 찾아서 써놓긴 했는데 정확히 모름)
A. event는 실제 이벤트를 의미하고, mask는 해당 이벤트를 마킹하는 것을 의미하는 것으로 공부함. 그러니까, 예를 들어 event를 key_press로 해놓고 다른 마스크가 관련이 없으면 동작을 안함..?
이에 대해 실험해보기


Q. mlx에서 win_ptr은 destroy하는데, mlx_ptr도 destroy했던가..? 까먹음.
	(내 so_long 코드에서는 안해줬음)
A.

Q. texture를 xpm파일로 받아와서 크기를 구겨서 프린트하는 방법이 있나..?
A.

Q. 동시키 입력을 해야할까?
A. 안해도 됨.

Q. pos_x, y 플레이어 위치 0 미만으로 갈 시 방지하는 부분이 있나요 ?
