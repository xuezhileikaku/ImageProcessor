
# ImageProcessor

A PHP class for creating GIFs and sprite images with text.

## Usage

### Creating a GIF

```php
require 'Image.php';

$image = new Image();
$image->createGif('output.gif', 'Hello World', 28, '#FF0000', '/path/to/font.ttf', '#FFFFFF');
```php
### Creating a Sprite Image
```php
require 'Image.php';

$image = new Image();
$image->createSprite('sprite.png', 'Hello World', 28, '#0000FF', '/path/to/font.ttf', '#FFFFFF');
```php
## Methods
### createGif
Description: Creates a GIF with the given text.
Parameters:
$file_name (string): The name of the output GIF file.
$words (string): The text to be displayed in the GIF.
$font_size (int): The size of the font.
$font_color (string): The color of the font in hexadecimal.
$font_path (string): The path to the font file.
$bg (string): The background color in hexadecimal.
### createSprite
Description: Creates a sprite image with the given text.
Parameters:
$file_name (string): The name of the output PNG file.
$words (string): The text to be displayed in the sprite image.
$font_size (int): The size of the font.
$words_color (string): The color of the text in hexadecimal.
$font_path (string): The path to the font file.
$bg (string): The background color in hexadecimal.
### hexToRgb
Description: Converts a hexadecimal color to RGB.
Parameters:
$hex (string): The hexadecimal color.
Returns: An array containing the RGB values.
### rgbToHex
**Description
