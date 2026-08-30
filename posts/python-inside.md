---
title: "Inside Python"
date: 2022-07-08
tags: [python]
description: "Exploring inner working of python"
publish: true
---

# Exploring Python
Being a embedded programmer and dealing with low level C I want to explore 
how C and python interact. This will provide inside on how various c and C++
libraries are used by python to provide dynamic programming environment.

It helps to understand how we can prototype software in python and convert
to C once verified and tested.

## Python libraries and modules 

### ctypes
Most of the python bindings are provided by using this module as gateway
to send receive data from dll in windows or shared library in linux.

This is most used module when interfacing C api with python. I observed that
for most of the time python provide dynamic environment around DLL or shared
libraries. I mean its not pure python code when we python provide some
kind device driver support.

Exploring the code for kvaser interface provided by [python-can](https://python-can.readthedocs.io)
and similar modules I observed below pattern

1. Load the DLL.
2. Get handle to functions or interfaces.
3. Using ctypes to create inputs to functions from python data types.
4. Call the function
5. Convert back return value from c dll functions to python.

#### Exploring kvaser bus interface
##### Loading DLL using *LoadLibrary* 

```
try:
  if sys.platform == "win32":
    __canlib = ctypes.windll.LoadLibrary("canlib32")
  else:
    __canlib = ctypes.cdll.LoadLibrary("libcanlib.so")
   
  log.info("Loaded kvaser can library")
expect OSError:
  log.warning("Kvaser can lib unavialble")
  __canlib = None

```

##### Get handle to function interfaces
Below is a common function defined to get handle to c library function.

```
def __get_canlib_function(func_name , argtypes = None, restype=None, errcheck=None):
  argtypes = [] if argtypes is None else argtypes
  
  try:
    retval = getattr(__canlib, func_name)
  expect AttributeError:
    log.warning("%s function not found in libarary", func_name)
    return _unimplemented_function
  else:
    retval.argtypes = argtypes
    retval.restype = restype

    if errcheck:
      retval.errcheck = errcheck

   return retval

```

#####  Using ctype to create input parameters

Above function *__get_canlib_function* is called like for example *canWrite*
```
canWrite = __get_canlib_function(
                "canWrite",
                argtypes = [
                c_canHandle,
                ctypes.c_long,
                ctypes.c_void_p,
                ctypes.c_uint,
                ctypes.c_uint,
                ],
                restype=canstat.c_canStatus,
                errcheck=__check_status_operartion,)
```

Here *c_canHandle* is empty class like and canstat is simple constant defined in
constant.py file.

```
class c_canHandle(ctypes.c_int):
  pass
```

Comparing this with kvaser canlib function prototype we see how ctypes
are used to map data types from python to c.

```
canStatus canWrite(const int hnd,
                  long id,
                  void * msg,
                  unsigned int dlc,
                  unsigned int flag
                  )
```

##### Call the function
*Send* function uses the canWrite function handle as shown below

Except int , byte and string all other parameters are converted to
ctypes.

```
def send(self,msg,timeout=None):
  flags = canstat.canMSG_EXT if msg.is_extended_id else canstat.canMSG_STD

  if msg.is_remote_frame:
    flags = canstat.canMSG_RTR
  if msg.is_error_frame:
    flags = canstat.canMSG_ERROR_FRAME
  if msg.is_fd:
    flags = canstat.canFDMSG_FDF
  if msg.bitrate_switch:
    flags = canstat.canFDMSG_BRS

  ArrayConstructor = ctypes.c_byte * msg.dlc 
  buf = ArrayConstructor(*msg.data)

  canWrite(self.c_canHandle,msg.arbitration_id,ctypes.byteref(buf),msg.dlc,flags)
  
```

##### Convert back return value from c dll functions to python.
In this case *send* function is ignoring return.
