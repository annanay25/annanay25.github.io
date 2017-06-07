## Why you should be using screen

Very few developers use the ```screen``` utility that is available in all *nix systems

- Screen will persist even if you have a network outage!
- Mitigate the problem of having multiple ssh sessions!
- Name your sessions according to work and create away!

#### Cheat sheet:

```Ctrl-A + Ctrl-D ``` - Detach  
```Ctrl-A + Esc ``` - Copy mode / Scroll 

```
screen -S <new-screen-name>  
screen -r <screen-name>  
screen -rd <screen-name>  
```

To enter command mode -
```
Ctrl-A + Esc 

: srollback 99999
```

