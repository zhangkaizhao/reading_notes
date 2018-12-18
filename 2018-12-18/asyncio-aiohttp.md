# asyncio aiohttp

2018-12-18

Source:

* https://pawelmhm.github.io/asyncio/python/aiohttp/2016/04/22/asyncio-aiohttp.html

> So 1k requests take 7 seconds, pretty nice! How about 10k? Trying to make 10k requests unfortunately fails…
>
> ...
>
> That’s bad, seems like I stumbled across [10k connections problem](http://www.webcitation.org/6ICibHuyd).
>
> It says “too many open files”, and probably refers to number of open sockets. Why does it call them files? Sockets are just file descriptors, operating systems limit number of open sockets allowed. How many files are too many? I checked with python resource module and it seems like it’s around 1024. How can we bypass this? Primitive way is just increasing limit of open files. But this is probably not the good way to go. Much better way is just adding some synchronization in your client limiting number of concurrent requests it can process. I’m going to do this by adding [asyncio.Semaphore()](https://docs.python.org/3/library/asyncio-sync.html#asyncio.Semaphore) with max tasks of 1000.
>
> Modified client code looks like this now:
>
> ```python
> # modified fetch function with semaphore
> import random
> import asyncio
> from aiohttp import ClientSession
>
> async def fetch(url, session):
>     async with session.get(url) as response:
>         delay = response.headers.get("DELAY")
>         date = response.headers.get("DATE")
>         print("{}:{} with delay {}".format(date, response.url, delay))
>         return await response.read()
>
>
> async def bound_fetch(sem, url, session):
>     # Getter function with semaphore.
>     async with sem:
>         await fetch(url, session)
>
>
> async def run(r):
>     url = "http://localhost:8080/{}"
>     tasks = []
>     # create instance of Semaphore
>     sem = asyncio.Semaphore(1000)
>
>     # Create client session that will ensure we dont open new connection
>     # per each request.
>     async with ClientSession() as session:
>         for i in range(r):
>             # pass Semaphore and session to every GET request
>             task = asyncio.ensure_future(bound_fetch(sem, url.format(i), session))
>             tasks.append(task)
>
>         responses = asyncio.gather(*tasks)
>         await responses
>
> number = 10000
> loop = asyncio.get_event_loop()
>
> future = asyncio.ensure_future(run(number))
> loop.run_until_complete(future)
> ```
>
> At this point I can process 10k urls. It takes 23 seconds and returns some exceptions but overall it’s pretty nice!

Summary:

* "Primitive way is just increasing limit of open files. But this is probably not the good way to go. Much better way is just adding some synchronization in your client limiting number of concurrent requests it can process. I’m going to do this by adding [asyncio.Semaphore()](https://docs.python.org/3/library/asyncio-sync.html#asyncio.Semaphore) with max tasks of 1000."
