Сборка socket.dll для lua 5.3 (quick 8.3) на mingw-w64:

качаем дистрибутив `https://sourceforge.net/projects/luabinaries/files/5.3.5/Tools Executables/lua-5.3.5_Win64_bin.zip/download` 
кладем содержимое в любое место, например `C:\dev\lua`

качаем исходники, например отсюда `https://sourceforge.net/projects/luabinaries/files/5.3.5/Windows Libraries/Dynamic/lua-5.3.5_Win64_dllw6_lib.zip/download` 
кладем папку include в C:\dev\lua

из `C:\dev\lua`

```CMD
git clone https://github.com/diegonehab/luasocket
```

в `C:\dev\lua\luasocket\src\luasocket.h` и `C:\dev\lua\luasocket\src\luasocket.с` в конце каждого файла правим

```C
LUASOCKET_API int luaopen_socket_core(lua_State *L);
```

на

```C
LUASOCKET_API int luaopen_socket(lua_State *L);
```

`mingw-w64\bin` должен быть в PATH из `C:\dev\lua\luasocket\src` вызываем

```CMD
mingw32-make PLAT=mingw LUAV=5.3 LUAINC_mingw="C:\dev\lua\include" LUALIB_mingw="C:\dev\lua\lua53.dll" all
```

```CMD
move "socket-3.0-rc1.dll" ..\..\socket.dll && move "mime-1.0.3.dll" ..\..\
```

теперь в `C:\dev\lua` есть `socket.dll` и он подключается через `require "socket"`

