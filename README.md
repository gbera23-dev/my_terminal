# my_terminal

A small interactive **shell written in C**, built to practice systems programming and data-structure implementation.

## Features

- Runs external programs through `fork` + `execvp`
- **String binding** with the backtick character so arguments can contain spaces
- **LRU cache** of previously entered commands
- **Dynamic dispatch table** for built-in commands (open/closed: new commands are just registered, with no `if`/`else` chain)
- Custom generic **hash map** (with dynamic resizing) backing the dispatcher, with `int` and `string` key implementations

## Built-in commands

`EXIT`, `UP`, `FULL`, `CHECK`, `CURRDIR`, `CHDIR`, `MAKEDIR`, `RMDIR`, `GETTIME`, plus two joke commands: `SPAWNMEESEEKS` and `ANSWER_TO_ULTIMATE_QUESTION`.

## Layout

```
main.c                          # read-eval loop, tokenizer, process execution
dyn_dispatcher/                 # command registry and dispatcher
dyn_dispatcher/special_functions/   # built-in command implementations
hashmap/                        # generic hash map (+ type_impls/intmap, strmap)
lru_cache/                      # doubly linked list LRU command history
```

## Build and run

```bash
gcc main.c dyn_dispatcher/dyn_dispatcher.c dyn_dispatcher/special_functions/functions.c \
    hashmap/hashmap.c hashmap/type_impls/*.c lru_cache/lru_cache.c -o my_terminal
./my_terminal
```

Linux/POSIX required. Related project: `my_server` serves this shell over TCP.
