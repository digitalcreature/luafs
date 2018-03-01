# concept

## model
path names are written in terms of lua values. rather than having a tree of directories with files at the leaves, we build a graph of lua tables that represent possible file locations. this graph can take on any structure that regular lua tables can take on within a standard lua runtime environment. tables can reference themselves, tables can reference other tables multiple times, cycles can exist, etc.

these tables do not represent files themselves, only possible locations. if the table exists, then it will be shown to the user as a file of size 0. tables also do not have their own names; they are named only by the path one must take to reach them. this is similar to the way that, in \*nix file systems, inodes have no names, and are only names by the paths that are linked to them.

### ptables
just like standard lua tables, our ptables ("path tables") are associative arrays of key-value pairs. take as an example the following traditional file structure:
```
foo
 |-- a
 |   \-- bar
 |
 |-- b
 |   |-- baz1
 |   \-- baz2
 |
 \-c
```
these paths would be structured as follows, using ptables (shown with lua table syntax)
```lua
foo = {
    a = {
        bar = {},
    },
    b = {
        baz1 = {},
        baz2 = {},
    },
    c = {},
}
```
