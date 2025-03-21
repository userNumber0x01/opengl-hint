# GLFW

> %%отображение ctrl+shift+v%%

## Инициализация, создание, управление окнами

- `glfw.init()` - проверка на поддержку GLFW и подготовка переменных среды.
- `glfw.create_window(width, height, title, monitor, share)` - создание окна.
  - **width** - ширина.
  - **height** - высота.
  - **title** - заголовок.
  - **monitor** (glfw.Monitor) - указатель на объект монитора (создание полноэкранного окна), `None` - оконный режим.
  - **share** (glfw.Window) - указатель на другое окно, с которым вы хотите разделить контекст OpenGL. `None` - новый контекст.
- `glfw.make_context_current(window)` - установка указанного окна в качестве текущего контекста OpenGL.
- `glfw.terminate()` - высвобождение всех ресурсов, завершение работы.
- `glfw.window_should_close(window)` - (true, false) Проверяет, было ли запрошено закрытие окна.
- `glfw.set_window_should_close(window, value)` - `value`=(true, false) Устанавливает флаг, указывающий, должно ли окно закрываться.
- `glfw.swap_buffers(window)` - содержимое заднего буфера (где вы рисуете) становится видимым на экране, а передний буфер (который отображается) становится задним буфером для следующей отрисовки.

## Обработка событий

- `glfw.poll_events()` - (не блокирует программу) библиотека обрабатывает все события, которые произошли с момента последнего вызова этой функции.
- `glfw.wait_events()` — функция, которая приостанавливает выполнение программы до тех пор, пока не произойдет одно из событий, связанных с окном, таких как нажатие клавиш, движение мыши, изменение размера окна и т.д.
- `glfw.wait_events_timeout(timeout)` - блокирует выполнение программы до тех пор, пока не произойдет событие или не истечет заданный таймаут.
- `glfw.get_time()` — возвращает (float) текущее время в секундах с момента инициализации библиотеки.

## Управление вводом

- `glfw.get_key(window, key)` - Возвращает состояние клавиши (нажата, отпущена и т.д.) для указанного окна.
  - **key**: Код клавиши, например `glfw.KEY_A`.
  - **return**: 
    - `glfw.RELEASE`: Клавиша не нажата.
    - `glfw.PRESS`: Клавиша нажата.
    - `glfw.REPEAT`: Клавиша нажата и удерживается (при этом она будет возвращать `glfw.REPEAT`, если она удерживается после первого нажатия).
- `glfw.get_mouse_button(window, button)` - Возвращает состояние кнопки мыши для указанного окна.
  - **button**: код клавиши, например `glfw.MOUSE_BUTTON_LEFT`
    - `glfw.RELEASE`: Кнопка не нажата.
    - `glfw.PRESS`: Кнопка нажата.
- `glfw.get_cursor_pos(window)` - Возвращает текущую позицию курсора мыши в окне.
  - **return**: (x,y)
- `glfw.set_cursor_pos(window, xpos, ypos)` - Устанавливает позицию курсора мыши в окне.
## Настройка параметров окна
- `glfw.window_hint(hint, value)` - Устанавливает параметры для создания окна, такие как возможность изменения размера, количество буферов и т.д. Эти параметры должны быть установлены перед вызовом `glfw.create_window()`.
  - `glfw.window_hint(glfw.RESIZABLE, glfw.TRUE)` - `glfw.RESIZABLE`: Указывает, может ли окно изменять размер `glfw.TRUE`,`glfw.FALSE`
  - `glfw.window_hint(glfw.VISIBLE, glfw.FALSE)` - `glfw.VISIBLE`: Указывает, будет ли окно видимым при создании. Значение `glfw.FALSE` делает окно невидимым до тех пор, пока вы не сделаете его видимым вручную.
## Работа с мониторами
- `glfw.get_monitors()` - Возвращает список всех доступных мониторов. (список указателей на объекты мониторов.) или None
- `glfw.get_primary_monitor()` - Возвращает основной монитор. (указатель на основной монитор.) или None
## Работа с контекстами
- `glfw.make_context_current(window)` - Устанавливает указанный контекст окна как текущий.
  - **window**: Указатель на окно, для которого вы хотите установить контекст OpenGL.
- `glfw.swap_interval(interval)` - Устанавливает интервал вертикальной синхронизации (V-Sync) для текущего контекста OpenGL.
  - **interval**: 0 - без синхронизации; 1 - синхронизация с частотой обновления экрана; 2 и более - Обмен буферов происходит каждые N кадров, где N — значение интервала.

# OpenGL

- `glClear(GLbitfield mask)` - для очистки указанных буферов, таких как цветовой буфер, буфер глубины и буфер трафарета.
  - **mask (GLbitfield)**: Маска, указывающая, какие буферы должны быть очищены.
    - **GL_COLOR_BUFFER_BIT**: Очищает цветовой буфер.
    - **GL_DEPTH_BUFFER_BIT**: Очищает буфер глубины.
    - **GL_STENCIL_BUFFER_BIT**: Очищает буфер трафарета.
- `glClearColor(GLfloat red, GLfloat green, GLfloat blue, GLfloat alpha)` - используется для установки цвета, которым будет очищен цветовой буфер при вызове функции `glClear()`
  - **red**: 0.0 - 1.0
  - **green**: 0.0 - 1.0
  - **blue**: 0.0 - 1.0
  - **alpha**: 0.0 - 1.0
- `glFlush()` - используется для принудительного выполнения всех ранее вызванных команд OpenGL.
## Координаты
- `glOrtho(GLdouble left, GLdouble right, GLdouble bottom, GLdouble top, GLdouble near, GLdouble far)`, определяет координатную систему, на которую полагается OpenGL при отрисовке финального изображения и проецировании изображения на экран.Все объекты, находящиеся в пределах указанных границ (left, right, bottom, top) и между ближней и дальней плоскостями (near и far), будут отображаться на экране.
  - **left** - Координата левой границы проекции.
  - **right** - Координата правой границы проекции.
  - **bottom** - Координата нижней границы проекции.
  - **top** - Координата верхней границы проекции.
  - **near** - Координата ближней плоскости отсечения.
  - **far** - Координата дальней плоскости отсечения.

## Окно

- `glViewport(GLint x, GLint y, GLsizei width, GLsizei height)` - определяет область окна, в которую будет выводиться изображение. 
  - **x**: Положение по оси X (в пикселях) в окне, где начинается область просмотра. Значение 0 соответствует левому краю окна.
  - **y**: Положение по оси Y (в пикселях) в окне, где начинается область просмотра. Значение 0 соответствует нижнему краю окна. в OpenGL координаты Y увеличиваются вверх.
  - **width**: Ширина области просмотра в пикселях.
  - **height**: Высота области просмотра в пикселях.

- `glMatrixMode(GLenum mode)` - устанавливает текущую матрицу для последующих операций с матрицами. 
  - **mode**: Указывает, какую матрицу вы хотите установить как текущую. Возможные значения:
    - **GL_MODELVIEW**: Устанавливает модельно-вью матрицу, которая используется для трансформации объектов в сцене и для определения положения камеры.
    - **GL_PROJECTION**: Устанавливает проекционную матрицу, которая определяет, как 3D-сцена проецируется на 2D-экран. Это может быть перспектива или ортографическая проекция.
    - **GL_TEXTURE**: Устанавливает матрицу текстуры, которая используется для трансформации текстурных координат.

- `glLoadIdentity(void)` - сбрасывает текущую матрицу к единичной матрице.Единичная матрица — это матрица, которая не вносит изменений в вектор, когда применяется к нему.



## Отрисовка объектов

- `glBegin(GLenum mode)` - это функция в OpenGL, которая используется для начала определения примитивов, таких как точки, линии и полигоны. 
  - **mode**
    - **GL_POINTS**: Рисует точки.
    - **GL_LINES**: Рисует линии между парами вершин.
    - **GL_LINE_LOOP**: Рисует замкнутый контур линий.
    - **GL_LINE_STRIP**: Рисует последовательность соединенных линий.
    - **GL_TRIANGLES**: Рисует треугольники, где каждые три вершины образуют один треугольник.
    - **GL_TRIANGLE_STRIP**: Рисует последовательность треугольников, где каждая новая вершина добавляет новый треугольник.
    - **GL_TRIANGLE_FAN**: Рисует треугольники, исходящие из одной центральной вершины.
    - **GL_QUADS**: Рисует четырехугольники, где каждые четыре вершины образуют один четырехугольник.
    - **GL_QUAD_STRIP**: Рисует последовательность четырехугольников.

- `glVertex*()` — это набор функций в OpenGL, используемых для определения вершин в процессе рендеринга.
  - **`glVertex2f(GLfloat x, GLfloat y)`**: Определяет 2D-вершину с плавающей точкой.
  - **`glVertex2i(GLint x, GLint y)`**: Определяет 2D-вершину с целыми числами.
  - **`glVertex3f(GLfloat x, GLfloat y, GLfloat z)`**: Определяет 3D-вершину с плавающей точкой.
  - **`glVertex3i(GLint x, GLint y, GLint z)`**: Определяет 3D-вершину с целыми числами.
  - **`glVertex4f(GLfloat x, GLfloat y, GLfloat z, GLfloat w)`**: Определяет 4D-вершину с плавающей точкой (используется для гомогенных координат).

- `glTexCoord*()` — это набор функций в OpenGL, используемых для задания текстурных координат вершин.
  - **`glTexCoord1f(GLfloat s)`**: Задает текстурную координату в 1D (одномерную).
  - **`glTexCoord2f(GLfloat s, GLfloat t)`**: Задает текстурные координаты в 2D (двумерные).
  - **`glTexCoord3f(GLfloat s, GLfloat t, GLfloat r)`**: Задает текстурные координаты в 3D (трехмерные).
  - **`glTexCoord4f(GLfloat s, GLfloat t, GLfloat r, GLfloat q)`**: Задает текстурные координаты в 4D (четырехмерные). 

- `glNormal*()` — это набор функций в OpenGL, используемых для задания нормалей вершин. 
  - **`glNormal3f(GLfloat nx, GLfloat ny, GLfloat nz)`**: Задает нормаль в 3D-пространстве с плавающей точкой.
  - **`glNormal3d(GLdouble nx, GLdouble ny, GLdouble nz)`**: Задает нормаль в 3D-пространстве с двойной точностью.
  - **`glNormal3i(GLint nx, GLint ny, GLint nz)`**: Задает нормаль в 3D-пространстве с целыми числами.

- `glEnd(void)` — это функция в OpenGL, которая используется для завершения определения примитивов, начатого с помощью функции `glBegin()`

## Машина состояния, state machine

- `glEnable(GLenum cap)` - используется для включения различных возможностей рендеринга. 
  - **cap**
    - **GL_DEPTH_TEST**: Включает тест глубины.
    - **GL_BLEND**: Включает смешивание (блендинг).
    - **GL_CULL_FACE**: Включает отсечение (culling) лиц.
    - **GL_LIGHTING**: Включает освещение.

- `glGetBooleanv(GLenum pname, GLboolean *data)` - используется для получения значения параметров состояния, хранящихся в виде логических значений (true/false). 
  - **name:** 
  - **GL_DEPTH_TEST:** возвращает, включен ли тест глубины.
  - **GL_CULL_FACE:** возвращает, включен ли отсечение.
  - **GL_BLEND:** возвращает, включено ли смешивание.

- `glDisable(GLenum cap)` - используется для отключения определенных возможностей рендеринга. 
  - **cap:**
  - **GL_DEPTH_TEST:** отключает тест глубины.
  - **GL_CULL_FACE:** отключает отсечение (culling) полигонов.
  - **GL_BLEND:** отключает смешивание (blending) цветов.
  - **GL_LIGHTING:** отключает освещение.
  - **GL_TEXTURE_2D:** отключает 2D текстурирование.
