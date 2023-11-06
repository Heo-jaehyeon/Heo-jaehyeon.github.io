

---

layout: single
title: "Win32API (3) GetMessage와 PeekMessage"
categories: Win32API
tag: [WIn32API, C++, Study]
toc: true
toc_sticky : true
author_profile: true
search: true

---

# GetMessage

프로세스에는 메세지 큐라고 존재한다

해당 프로그램으로 발생한 메세지들을 메세지큐에 받아놨을텐데 그것을 꺼내보는 함수이다

ex) 그림판에서 마우스클릭 발생 -> 그림판 메세지 큐에 마우스클릭이 들어옴 -> 현재 마우스 위치에 색상을 칠함

해당 프로세스에 포커싱 되어있을때만 메세지 큐에 정보가 들어간다



GetMessage 함수는 메세지큐에서 메세지 확인할때까지 대기. 함수가 종료되지 않는다

한계 : 메세지가 없는 경우에 작동하지 않는다



msg.message == WM_QUIT 일때 false를 반환 -> 프로그램 종료



메세지 큐에 메세지를 아무리 많이 넣어도 처리하는 시간은 순식간이기 때문에 메세지가 발생하지 않는 시간이 더 많다 

# PeekMessage

GetMessage의 한계점을 보완해주는 PeekMessage 함수는 메세지 유무와 관계없이 반환한다

메세지큐에서 메세지를 확인한 경우 true, 메세지큐에 메세지가 없는 경우 false 를 반환한다



```c++
 while (1)
    {
        if (PeekMessage(&msg, nullptr, 0, 0, PM_REMOVE)) // 메세지가 확인된 경우
        {

            if (msg.message == WM_QUIT)
                break;

            if (!TranslateAccelerator(msg.hwnd, hAccelTable, &msg))
            {
                TranslateMessage(&msg);
                DispatchMessage(&msg);
            }
        }
        else // 메세지가 발생하지 않는 대부분의 시간
        {
            CCore::GetInst()->progress();
        }
    }

    return (int) msg.wParam;

}
```
