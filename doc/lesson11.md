# Lesson 11: Java Threadds

## Вступление
При помощи команды ps в Linux и при помощи команды tasklist в windows можно вывести список всех процессов, запущенных в ОС на текущий момент.
Например, на Windows можем запросить все процессы Java:
```
tasklist /fi "imagename eq java.exe"
```
У каждого процесса своё так называемое "виртуальное адресное пространство", к которому у процесса есть прямой доступ. Это пространство доступно только процессу, содержит только его данные. Операционная система отвечает за то, каким образом виртуальное адресное пространство процесса проецируется на физическую память.

Один поток (thread) – это одна единица исполнения кода.
Поток — это процесс выполнения инструкций, который работает на выделенном процессоре, выполнение которого контролирует планировщик (scheduler) ОС, и который может быть заблокирован. Потоки создаются внутри процесса и пользуются общими ресурсами. Это означает, что, например, память и декскрипторы файлов, являются общими для всех потоков процесса. Подобный подход принято называть native threads.

Начиная с версии 1.2 Java поддерживает native threads, и с тех пор они используются по умолчанию. До этого использовался другой тип многопоточности, который называется green threads. Green threads — это, по сути, имитация потоков. Виртуальная машина Java берёт на себя заботу о переключении между разными green threads, а сама машина работает как один поток ОС. Но т.к. при green threads вы не можете исполнять два потока одновременно - от такого подхода отказались.
Подробнее: [Обзор моделей работы с потоками](https://habrahabr.ru/post/39543/).

Тот поток, с которого начинается выполнение программы, называется главным. После создания процесса, как правило, JVM начинает выполнение главного потока с метода main(). Затем, по мере необходимости, могут быть запущены дополнительные потоки.

Более детальное описание читать здесь: "[Многопоточность в Java](https://habrahabr.ru/post/164487/)".

В Java есть Планировщик Потоков(Thread Scheduler), который контролирует все запущенные потоки во всех программах и решает, какие потоки должны быть запущены, и какая строка кода выполняться.

Более подробно: [Потоки в Java (java threads)](http://www.quizful.net/post/java-threads).

## Жизненный цикл потока
У каждого потока есть свой жизненный цикл:
![](../img/ThreadLifecycle.png)