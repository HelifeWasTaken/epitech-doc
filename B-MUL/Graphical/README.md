# The Graphical Side of the B-MUL

## Prerequirities

Make sure that you understand malloc that you know how to do a NULL check and that you know how structs work
Make sure also that you know what enums are do not work with volatile i value

It would awesome that you also know about function pointers if you want to have a good start

## Prelude

Make sure that you destroy well the program items

Leaks are really bad for your program please be concensious about that

Try not to load everything from the beginning it's bad like really bad make sure to load stuff only when it is necessary

## Resources
If you want to make a resource handler the best would be to implement hashmaps
You can create hashmaps with static memory such as:
```c
struct hashmap_resource {
    any_type resource;
    char *filepath;
};

struct game {
    // ...
    struct hashmap_resource resource[8192];
};
```

Handle the conflicts like you want but avoid at any cost the to pass over 15000 resources in static at this rate use dynamic memory

If stuff like this is a blurry you should learn what an hashmap is.
[An advanced video](https://www.youtube.com/watch?v=wg8hZxMRwcw)
[A beginner video](https://www.youtube.com/watch?v=2Ti5yvumFTU)

If you understood that check the Union and resources section

## Union and resources (Really advanced stuff)

An union is a data type that uses the same memory space you should really know how to use them
A real implementation of the `struct hashmap_resource` would be
```c
struct hashmap_resource {
    union {
        sfTexture *texture;
        sfMusic *music;
        ...
    };
    char *filepath;
    enum {
        HR_TEXTURE,
        HR_MUSIC,
    } type; // HR namspace for hashmap_resource
};
```
If we still use SFML by the time we read that otherwise it is still transposable with a lot of other things

## Scenes

A scene is state of your game for example your menu is a scene
The game boss scene or the village scene is a sub scene of your scene game etc...

Use enum and function pointers for your scene here is an example:

```c
// considering thoses 3 functions
// game_playing is 1
// game_menu is 2
// game_stuff is 3

void game_playing(game_system_t *sys)
{
    does stuff
}

void game_menu(game_system_t *sys)
{
    does stuff
}

void game_stuff(game_system_t *sys)
{
    doess stuff
}
```

The bad example:
```c
void game_loop(game_system_t *sys)
{
    if (sys.game_state == 0)
        game_playing(sys)
    else if (sys.game_state == 1)
        game_menu(sys)
    else if (sys.game_state == 2)
        game_stuff(sys);
}
```
We don't really know what means 0 1 and 2 and that can add up to many else if

The slightly better one
```c
enum game_scenes {
    GAME_PLAYING,
    GAME_MENU,
    GAME_STUFF
};

void game_loop(game_system_t *sys)
{
    switch (sys.game_state) {
        case GAME_PLAYING:
            game_playing(sys)
            break;
        case GAME_MENU:
            game_menu(sys)
            break;
        case GAME_STUFF:
            game_stuff(sys);
            break;
    }
}
```
This time the code is much more readable and he used a switch case to call his functions that makes a bit more sense but the switch can become really long so it can be a problem with more than 5 scenes

The best one:
First we can notice that all thoses functions returns the same thing and take the same type of variable so we can do:

(We implicitely assume that there is an enum for the scenes)

```c
void game_loop(game_system_t *sys)
{
    void (*game_fun[])(game_system_t *) = {
        game_playing, game_menu, game_stuff
    };
    game_fun[sys.game_state](sys);
}
```
The principle of this is an array of function using the state
If `sys.game_state` is equivalent to 0 it will be equal to the `game_playing` function and will call with as argument sys

### Entity

You shall look about what an ECS is and how to implement one
