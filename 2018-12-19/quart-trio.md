# Quart-Trio

2018-12-19

Source:

* https://medium.com/@pgjones/quart-trio-9415d7c1928a

> What makes Trio special though is its focus on the API. Trio is easier to understand, especially when compared with asyncio. This means that any applications built with Quart-Trio will be simpler and better reasoned.
>
> ## A real example
>
> I’ve prepared a [simple chat application](https://github.com/pgjones/trio_quart_article) to demonstrate how to use Quart-Trio, the key to this example is this function,
>
> ```python
> @app.websocket("/ws")
> async def chat():
>     try:
>         connections.add(websocket._get_current_object())
>         async with trio.open_nursery() as nursery:
>             nursery.start_soon(heartbeat)
>             while True:
>                 message = await websocket.receive()
>                 await broadcast(message)
>     finally:
>         connections.remove(websocket._get_current_object())
> ```
>
> This is a very succinct way to create a background task (the heartbeat) with confidence that it will cancelled when the connection is closed. In addition any exception raised in the background task will also trigger the finally clause as you’d expect. This is a non-trivial exercise with asyncio.
