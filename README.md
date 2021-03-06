# colorutilities [![NPM version][npm-image]][npm-url]
> A library of well-tested helper methods for working with colors. Comes with flow typings and tree-shakeable modules.

## Installation
Simply do: `npm install colorutilities`.

## What is it?

This is a collection of helper methods for working with colors and converting between color systems. Simple methods are provided such as `toHex()`, `toHsl()`, `toHsv()`, `toRgb()`, `saturate()`, `lighten()` and much more.

The library takes care of figuring out which color system your input string comes from, so you can just use the library and not care about the rest.

Supported color systems:
- RGB/RGBa
- Hex
- HSV/HSB
- HSL/HSLa
- HTML color names.

Beyond that, everything is typed with [Flow](https://flowtype.org/) and every method is exported as separate modules. This makes this library very easy to tree-shake and incorporate in your rollup or webpack build.

At the time of writing, 388 tests has been written for the library methods. I'd say you can use it in production today.

Have fun!

## Examples

```javascript
import {toHsl, lighten, saturate, isLight, randomHexColor} from "colorutilities";

toHsl("#DC143C")          // returns 'hsl(348, 83%, 47%)'
toHsl("DC143C")           // returns 'hsl(348, 83%, 47%)'
toHsl("rgb(220, 20, 60)") // returns 'hsl(348, 83%, 47%)'
toHsl("crimson")          // returns 'hsl(348, 83%, 47%)'
toHsl("hsb(348, 91, 86)") // returns 'hsl(348, 83%, 47%)'

lighten("#DDACED", 10)        // lightens the color 10% and returns the new value: #EACDF4.
saturate("brown", 100)        // saturates the HTML color 'brown' an additional 100%.
isLight("rgb(234, 205, 244)") // returns true, that's a pretty light color.
randomHexColor();             // returns a random hex color.
```

## Changelog:

**v0.02**:

- Fixed a bug where RGB colors could be returned non-rounded even though 'rounding' was true.

**v0.01**:

- First release! 388 tests has been written and bidirectional conversions between HEX, RGB/RGBa, HSL/HSLa, HSV/HSB and HTML color names are supported in this initial release.

## Usage
Import it in your project like this:

```javascript
import {saturate, toRgb, ...} from "colorutilities"; // (standard) Transpiled to ES5.
// or

import {saturate, toRgb, ...} from "colorutilities/native"; // Transpiled to ES5 except for native ES-modules.
// or

import {saturate, toRgb, ...} from "colorutilities/typed"; // Flow typings, ES-modules, pretranspile.
```

## Documentation

### `#isLight()`

*Determines if the given color is light or not.*

**Signature:**

```javascript
isLight (color: string): boolean
```

**Arguments**:

- `color: string` - The color to check. Can be any of the color systems CSS can handle with the addition of HSB/HSV.

**Returns**:

`boolean`         - Returns true if the color is light, false otherwise.

#### Example
```javascript
isLight("rgb(234, 205, 244)") // returns true, that's a pretty light color.
```

### `#lighten()`

*Changes the lightness of the given color. Will automatically determine the type of color and how to handle it. Pass negative values to darken the color instead.*

**Signature:**

```javascript
lighten (color: string, percentage: number = 10): string
```

**Arguments**:

- `color: string`        - The color to lighten. Can be any of the color systems CSS can handle with the addition of HSB/HSV.

- `percentage?: number`  - Optionally, the amount of percentage to lighten the color. Pass a negative value to darken the color instead. `Default = 10`

**Returns**:

`string` - The lightened/darkened color.

#### Example
```javascript
lighten("#DDACED", 10) // lightens the color 10% and returns the new value: #EACDF4.
lighten("#DDACED", -90) // darkens the color 90% and returns the new value: #1B0721.
```

### `#saturate()`

*Changes the saturation of the given color. Will automatically determine the type of color and how to handle it. Pass a negative percentage value to desaturate the color instead.*

**Signature:**

```javascript
saturate (color: string, percentage: number = 10): string
```

**Arguments**:

- `color: string`        - The color to saturate. Can be any of the color systems CSS can handle with the addition of HSB/HSV.

- `percentage?: number`  - Optionally, the amount of percentage to saturate the color. Pass a negative value to desaturate the color instead. `Default = 10`

**Returns**:

`string` - The saturated/desaturated color.

#### Example
```javascript
saturate("brown", 100)  // saturates the HTML color 'brown' an additional 100%.
saturate("brown", -100) // desaturates the HTML color 'brown' 100%.
```

### `#toHex()`

*Takes a color and converts it to a hex color.*

**Signature:**

```javascript
toHex (color: string): string
```

**Arguments**:

- `color: string`        - The color to convert to a hex color. Can be any of the color systems CSS can handle with the addition of HSB/HSV. If a hex color is given, a hex color will be returned.

**Returns**:

`string` - The hex representation of the given color. Will always have a '#' in front of it.

**Throws**:

- `TypeError` - If the first argument is not of type 'string'.
- `TypeError` - If the given color appears to be a hex color but is of invalid length.
- `TypeError` - If the method didn't succeed in normalizing the given argument into a hex color.

#### Example
```javascript
toHex("#DC143C")          // returns '#DC143C'
toHex("DC143C")           // returns '#DC143C'
toHex("rgb(220, 20, 60)") // returns '#DC143C'
toHex("crimson")          // returns '#DC143C'
toHex("hsb(348, 91, 86)") // returns '#DC143C'
```

### `#toRgb()`

*Takes a color and converts it to an RGB color.*

**Signature:**

```javascript
toRgb (color: string): string
```

**Arguments**:

- `color: string`        - The color to convert to an RGB color. Can be any of the color systems CSS can handle with the addition of HSB/HSV. If an RGB color is given, an RGB color will be returned.

**Returns**:

`string` - The RGB representation of the given color.

**Throws**:

- `TypeError` - If the first argument is not of type 'string'.
- `TypeError` - If the given color appears to be a hex color but is of invalid length.
- `TypeError` - If the method didn't succeed in normalizing the given argument into an RGB color.

#### Example
```javascript
toRgb("#DC143C")          // returns 'rgb(220, 20, 60)'
toRgb("DC143C")           // returns 'rgb(220, 20, 60)'
toRgb("rgb(220, 20, 60)") // returns 'rgb(220, 20, 60)'
toRgb("crimson")          // returns 'rgb(220, 20, 60)'
toRgb("hsb(348, 91, 86)") // returns 'rgb(220, 20, 60)'
```

### `#toHsl()`

*Takes a color and converts it to an HSL color.*

**Signature:**

```javascript
toRgb (color: string): string
```

**Arguments**:

- `color: string`        - The color to convert to an HSL color. Can be any of the color systems CSS can handle with the addition of HSB/HSV. If an HSL color is given, an HSL color will be returned.

**Returns**:

`string` - The HSL representation of the given color.

**Throws**:

- `TypeError` - If the first argument is not of type 'string'.
- `TypeError` - If the given color appears to be a hex color but is of invalid length.
- `TypeError` - If the method didn't succeed in normalizing the given argument into an HSL color.

#### Example
```javascript
toHsl("hsl(348, 83%, 47%)") // returns 'hsl(348, 83%, 47%)'
toHsl("#DC143C")            // returns 'hsl(348, 83%, 47%)'
toHsl("DC143C")             // returns 'hsl(348, 83%, 47%)'
toHsl("rgb(220, 20, 60)")   // returns 'hsl(348, 83%, 47%)'
toHsl("crimson")            // returns 'hsl(348, 83%, 47%)'
toHsl("hsb(348, 91, 86)")   // returns 'hsl(348, 83%, 47%)'
```

### `#toHsv()`

*Takes a color and converts it to an HSV/HSB color.*

**Signature:**

```javascript
toRgb (color: string): string
```

**Arguments**:

- `color: string`        - The color to convert to an HSV/HSB color. Can be any of the color systems CSS can handle with the addition of HSB/HSV. If an HSV/HSB color is given, an HSV/HSB color will be returned.

**Returns**:

`string` - The HSV/HSB representation of the given color.

**Throws**:

- `TypeError` - If the first argument is not of type 'string'.
- `TypeError` - If the given color appears to be a hex color but is of invalid length.
- `TypeError` - If the method didn't succeed in normalizing the given argument into an HSVB/HSB color.

#### Example
```javascript
toHsv("hsb(348, 91, 86)")   // returns 'hsb(348, 91, 86)'
toHsv("hsv(348, 91, 86)")   // returns 'hsv(348, 91, 86)'
toHsv("hsl(348, 83%, 47%)") // returns 'hsb(348, 91, 86)'
toHsv("#DC143C")            // returns 'hsb(348, 91, 86)'
toHsv("DC143C")             // returns 'hsb(348, 91, 86)'
toHsv("rgb(220, 20, 60)")   // returns 'hsb(348, 91, 86)'
toHsv("crimson")            // returns 'hsb(348, 91, 86)'
```

### `#randomHexColor()`

*Generates a random hex color and returns it.*

**Signature:**

```javascript
randomHexColor (): string
```

**Returns**:

`string` - A random hex color. Always starts with '#'.

#### Example
```javascript
setInterval(() => document.body.style.backgroundColor = randomHexColor(), 100);

// Makes the background of the body element change to a new random color every 100ms. Welcome back to web 1.0!
```

### `#randomRgbColor()`

*Generates a random RGB color and returns it.*

**Signature:**

```javascript
randomRgbColor (): string
```

**Returns**:

`string` - A random RGB color.

#### Example
```javascript
setInterval(() => document.body.style.backgroundColor = randomRgbColor(), 100);

// Makes the background of the body element change to a new random color every 100ms. Welcome back to web 1.0!
```

### `#randomHslColor()`

*Generates a random HSL color and returns it.*

**Signature:**

```javascript
randomHslColor (): string
```

**Returns**:

`string` - A random HSL color.

#### Example
```javascript
setInterval(() => document.body.style.backgroundColor = randomHslColor(), 100);

// Makes the background of the body element change to a new random color every 100ms. Welcome back to web 1.0!
```

### `#randomHsvColor()`

*Generates a random HSV color and returns it.*

**Signature:**

```javascript
randomHsvColor (): string
```

**Returns**:

`string` - A random HSV color.

#### Example
```javascript
setInterval(() => document.body.style.backgroundColor = randomHsvColor(), 100);

// Makes the background of the body element change to a new random color every 100ms. Welcome back to web 1.0!
```


### Other methods
There's a lot of them. The above was the highlights. Everything is well-documented in the source code. Here's a quick overview of the methods that isn't included in this *readme*:

- **`hslStringToHslTuple`:**
	-	Converts a string-represented HSL color to a tuple of the values.

- **`hslToHsla`:**
	-	Generates a HSLA color from a HSL color.

- **`hslaStringToHslaTuple`:**
	-	Converts a string-represented HSLa color to a tuple of the values.

- **`hslToRgbTuple`:**
	-	Converts the given HSL color to an RGB color and returns it as a tuple of the values.

- **`hslToRgb`:**
	-	Converts the given HSL color to an RGB color and returns it as a string.

- **`hslaToRgbaTuple`:**
	-	Converts the given HSLa color to an RGBa color and returns it as a tuple of the values.

- **`hslaToRgba`:**
	-	Converts the given HSLa color to an RGBa color and returns it as a string.

- **`hslaToHsl`:**
	-	Converts the given HSLa color to an HSL color and returns it as a string.

- **`rgbStringToRgbTuple`:**
	-	Generates a tuple-representation of an RGB color.

- **`rgbaStringToRgbaTuple`:**
	-	Generates a tuple-representation of an RGBa color.

- **`rgbToHex`:**
	-	Generates a hex representation of an RGB color.

- **`rgbaToHex`:**
	-	Generates a hex representation of an RGBa color.

- **`hsvStringToHsvTuple`:**
	-	Generates a tuple-representation of an HSV/HSB color.

- **`hsvToRgbTuple`:**
	-	Converts an HSV/HSB color to an RGB color and returns it as a tuple of the values.

- **`hsvToRgb`:**
	-	Converts a HSV color to an RGB color and returns it as a string.

- **`hexToRgbTuple`:**
	-	Generates a RGB version of a hex color and returns it as a tuple of the values.

- **`hexToRgb`:**
	-	Generates a RGB version of a hex color and returns it as a string.

- **`hexToHslTuple`:**
	-	Generates a HSL color from a hex color and returns it as a tuple.

- **`hexToHslaTuple`:**
	-	Generates a HSLA color from a hex color and returns it as a tuple.

- **`hexToHsla`:**
	-	Generates a HSLA color from a hex color and returns it as a string.

- **`hexToHsl`:**
	-	Generates a HSL color from a hex color and returns it as a string.

- **`rgbToHslTuple`:**
	-	Generates a HSL color from a RGB color and returns it as a tuple of the values.

- **`rgbToHsl`:**
	-	Generates a HSL color from a RGB color and returns it as a string.

- **`rgbToHsvTuple`:**
	-	Converts an RGB color to an HSV/HSB color and returns it as a tuple of the values.

- **`rgbToHsv`:**
	-	Converts an RGB color to an HSV/HSB color and returns it as a string.

- **`randomRgbColor`:**
	-	Generates a random RGB color and returns it.

- **`randomHslColor`:**
	-	Generates a random HSL color and returns it.

- **`randomHsvColor`:**
	-	Generates a random HSV/HSB color and returns it.

[npm-url]: https://npmjs.org/package/colorutilities
[npm-image]: https://badge.fury.io/js/colorutilities.svg
