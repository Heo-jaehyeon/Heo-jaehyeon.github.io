---

layout: single
title: "Win32API (6) Double Buffering"
categories: Win32API
tag: [WIn32API, C++, Study]
toc: true
toc_sticky : true
author_profile: true
search: true

---

## 이중 버퍼링

DC를 하나만 두고( 단일 버퍼링) 정사각형을 그렸을때는 Clear 하고 생성하고 Clear 하고 생성하면 화면이 엄청 깜빡거리는 문제가 발생한다

그러나 이중 버퍼링을 사용하면 작업 중인 화면을 숨겨놓고 미리 그려진 이미지를 표시하므로 화면 깜빡임이 방지된다

즉 버퍼를 2개를 두고(원래 있던 DC와 DC를 하나 더 만들어서) 렌더를 양쪽으로 관리하면 된다



```c++
#include "pch.h"
#include "CCore.h"
#include "CObject.h"
#include "CTimeMgr.h"
#include "CKeyMgr.h"

// CCore* CCore::g_pInst = nullptr;
CObject g_obj;

CCore::CCore()
	: m_hWnd(0)
	, m_ptResolution{}
	, m_hDC(0)
	, m_hBit(0)
	, m_memDC(0)
{
}

CCore::~CCore()
{
	ReleaseDC(m_hWnd, m_hDC);

	DeleteDC(m_memDC); // CreateCompatible로 생성한 DC와 비트맵은 Release가 아닌 Delete를 사용하여 제거해야한다
	DeleteObject(m_hBit);
}

int CCore::init(HWND _hWnd, POINT _ptResolution)
{
	m_hWnd = _hWnd;
	m_ptResolution = _ptResolution;

	// 해상도에 맞게 윈도우 크기 조정
	RECT rt = {0, 0, m_ptResolution.x, m_ptResolution.y};
	AdjustWindowRect(&rt, WS_OVERLAPPEDWINDOW, true);
	SetWindowPos(m_hWnd, nullptr, 100, 100, rt.right - rt.left, rt.bottom - rt.top, 0);

	m_hDC = GetDC(m_hWnd);
	// m_hWnd의 비트맵을 가져와 m_hDC 그리기에 목적지로 삼음

	// 이중 버퍼링 용도의 비트맵과 DC 를 만든다 ( 윈도우를 하나 더 만들면 창이 2개가 생김, 비트맵만 가져오기 )
	m_hBit = CreateCompatibleBitmap(m_hDC, m_ptResolution.x, m_ptResolution.y); // 비트맵 생성
	m_memDC = CreateCompatibleDC(m_hDC); // DC 생성

	HBITMAP hOldBit = (HBITMAP)SelectObject(m_memDC, m_hBit);  // 그림을 그릴 타겟 설정, 원래있던 1픽셀 비트맵 반환
	DeleteObject(hOldBit); // 쓸모없으므로 바로 삭제

	// Manager 초기화
	CTimeMgr::GetInst()->init();
	CKeyMgr::GetInst()->init();

	g_obj.SetPos(Vec2((float)m_ptResolution.x / 2, (float)m_ptResolution.y / 2));
	g_obj.SetScale(Vec2(100, 100));


	return S_OK;
}

void CCore::progress()
{
	// Manager Update
	CTimeMgr::GetInst()->update();

	update();
	render();
}

void CCore::update() // 물체들의 변경점
{
	Vec2 vPos = g_obj.GetPos();

	if (GetAsyncKeyState(VK_LEFT) & 0x8000) // 왼쪽키가 눌림
	{
		vPos.x -= 200.f * CTimeMgr::GetInst()->GetfDT();
	}

	if (GetAsyncKeyState(VK_RIGHT) & 0x8000) // 왼쪽키가 눌림
	{
		vPos.x += 200.f * CTimeMgr::GetInst()->GetfDT();
	}

	g_obj.SetPos(vPos);
}

void CCore::render()
{
	// 화면 clear
	Rectangle(m_memDC, -1, -1, m_ptResolution.x + 1, m_ptResolution.y + 1);

	// 그리기
	Vec2 vPos = g_obj.GetPos();
	Vec2 vScale = g_obj.GetScale();

	Rectangle(m_memDC ,int(vPos.x - vScale.x / 2.f)
					,int(vPos.y - vScale.y / 2.f)
					,int(vPos.x + vScale.x / 2.f)
					,int(vPos.y + vScale.y / 2.f));

	BitBlt(m_hDC, 0, 0, m_ptResolution.x, m_ptResolution.y
		, m_memDC, 0, 0, SRCCOPY);
}
 
```

### 

### CreateCompatibleBitmap

호환 비트맵을 생성하는데 사용되는 함수이다

호환 비트맵이란 화면이나 다른 비트맵에 그리거나 복사하는데 사용되는 비트맵을 말한다



### CreateCompatibleDC

호환 디바이스 컨텍스트(DC)를 생성하는데 사용되는 함수이다

호환 디바이스 컨텍스트는 CreateCompatibleBitmap로 만든 비트맵에 도형 등을 그리기 위해 주로 같이 쓰인다



### SelectObject

비트맵과 DC를 지정해주는 함수이다

반환값으로는 이전에 선택된 객체의 핸들을 반환한다



###  BitBlit

비트맵 데이터를 다른 비트맵으로 복사하는데 사용되는 함수이다



BitBlit 함수를 사용해 복사하는 순간 프레임이 확 떨어짐 -> 윈도우에서 제공해주는 기능(Win32API) 들은 CPU만 사용하기 때문이다

-> 프레임 저하를 해결하는 방법은 GPU를 사용하기 ( Direct 라이브러리가 GPU를 컨트롤 할수 있음 )

-> GPU가 일을 대신 해줌으로써 프레임을 확 높일수 있다