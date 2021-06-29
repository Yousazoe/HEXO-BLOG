---
title: Window Events
comment: false
abbrlink: 1bc324b9
date: 2021-05-27 20:49:05
type:
tags:
  - Cpp
  - Game Engine
categories: 游戏引擎开发 (Game Engine Series)
banner_img:
index_img:
translate_title:
top:
mathjax:
---

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/77cbdc61408483.5a9276f541b0d.png)

<div align=center>
  <font size="3">
    <i>
      <a href="https://www.behance.net/gallery/61408483/Memories">Memories</a> by 
      <a href="https://www.behance.net/MChahin">Mohamed Chahin</a>
    </i>
  </font>
</div>



### 引言

上一节为我们的游戏引擎创建了一个窗口，讨论了很多抽象类以及我们如何才能真正抽象出真正的窗口逻辑API，而今天我们将通过该窗口实际添加事件。

<!--more-->





窗口会随时生成事件，我们移动鼠标、按一个键、关闭窗口、调整窗口大小、单击鼠标按键......所有这些都会生成事件，事件发生在我们的窗口内，我们想创建一个事件并分发出去。现在我们实际上迫切需要的例子是关闭，现在当我们点击关闭按钮时程序什么也不会发生，只是我们单击它，而我们想正确的终止程序。

所以今天我们将要实施的功能是调度所有不同的事件类型，例如按键事件、鼠标事件、窗口调整事件等等。



### 事件回调

为了能够在窗口上设置回调函数，所以在窗口内部编写的是之前在抽象窗口`Window.h`中的事件回调函数：一个返回`void`并接收事件引用的函数：

```c++
using EventCallbackFn = std::fuction<void(Event&)>;
```



在`Application.h`中我们声明一个称为`OnEvent(Event& e)`的函数：

```diff
#include "Core.h"
#include "Events/Event.h"
#include "Events/ApplicationEvent.h"
#include "Window.h"

namespace Infinite {
		virtual ~Application();

		void Run();
+		void OnEvent(Event& e);
	private:
		std::unique_ptr<Window> m_Window;
		bool m_Running = true;
	};
```





接着返回`Application.cpp`中实现`OnEvent(Event& e)`函数。我们可以通过标准库中的`bind`实现，它将绑定应用程序事件，回调事件回调进入这个窗口数据结构`EventCallbackFn EventCallback`，这里我们用宏：

```diff
#include "ifnpch.h"
#include "Application.h"
#include "Events/ApplicationEvent.h"
#include "Log.h"
#include <GLFW/glfw3.h>

namespace Infinite {

+#define BIND_EVENT_FN(x) std::bind(&Application::x, this, std::placeholders::_1)

	Application::Application() 
	{
		m_Window = std::unique_ptr<Window>(Window::Create());
+		m_Window->SetEventCallback(BIND_EVENT_FN(OnEvent));
	}

	Application::~Application() {}

+	void Application::OnEvent(Event& e)
+ {
+		IFN_CORE_TRACE("{0}", e);
+ }

	void Application::Run() 
	{
		while (m_Running)
		{
			glClearColor(1, 0, 1, 1);
			glClear(GL_COLOR_BUFFER_BIT);
			m_Window->OnUpdate();
		}
	}
}
```



这里需要注意`OnEvent()`函数前面别忘记加`Application::`，函数体内用之前的日志系统打印事件类型和详细信息。

正如刚才所说，我们将从`GLFW`中获取一些回调，因此我们在`WindowsWindow.cpp`中的`Init()`加入注释：`//Set GLFW callbacks`，之后的代码都在这个位置添加：

```c++
void WindowsWindow::Init(const WindowProps& props)
{
		m_Data.Title = props.Title;
		m_Data.Width = props.Width;
		m_Data.Height = props.Height;
		IFN_CORE_INFO("Creating window {0} ({1}, {2})", props.Title, props.Width, props.Height);
		if (!s_GLFWInitialized)
		{
			// TODO: glfwTerminate on system shutdown
			int success = glfwInit();
			IFN_CORE_ASSERT(success, "Could not intialize GLFW!");

            glfwSetErrorCallback(GLFWErrorCallback);
			s_GLFWInitialized = true;
		}

		m_Window = glfwCreateWindow((int)props.Width, (int)props.Height, m_Data.Title.c_str(), nullptr, nullptr);
		glfwMakeContextCurrent(m_Window);
		glfwSetWindowUserPointer(m_Window, &m_Data);
		SetVSync(true);

		// Set GLFW callbacks
		.........
```



需要注意引入事件类相关的头文件：

```diff
#include "ifnpch.h"
#include "WindowsWindow.h"

+#include "Events/ApplicationEvent.h"
+#include "Events/MouseEvent.h"
+#include "Events/KeyEvent.h"

namespace Infinite {
}
```





### 更改窗口大小

我们首先来编写窗口大小调整的回调，使用lambda去到`glfwSetWindowSizeCallback()`这个函数。实际的窗口大小很有趣，三个参数分别是窗口和两个窗口长宽整数：

```c++
/*
 *  @param[in] window The window that was resized.
 *  @param[in] width The new width, in screen coordinates, of the window.
 *  @param[in] height The new height, in screen coordinates, of the window.
 */
typedef void (* GLFWwindowsizefun)(GLFWwindow*,int,int)
```



那么我们可以在此处编写实际的实现，把更新后的长度和宽度返给`data`并创建窗口大小调整事件：

```c++
// Set GLFW callbacks
glfwSetWindowSizeCallback(m_Window,[](GLFWwindow* window,int width,int height)
{
		WindowData& data = *(WindowData*)glfwGetWindowUserPointer(window);
		data.Width = width;
		data.Height = height;

		WindowResizeEvent event(width,height);
		data.EventCallback(event);
});
```



### 关闭窗口

```c++
typedef void (*GLFWwindowclosefun)(GLFWwindow*)
```



前面是一样的，真正需要做的是创建窗口关闭事件然后分派它：

```c++
glfwSetWindowCloseCallback(m_Window, [](GLFWwindow* window)
{
    WindowData& data = *(WindowData*)glfwGetWindowUserPointer(window);

    WindowCloseEvent event;
    data.EventCallback(event);
});
```





### 按键事件

```c++
typedef void (*GLFWkeyfun)(GLFWwindow*,int,int,int,int)
```



`GLFW`为我们提供了不同的行为，我们用`switch`区分：

+ `GLFW_PRESS`：按下按键
+ `GLFW_RELEASE`：松开按键
+ `GLFW_REPEAT`：连击按键

```c++
glfwSetKeyCallback(m_Window,[](GLFWwindow* window,int key,int scancode,int action,int mods){
	WindowData& data = *(WindowData*)glfwGetWindowUserPointer(window);

  switch (action) {
    case GLFW_PRESS:
      {
        KeyPressedEvent event(key,0);
        data.EventCallback(event);
        break;
      }

    case GLFW_RELEASE:
      {
        KeyReleasedEvent event(key);
        data.EventCallback(event);
        break;
      }

    case GLFW_REPEAT:
      {
        KeyPressedEvent event(key,1);
        data.EventCallback(event);
        break;
      }
  }
});
```



### 鼠标点击

```c++
typedef void (* GLFWmousebuttonfun)(GLFWwindow*,int,int,int);
```





```c++
glfwSetMouseButtonCallback(m_Window, [](GLFWwindow* window, int button, int action, int mods){
			WindowData& data = *(WindowData*)glfwGetWindowUserPointer(window);
			switch (action) {
			    case GLFW_PRESS:
			    {
				    MouseButtonPressedEvent event(button);
				    data.EventCallback(event);
				    break;
			    }

			    case GLFW_RELEASE:
			    {
				    MouseButtonReleasedEvent event(button);
				    data.EventCallback(event);
				    break;
			    }
			}
		});
```





### 鼠标滚轮

```c++
typedef void (* GLFWmousebuttonfun)(GLFWwindow*,int,int,int);
```







```c++
glfwSetScrollCallback(m_Window,[](GLFWwindow* window,double xOffset,double yOffset){
  WindowData& data = *(WindowData*)glfwGetWindowUserPointer(window);

  MouseScrolledEvent event((float)xOffset,(float)yOffset);
  data.EventCallback(event);
});
```





### 鼠标位置

```c++
typedef void (* GLFWcursorposfun)(GLFWwindow*,double,double);
```





```c++
glfwSetCursorPosCallback(m_Window,[](GLFWwindow* window,double xPos,double yPos){
  WindowData& data = *(WindowData*)glfwGetWindowUserPointer(window);

  MouseMovedEvent event((float)xPos,(float)yPos);
  data.EventCallback(event);
});
```



### GLFW报错

在`WindowsWindow.cpp`中加入`GLFW`报错的回调，打印报错信息：

```diff
namespace Infinite {

	static bool s_GLFWInitialized = false;
+	static void GLFWErrorCallback(int error,const char* description)
+	{
+		IFN_CORE_ERROR("GLFW Error ({0}): {1}",error,description);
+	}

	......
	
	WindowsWindow::WindowsWindow(const WindowProps& props)
	{
		Init(props);
	}
	WindowsWindow::~WindowsWindow()
	{
		Shutdown();
	}
	void WindowsWindow::Init(const WindowProps& props)
	{
		......
		if (!s_GLFWInitialized)
		{
			// TODO: glfwTerminate on system shutdown
			int success = glfwInit();
			IFN_CORE_ASSERT(success, "Could not intialize GLFW!");

+     glfwSetErrorCallback(GLFWErrorCallback);
			s_GLFWInitialized = true;
		}

		......
}
```





回到`Application.h`，声明`OnWindowClose()`窗口关闭函数：

```diff
#include "Core.h"
#include "Events/Event.h"
#include "Events/ApplicationEvent.h"
#include "Window.h"

namespace Infinite {
		virtual ~Application();

		void Run();
		void OnEvent(Event& e);
	private:
+		bool OnWindowClose(WindowCloseEvent& e);

		std::unique_ptr<Window> m_Window;
		bool m_Running = true;
	};
```



接着在`Application.cpp`中实现：

```diff
#include "ifnpch.h"
#include "Application.h"
#include "Events/ApplicationEvent.h"
#include "Log.h"
#include <GLFW/glfw3.h>

namespace Infinite {

#define BIND_EVENT_FN(x) std::bind(&Application::x, this, std::placeholders::_1)

	Application::Application() 
	{
		m_Window = std::unique_ptr<Window>(Window::Create());
		m_Window->SetEventCallback(BIND_EVENT_FN(OnEvent));
	}

	Application::~Application() {}

	void Application::Run() {
	void Application::OnEvent(Event& e)
    {
+		EventDispatcher dispatcher(e);
+		dispatcher.Dispatch<WindowCloseEvent>(BIND_EVENT_FN(OnWindowClose));

		IFN_CORE_TRACE("{0}", e);
    }

	void Application::Run() 
	{
		while (m_Running)
		{
			glClearColor(1, 0, 1, 1);
			glClear(GL_COLOR_BUFFER_BIT);
			m_Window->OnUpdate();
		}
	}

+	bool Application::OnWindowClose(WindowCloseEvent& e)
+	{
+		m_Running = false;
+		return true;
+	}

}
```







### 调试

如果报错请注意作用域（我一开始报错是因为`OnEvent()`）和头文件（部分需要引用事件类头文件）引用即可，下面是运行引擎事件回调测试：



#### 鼠标移动事件

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210528195818356.png)



#### 按键事件

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210528195841358.png)



#### 窗口大小调整事件

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210528195857882.png)



#### 窗口关闭事件

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210528195913808.png)



可以看到现在我们能够成功监测引擎应用程序额窗口事件，并在控制台打印信息出来。
