# CIEDE2000 color difference formula in PHP

This page presents the CIEDE2000 color difference, implemented in the PHP programming language.

![Logo for CIEDE2000 in Hypertext Preprocessor](https://raw.githubusercontent.com/michel-leonard/ciede2000-color-matching/refs/heads/main/docs/assets/images/logo.jpg)

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

## Public Domain Licence

You are free to use these files, even for commercial purposes.
