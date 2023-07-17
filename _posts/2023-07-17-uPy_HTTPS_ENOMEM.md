---
layout: post
title: ENOMEM when using urequests on MicroPython
---

# ENOMEM when using urequests on MicroPython

If you're making https requests with the MicroPython `requests` module, you might encounter ENOMEM errors. For me, they appeared after every 2nd request to a different HTTPS endpoint - 
first endpoint request would always succeed. Weird stuff. Anyway, go get your own copy of the `requests` library from the MicroPython repo, and find where the `requests` function is returning
a Request object. [Library download link here](https://raw.githubusercontent.com/micropython/micropython-lib/master/python-ecosys/urequests/urequests.py)

You'll notice that, before it, there are a bunch of error cases, and the socket is closed in case of those. In case of a successful HTTP response, however, the socket is not closed.

Close it.

```python
        resp = Response(s)
        resp.status_code = status
        resp.reason = reason
        if resp_d is not None:
            resp.headers = resp_d
        + s.close()
        return resp
```

I have no idea what the side effects are - my device is a throwie, it will reset itself if the code fails. I do know that this made the ENOMEM error disappear.

After modifying this, upload this onto your device, and make sure that it is called instead of the builtin - I named my lib `urequests.py` and did `import urequests`. gl.

If you think that this is bad advice, contact me somehow and let me know. Cheers!
