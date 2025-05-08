# Functor

```haskell
module Boh.Functor
  ( Functor(..)
  ) where
```

## Overview

TODO

## Motivation

TODO

## TODO

```haskell
import Boh.Prelude
```

```haskell
class Functor f where
  fmap :: (a -> b) -> f a -> f b
```

## Instances

### `[]`

```haskell
instance Functor [] where
  fmap :: (a -> b) -> [a] -> [b]
  fmap _ [] = []
  fmap f (x:xs) = f x : fmap f xs
```

### `Maybe`

```haskell
instance Functor Maybe where
  fmap :: (a -> b) -> Maybe a -> Maybe b
  fmap _ Nothing = Nothing
  fmap f (Just x) = Just (f x)
```

### `Either`

```haskell
instance Functor (Either a) where
  fmap :: (b -> c) -> Either a b -> Either a c
  fmap _ (Left x) = Left x
  fmap g (Right y) = Right (g y)
```

### `(,)`

```haskell
instance Functor ((,) a) where
  fmap :: (b -> c) -> (a, b) -> (a, c)
  fmap g (a, y) = (a, g y)
```

### `(->)`

```haskell
instance Functor ((->) a) where
  fmap :: (b -> c) -> (a -> b) -> a -> c
  fmap g f x = g (f x)
```

## Laws

```haskell ignore
fmap id == id
```

```haskell ignore
fmap (g . f) == fmap f . fmap g
```

## Exercises

TODO

## References

TODO

* Hutton (2016, section 12.1)

## Bibliography

TODO

* Hutton, Graham (2016). _Programming in Haskell_. 2nd ed. Cambridge
  University Press.
* Lipovača, Miran (2011). _Learn You a Haskell for Great Good! A
  Beginner's Guide_. No Starch Press.
* Marlow, Simon, ed. (2010). _Haskell 2010 Language Report_.
* Yorgey, Brent (2009). The Typeclassopedia. In: _The Monad.Reader_
  13, pp. 17–68.
