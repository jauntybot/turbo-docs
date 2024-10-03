# Nine Slices

Nine slices are sprites that are designed to be transformed and stretched to any dimensions. Turbo's nine slices are sliced into even squares, so to draw a nine slice you need a sprite with dimensions divisible by 3.

> Sprite Setup
>
> Follow these simple steps to integrate sprites into your Turbo game:
> 
> 1. **Create a `sprites` Folder**
> 
> - Inside your project directory, create a folder named `sprites`. This folder will contain all your game sprites.
> 
> 2. **Put Images in the Folder**
> 
> - The following image formats are supported: `.png`, `.gif` (non-animated), `.webp`, and `.jpg`/`.jpeg`.
>
> Now you're ready to draw some sprites!

## `nine_slice!`

Nine slice sprites from your project's `sprites` folder can be drawn using the `nine_slice` macro.

```rust title="turbo::canvas"
nine_slice!(
    &str,
    slice_size: u32,
    x: i32,
    y: i32,
    w: u32,
    h: u32,
    absolute: bool,
    opacity: f32
)
```

| Param       | Type   | Default         | Description                                                      |
| :---------- | :----- | :-------------- | :--------------------------------------------------------------- |
| -           | `&str` | -               | The sprite's name (filename minus the extension)                 |
| `slice_size`| `i32`  | `0`             | Dimension of sprite slice,  1/3 of your sprite's dimensions      |
| `x`         | `i32`  | `0`             |                                                                  |
| `y`         | `i32`  | `0`             |                                                                  |
| `w`         | `u32`  | [sprite width]  | Width of drawn nine slice                                        |
| `h`         | `u32`  | [sprite height] | Height of drawn nine slice                                       |
| `opacity`   | `f32`  | `1.0`           | Sprite opacity - `0.0` = fully transparent. `1.0` = fully opaque |
| `absolute`  | `bool` | `false`         | Screen anchor - `false` = anchor to game canvas `true` = anchor to camera |


## Example use
Button.png is a 15x15px nine slice sprite in our `sprites` folder. To draw it in our Turbo game, we call the `nine_slice!` macro in the `Turbo::go!` loop. We set `x` and `y` to it's position in the window, and `w` and `h` to how wide and tall we want it to draw.
```rust title="turbo::canvas"
nine_slice!("button", slice_size = 5, x = 42, y = 120, w = 120, h = 45);
```
### `slice_size`
This parameter determines how Turbo slices your sprite, its value should be equal to 1/3 of your sprite's dimensions. For example, a nine slice sprite that is 15x15px should have a `slice_size` value of 5.

### `absolute`
This parameter determines how the nine slice is drawn in the Turbo game window. `False` anchors the nine slice's position to the game canvas. `True` anchors the nine slice's position relative to the camera, useful for persistent UI elements.

### Repeating slices
Turbo draws nine slices by repeating the sliced segements to fit the inputed dimensions. Keep this in mind when designing your nine slice sprites, the borders aren't acutally stretched, they're repeated!
