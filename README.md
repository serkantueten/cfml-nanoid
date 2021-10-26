 [![cfmlbadges](https://cfmlbadges.monkehworks.com/images/badges/compatibility-coldfusion-2016.svg)](https://cfmlbadges.monkehworks.com) [![cfmlbadges](https://cfmlbadges.monkehworks.com/images/badges/modernize-or-die.svg)](https://cfmlbadges.monkehworks.com)

# cfml-nanoid
CFML implementation of [nanoid](https://github.com/ai/nanoid), secure URL-friendly unique ID generation.

- A tiny, secure URL-friendly unique string ID generator for JavaScript
- Safe. It uses CFML's RandRange("SHA1PRNG") to guarantee a proper distribution of symbols.
- Compact. It uses more symbols than UUID (`A-Za-z0-9_-`) and has the same number of unique options in just 21 symbols instead of 36.

## Usage

Instantiate the component:

```js
nanoId = new nanoId();
```

## nanoId.generate()

Generates compact ID using settings.  (Defaults to `21` characters of the alphabet `0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ_abcdefghijklmnopqrstuvwxyz-` using `SHA1PRNG` algorithm.)

```js
writeOutput(nanoId.generate());
// jLWi7TKamN1zqpE_Z00Ab
```

## nanoId.generate(_alphabet_, _size_, _algorithm_)
One-time override for a single ID generation
```js
writeOutput(nanoId.generate(alphabet="ABCDEFGHJKLMNPQRSTUVXYZ"));
// XYDADCEJSYBMDLLTREBEF

writeOutput(nanoId.generate(size=12));
// 2PBPRu7HRoJP

writeOutput(nanoId.generate(algorithm="NativePRNG"));
// fkDNYl2snoOXMegoFi_Dr

// Using 2 ordered arguments
writeOutput(nanoId.generate("ABCDEFGHIJKLMNOPQRSTUVXYZ", 12));
// THTMYMVEGMAV

// Using 3 ordered arguments
writeOutput(nanoId.generate("ABCDEFGHIJKLMNOPQRSTUVXYZ", 12, "IBMSecureRandom"));
// RMQFYHVJIMEZ

```

## nanoId.setAlphabet(_alphabet_)

Sets a custom characters for all subsequent ID generations. A dictionary name can also be used. (Defaults to `0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ_abcdefghijklmnopqrstuvwxyz-`.)
```js
nanoId.setAlphabet("ABCDEFGHJKLMNPQSTUVWXYZ");
// no output
```

## nanoId.setSize(_integer_);

Sets custom string length for all subsequent ID generations. (Defaults to `21`)
```js
nanoId.setSize(12);
// no output
```

## nanoId.setAlgorithm(_algorithm_);

Sets `secure` or `non-secure` generation type.  (Defaults to `SHA1PRNG`. Options are `SHA1PRNG`, `IBMSecureRandom`, `NativePRNG`, `NativePRNGBlocking`, `NativePRNGNonBlocking`.)
```js
nanoId.setAlgorithm("IBMSecureRandom");
// no output
```

## Alphabet Dictionary

Code | Description | Characters
--- | --- | ---
default | Default | 0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ_abcdefghijklmnopqrstuvwxyz-
numbers | Numbers from 0 to 9 | 0123456789
hexadecimalLowercase | Lowercase English hexadecimal lowercase characters | 0123456789abcdef
hexadecimalUppercase | Lowercase English hexadecimal uppercase characters | 0123456789ABCDEF
lowercase | Lowercase English letters | abcdefghijklmnopqrstuvwxyz
uppercase | Uppercase English letters | ABCDEFGHIJKLMNOPQRSTUVWXYZ
alphanumeric | Combination of all the lowercase, uppercase characters & numbers from 0 to 9. Does not include any symbols or special characters | 0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz
nolookalikes | Numbers & english alphabet without lookalikes: `1`, `l`, `I`, `0`, `O`, `o`, `u`, `v`, `5`, `S`, `s`, `2`, `Z`. | 346789ABCDEFGHJKLMNPQRTUVWXYabcdefghijkmnpqrtwxyz
nolookalikesSafe | Same as `noolookalikes` but with removed vowels & following letters: `3`, `4`, `x`, `X`, `V`. This list should protect you from accidentally getting obscene words in generated strings. | 6789BCDFGHJKLMNPQRTWbcdfghjkmnpqrtwz

## To Review

Research to determine if Java native `java.security.SecureRandom` is sufficient and whether there are any [hardware random generator](https://github.com/ai/nanoid/issues/311#issuecomment-951434986) options available.
