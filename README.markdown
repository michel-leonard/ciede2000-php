Browse : [Julia](https://github.com/michel-leonard/ciede2000-julia) · [Kotlin](https://github.com/michel-leonard/ciede2000-kotlin) · [Lua](https://github.com/michel-leonard/ciede2000-lua) · [MATLAB](https://github.com/michel-leonard/ciede2000-matlab) · [Microsoft Excel](https://github.com/michel-leonard/ciede2000-excel) · **PHP** · [Perl](https://github.com/michel-leonard/ciede2000-perl) · [Python](https://github.com/michel-leonard/ciede2000-python) · [R](https://github.com/michel-leonard/ciede2000-r) · [Ruby](https://github.com/michel-leonard/ciede2000-ruby) · [Rust](https://github.com/michel-leonard/ciede2000-rust)

# CIEDE2000 color difference formula in PHP

This page presents the CIEDE2000 color difference, implemented in the PHP programming language.

![Logo for CIEDE2000 in Hypertext Preprocessor](https://raw.githubusercontent.com/michel-leonard/ciede2000-color-matching/refs/heads/main/docs/assets/images/logo.jpg)

## About

Here you’ll find the first rigorously correct implementation of CIEDE2000 that doesn’t use any conversion between degrees and radians. Set parameter `canonical` to obtain results in line with your existing pipeline.

`canonical`|The algorithm operates...|
|:--:|-|
`false`|in accordance with the CIEDE2000 values currently used by many industry players|
`true`|in accordance with the CIEDE2000 values provided by [this](https://hajim.rochester.edu/ece/sites/gsharma/ciede2000/) academic MATLAB function|

## Our CIEDE2000 offer

This production-ready file, released in 2026, contain the CIEDE2000 algorithm.

Source File|Type|Bits|Purpose|Advantage|
|:--:|:--:|:--:|:--:|:--:|
[ciede2000.php](./ciede2000.php)|`float`|64|General|Interoperability|

### Software Versions

- PHP 4.4.9
- PHP 5.6.34
- PHP 7.4.33
- PHP 8.3.21

### Example Usage

We calculate the CIEDE2000 distance between two colors, first without and then with parametric factors.

```php
// Example of two L*a*b* colors
list($l1, $a1, $b1) = array(87.5, 94.2, -12.5);
list($l2, $a2, $b2) = array(85.5, 71.4, 14.8);

$delta_e = ciede2000($l1, $a1, $b1, $l2, $a2, $b2);
echo "delta_e = $delta_e\n"; // ΔE2000 = 11.66865751625

// Example of parametric factors used in the textile industry
list($kl, $kc, $kh) = array(2.0, 1.0, 1.0);

// Perform a CIEDE2000 calculation compliant with that of Gaurav Sharma
$canonical = true;

$delta_e = ciede2000($l1, $a1, $b1, $l2, $a2, $b2, $kl, $kc, $kh, $canonical);
echo "delta_e = $delta_e\n"; // ΔE2000 = 11.614545643316
```

As of PHP8, the CIEDE2000 function can be significantly faster by properly configuring `opcache.jit`.

### Test Results

LEONARD’s tests are based on well-chosen L\*a\*b\* colors, with various parametric factors `kL`, `kC` and `kH`.

```
 CIEDE2000 Verification Summary :
          Compliance : [ ] CANONICAL [X] SIMPLIFIED
  First Checked Line : 50.0,128.0,-124.0,50.0,33.0,32.0,1.0,1.0,1.0,44.83453294874678
           Precision : 12 decimal digits
           Successes : 100000000
               Error : 0
            Duration : 530.53 seconds
     Average Delta E : 67.12
   Average Deviation : 5e-15
   Maximum Deviation : 1.4e-13
```

```
CIEDE2000 Verification Summary :
          Compliance : [X] CANONICAL [ ] SIMPLIFIED
  First Checked Line : 50.0,128.0,-124.0,50.0,33.0,32.0,1.0,1.0,1.0,44.83434288128610
           Precision : 12 decimal digits
           Successes : 100000000
               Error : 0
            Duration : 533.95 seconds
     Average Delta E : 67.12
   Average Deviation : 5.5e-15
   Maximum Deviation : 1.4e-13
```

## Public Domain Licence

You are free to use these files, even for commercial purposes.
