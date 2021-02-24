---
title: Event System
tags:
  - Cpp
  - Game Engine
categories: 游戏引擎开发 (Game Engine Series)
abbrlink: fe6918d5
date: 2021-02-14 17:53:29
banner_img:
index_img:
comment:
translate_title:
top:
---







![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/Eq5wAQ1XMAU2cvz.jpeg)

<div align=center>
  <font size="3">
    <i>
      <a href=" https://twitter.com/m4ndrill">Twitter@m4ndrill</a>
    </i>
  </font>
</div>



### 引言

上一节我们对项目进行重构生成。这节我们将为我们的引擎创建一个事件系统，以便我们处理窗口事件。

<!--more-->



我们希望当我们实际创建一个窗口时，我们可以非常轻松地处理所有事情。以前可能先编写整个窗口系统然后再处理事件，但现在最好是先完成事件系统，当我们编写到窗口时已经可以调度所有事件。

目前我们有一个叫`Application`做应用程序的东西，这意味着它实际上包含了使一切保持运行的循环并且一直不断更新我们的游戏。不仅如此，它还要作为事件的枢纽需要接收事件，最终将它们分派到一个`Layer`层中，现在的游戏层是我们以后会讨论的话题所以不会过多地提及它们，因为我们将为此有单独的章节。总之现在事件最终传播到层以便它们可以处理。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210222152835350.png)

根据我们的应用程序，需要有一个应用程序能够接收事件，所以我们来画一些窗口，然后看看这种交流将如何进行。我们的窗口类代表了我们实际构成的窗口，我们的应用程序就像人们熟知的Windows窗口一样，每次我们在此窗口收到事件时是否有人调整了大小、点击关闭按钮、某种鼠标移动事件等等。无论何时每当这些事情发生时，在我们的窗口库或Win32 API都会收到一个事件，然后一旦该事件发生在该窗口类中，我们需要一种将其传达给应用程序的方式。本质上就是窗口类收到一个事件回调，然后构造一个Infinite事件并以某种方式传播回去。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210222153049788.png)

但我们实际上并不想绑定我们的应用程序到窗口类，所以窗口类不应该知道我们的应用程序。所有的应用程序类都会创建一个窗口，所以我们实际上需要做的是将所有这些事件信息发送给应用程序。

接着我们来谈谈其中的细节。首先是Infinite事件，我们需要一个事件类包含所有对事件系统而言所需的信息。例如鼠标右击，我移动了鼠标并在某个位置单击了它，我们需要什么类型的信息呢？需要确定鼠标点击的X&Y坐标以及哪个按钮被按下，然后我们可以处理该信息，这就是所谓的鼠标按下事件。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210222153938439.png)

我们创建一个鼠标右键事件后，需要一种方法将数据发送到应用程序以便我们后续的操作。我们希望这个应用程序为窗口提供回调，就像一个简单的函数指针一样：当我们由应用程序创建一个窗口时我们还将设置一个回调到该窗口类的事件回调，这样每次此窗口得到一个事件，它可以检查回调是否存在。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210222162405638.png)



窗口实际上并不了解应用程序，但如果我们设置了回调窗口，窗口将以这种方式调用此功能。当接收鼠标按钮按下事件时，我们用堆栈上构造它并立即调用此函数，将来我们可以创建类似缓冲事件的系统。



### Event.h

> Events in Hazel are currently blocking, meaning when an event occurs it
> immediately gets dispatched and must be dealt with right then an there.
> For the future, a better strategy might be to buffer events in an event
> bus and process them during the "event" part of the update stage.



现在的设计方式是没有缓冲的，这类事件不会立刻推迟。之后我们可能会设计为更合理的将事件中的信息推入某种队列或者缓冲，它们会推迟到我们实际经历该事件之前不会立即发生。

首先我们有一个事件类型的枚举类`EventType`拥有不同类型的事件类型，我们将其隔行拆分，包含了按键事件、鼠标事件等等这些内容，这些实际事件在其相关类型的文件中实现，也就是应用程序事件`ApplicationEvent.h`。

```c++
	enum class EventType
	{
		None = 0,
		WindowClose, WindowResize, WindowFocus, WindowLostFocus, WindowMoved,
		AppTick, AppUpdate, AppRender,
		KeyPressed, KeyReleased,
		MouseButtonPressed, MouseButtonReleased, MouseMoved, MouseScrolled
	};
```



将事件分类的原因是因为我们想过滤某些事件，换句话说，从应用程序到某些事件类我正在接收所有的事件，但我只关心键盘事件是否正确。比如一个非常简单的场景，现在我们想记录每个键盘事件或鼠标事件，所以我们必须去检查一下前面的事件：被按下或释放、移动或滚动......

```c++
	enum EventCategory
	{
		None = 0,
		EventCategoryApplication    = BIT(0),
		EventCategoryInput          = BIT(1),
		EventCategoryKeyboard       = BIT(2),
		EventCategoryMouse          = BIT(3),
		EventCategoryMouseButton    = BIT(4)
	};
```

而`BIT(x)`则在`Infinite/Core.h`中定义：

```diff
#pragma once

#ifdef IFN_PLATFORM_WINDOWS
	#ifdef IFN_BUILD_DLL
		#define INFINITE_API _declspec(dllexport)
	#else
		#define INFINITE_API _declspec(dllimport)
	#endif
#else
	#error Infinite only support Windows
#endif
+ #define BIT(x)(1 << x)
```

事件可以分为多个类别，例如`Keyboard`、`Mouse`、`MouseButton`都是`Input`事件、`MouseButton`是`Mouse`事件......而我们想要将多个类别应用与单个事件类型，因此我们需要创建一个位字段以便我们可以设置多个位。



让我们来看一下实际的事件基类

```c++
class HAZEL_API Event
	{
		friend class EventDispatcher;
	public:
		virtual EventType GetEventType() const = 0;
		virtual const char* GetName() const = 0;
		virtual int GetCategoryFlags() const = 0;
		virtual std::string ToString() const { return GetName(); }

		inline bool IsInCategory(EventCategory category)
		{
			return GetCategoryFlags() & category;
		}
	protected:
		bool m_Handled = false;
	};
```





```c++
#pragma once

#include "Hazel/Core.h"

#include <string>
#include <functional>

namespace Hazel {

	// Events in Hazel are currently blocking, meaning when an event occurs it
	// immediately gets dispatched and must be dealt with right then an there.
	// For the future, a better strategy might be to buffer events in an event
	// bus and process them during the "event" part of the update stage.

	enum class EventType
	{
		None = 0,
		WindowClose, WindowResize, WindowFocus, WindowLostFocus, WindowMoved,
		AppTick, AppUpdate, AppRender,
		KeyPressed, KeyReleased,
		MouseButtonPressed, MouseButtonReleased, MouseMoved, MouseScrolled
	};

	enum EventCategory
	{
		None = 0,
		EventCategoryApplication    = BIT(0),
		EventCategoryInput          = BIT(1),
		EventCategoryKeyboard       = BIT(2),
		EventCategoryMouse          = BIT(3),
		EventCategoryMouseButton    = BIT(4)
	};

#define EVENT_CLASS_TYPE(type) static EventType GetStaticType() { return EventType::##type; }\
								virtual EventType GetEventType() const override { return GetStaticType(); }\
								virtual const char* GetName() const override { return #type; }

#define EVENT_CLASS_CATEGORY(category) virtual int GetCategoryFlags() const override { return category; }

	class HAZEL_API Event
	{
		friend class EventDispatcher;
	public:
		virtual EventType GetEventType() const = 0;
		virtual const char* GetName() const = 0;
		virtual int GetCategoryFlags() const = 0;
		virtual std::string ToString() const { return GetName(); }

		inline bool IsInCategory(EventCategory category)
		{
			return GetCategoryFlags() & category;
		}
	protected:
		bool m_Handled = false;
	};

	class EventDispatcher
	{
		template<typename T>
		using EventFn = std::function<bool(T&)>;
	public:
		EventDispatcher(Event& event)
			: m_Event(event)
		{
		}

		template<typename T>
		bool Dispatch(EventFn<T> func)
		{
			if (m_Event.GetEventType() == T::GetStaticType())
			{
				m_Event.m_Handled = func(*(T*)&m_Event);
				return true;
			}
			return false;
		}
	private:
		Event& m_Event;
	};

	inline std::ostream& operator<<(std::ostream& os, const Event& e)
	{
		return os << e.ToString();
	}
}
```







### Application.cpp



