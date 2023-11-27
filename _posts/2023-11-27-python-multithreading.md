---
layout: post
title: Python MultiThreading은 효과적인가?
subtitle: I/O Bound Tasks에는 쓸만한 MultiThreading!
tags: [Python, Dev]
categories : [Python]
---

### 네트워크 스캔 작업에 MultiThreading을 사용해도 효과적인 지 궁금할 땐 ChatGPT에게 문의하기

Python은 GIL로 인해 멀티스레드 보다는 멀티프로세싱이 성능면에서 더 좋다고 한다. 실제로 멀티프로세스와 멀티스레드를 스크립트로 구현하여 테스트했을 때, 멀티스레드 성능이 프로세스만큼 좋진 않았다.<br>
오히려 단일 스레드보다 다중 스레드가 더 작업 시간이 오래 걸리는 걸 볼 수 있었다. 이는 아마도 스레드끼리 queue를 공유하면서 Context Switching이 발생되었기 때문이다.

그렇담 파이썬에서 멀티스레드는 정말 필요없는 것일까?
이를 확인하기위해서 ChatGPT에 물어보니, I/O Bound한 작업에서는 효과가 있을 것이라는 답변을 받았다.

I/O Bound한 작업이란 결국 응답을 기다리는 작업.. 그렇담 네트워크 패킷 전송테스트를 해보고 그 결과를 확인해봐야겠다.

In Python, the `Global Interpreter Lock (GIL)` significantly impacts the effectiveness of multithreading for CPU-bound tasks. The GIL is a mechanism used in CPython (the reference implementation of Python) to synchronize access to Python objects, preventing multiple native threads from executing Python bytecodes at once. This means that, in CPython, only one thread can execute Python bytecode at a time, even on multi-core systems.

However, multithreading in Python can still be effective for certain types of tasks, especially those that are I/O-bound or benefit from parallelism due to external factors (such as waiting for responses from multiple servers). In I/O-bound scenarios, the GIL is less of a limiting factor because threads can release the GIL while waiting for I/O operations to complete.

Here are some considerations:

I/O-Bound Tasks:
Multithreading can be effective for I/O-bound tasks, where the program spends a significant amount of time waiting for external resources like file I/O, network requests, or database queries. In such cases, the GIL is less of a bottleneck, and the concurrent execution of I/O operations by multiple threads can lead to performance improvements.

CPU-Bound Tasks:
For CPU-bound tasks that require intensive computation and don't involve much I/O, using multiprocessing or asynchronous programming might be more effective than multithreading. Multiprocessing allows separate Python processes to run in parallel, bypassing the GIL limitation. Additionally, asynchronous programming with asyncio can be used to achieve concurrency without relying on threads.

Alternatives:
Multiprocessing:

If you have CPU-bound tasks, consider using the multiprocessing module. Each process runs in its own interpreter and has its own GIL, allowing true parallelism.

```
from multiprocessing import Pool


def cpu_bound_task(x):
    # Some CPU-bound task
    return x * x

if __name__ == "__main__":
    with Pool() as pool:
        result = pool.map(cpu_bound_task, [1, 2, 3, 4, 5])
        print(result)
```
Asynchronous Programming:

Asynchronous programming using asyncio can be effective for I/O-bound tasks, allowing you to write asynchronous code without relying on threads.

```
import asyncio

async def io_bound_task():
    # Some I/O-bound task
    await asyncio.sleep(1)
    return "Done"

async def main():
    tasks = [io_bound_task() for _ in range(5)]
    results = await asyncio.gather(*tasks)
    print(results)

asyncio.run(main())

```
In summary, while multithreading in Python may not be as effective for CPU-bound tasks due to the GIL, it can still be useful for certain scenarios, especially those involving I/O-bound operations. For CPU-bound tasks, consider using multiprocessing or asynchronous programming depending on your specific requirements.