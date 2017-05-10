# ds_sprite_buffer

SpriteBatchBuffer which can be used along with the diesel renderer. it is a single header file which you
can copy to your project. 

## How to use it

In general only the API and classes are visible. So at point you need to include the implementation as well.
You do this be definining SPRITE_IMPLEMENTATION right before the include. You only need to do this once.

```c
#define SPRITE_IMPLEMENTATION
#include <SpriteBatchBuffer.h>
```

First you need to initialize the SpriteBatchBuffer:

```c
SpriteBatchBufferInfo sbbInfo = { 2048, textureID };
SpriteBatchBuffer spriteBuffer(sbbInfo);
```

SpriteBatchBufferInfo

| Attribute   | Description                                 |
| ----------- |---------------------------------------------|
| maxSprites  | the maximum number of sprites for one batch |
| textureID   | the texture id                              |

The SBB can only work with one texture. It is usually a good approach to include all your textures
into one texture atlas. Therefore this one uses only one texture.

You can then start drawing sprites:

```c
spriteBuffer.begin();
spriteBuffer.add(ds::vec2(512,384), ds::vec4(46, 138, 46, 46));
spriteBuffer.flush();
```

The texture rect defines the rectangle within the texture. The parameter are:

- left
- top
- width
- height

If you exceed the maximum number of sprites the SBB will flush and then start all over again.
This way you can easily draw much more sprites than defined as maximum sprites.