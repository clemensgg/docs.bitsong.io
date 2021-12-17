# Export the state

go-bitsong can dump the entire application state into a JSON file. This application state dump is useful for manual analysis and can also be used as the genesis file of a new network.

Export state with:

```
bitsongd export > [filename].json
```

You can also export state from a particular height (at the end of processing the block of that height):

```
bitsongd export --height [height] > [filename].json
```

If you plan to start a new network from the exported state, export with the `--for-zero-height` flag:

```
bitsongd export --height [height] --for-zero-height > [filename].json
```
