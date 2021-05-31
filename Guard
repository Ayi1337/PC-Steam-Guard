import hmac
import hashlib
from base64 import b64decode
from time import time,sleep
import struct
from tkinter import *

def get_steam_auth_code(secret: str, t: int = None) -> str:
    if not t:
        t = int(time()/30)
    msg = struct.pack(">Q", t)
    key = b64decode(secret)
    mac = hmac.new(key, msg, hashlib.sha1).digest()
    offset = mac[-1] & 0x0f
    binary = struct.unpack('>L', mac[offset:offset+4])[0] & 0x7fffffff
    codestr = list('23456789BCDFGHJKMNPQRTVWXY')
    chars = []
    for _ in range(5):
        chars.append(codestr[binary % 26])
        binary //= 26
    code = ''.join(chars)
    return code

#print(get_steam_auth_code('',))
grad=get_steam_auth_code('Steam secret key Here',)
r = Tk()
r.withdraw()
r.clipboard_clear()
r.clipboard_append(grad)
r.update()
sleep(.2)
r.update()
r.destroy()
