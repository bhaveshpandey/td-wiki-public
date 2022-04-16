# Scalpel

Recently I nuked some data I should not have. Big problem. Can we undo this shit? Can we recover the data. Well maybe we can.

```shell

sudo scalpel -c ~/scalpel.conf  -o recovered /dev/sda1
```

## Configuration

Following is an example configuration which is used by `scalple` to recover the data.

```text

#---------------------------------------------------------------------
# COMPUTER GRAPHICS
#---------------------------------------------------------------------
    # hip     y   575000000    \x30\x37\x30\x37\x30\x37\x30\x30   \x45\x52\x21\x21\x21\x00
    hip     y   575000000    \x30\x37\x30\x37\x30\x37   \x45\x52\x21\x21\x21\x00

    # hdr     y   750000000    \x23\x3f\x52\x41\x44\x49\x41\x4e

    # fbx     y   10000000000  \x4b\x61\x79\x64\x61\x72\x61\x20

    # abc     y   10000000000  \x4f\x67\x61\x77\x61\xff\x00\x01
#
```


## Resources

* [Sample config](https://github.com/sleuthkit/scalpel/blob/master/scalpel.conf)
