# Functor

```haskell
module Boh.Functor
  ( Functor(..)
  ) where
```

## Overview

TODO: In this chapter we're going to talk about functors, the first of
three type classes that might be the most important we'll see and work
as a foundation for a lot of other topics in Haskell.

## Motivation

TODO: First of all, we'll see examples of why we'd like to talk about
functors. The usual way is to start with `map` for lists and identify
that similar behaviors exist for other types, such as `Maybe` or other
structure types like trees. Then we can see that functor generalizes
this idea.

## TODO

TODO: In this section we'll see the functor type class and explain
its parts.

```haskell
import Boh.Prelude
```

```haskell
class Functor f where
  fmap :: (a -> b) -> f a -> f b
```

TODO: There are two parts to this type class. The first is `f`, which
is a type constructor. We've seen concrete types so far, but now we
have a type constructor. We'll see that `Int` is a concrete type, but
`Maybe` is a type constructor because it expects one more type, and
then `Maybe Int` is a concrete type.

```haskell ignore
class Functor (f :: Type -> Type) where
  fmap :: (a -> b) -> f a -> f b
```

The second part of the type class is the fmap function, which is a
lifting function. We could think about it as mapping over a container
or over a context, but the thinking that always applies is that of
lifting. We can see it with explicit parentheses:

```haskell ignore
class Functor (f :: Type -> Type) where
  fmap :: (a -> b) -> (f a -> f b)
```

## Instances

### `Identity`

```haskell
newtype Identity a = Identity a
```

```haskell
instance Functor Identity where
  fmap :: (a -> b) -> Identity a -> Identity b
  fmap f (Identity x) = Identity (f x)
```

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

TODO: Functors actually expect some laws to hold, but Haskell doesn't
force us to do that. There are two laws. The first is identity and
the second composition.

```haskell ignore
fmap id == id
```

```haskell ignore
fmap (g . f) == fmap f . fmap g
```

## Category theory

TODO: We'll now briefly mention that functors come from category
theory. Just the main concept and perhaps link somewhere else for
reading.

## Limitations

TODO: We're now going to work on an example that shows what we can't
do with functors, which should work as motivation to move on to
Applicative. Or maybe that's the start of the next chapter?

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
