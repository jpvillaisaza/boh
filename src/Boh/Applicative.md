# Applicative

```haskell
module Boh.Applicative
  ( Applicative(..)
  ) where
```

```haskell
import Boh.Functor (Functor(..))
import Boh.Monoid (Monoid(..))
import Boh.Prelude
import Boh.Semigroup (Semigroup(..))
```

```haskell
class Functor f => Applicative f where
  pure :: a -> f a
  (<*>) :: f (a -> b) -> f a -> f b
```

## Instances

### `[]`

```haskell
instance Applicative [] where
  pure :: a -> [a]
  pure x = [x]

  (<*>) :: [a -> b] -> [a] -> [b]
  fs <*> xs = [f x | f <- fs, x <- xs]
```

### `Maybe`

```haskell
instance Applicative Maybe where
  pure :: a -> Maybe a
  pure = Just

  (<*>) :: Maybe (a -> b) -> Maybe a -> Maybe b
  Nothing <*> _ = Nothing
  Just f <*> mx = fmap f mx
```

### `Either`

```haskell
instance Applicative (Either a) where
  pure :: b -> Either a b
  pure = Right

  (<*>) :: Either a (b -> c) -> Either a b -> Either a c
  Left x <*> _ = Left x
  Right g <*> ey = fmap g ey
```

### `(,)`

```haskell
instance Monoid a => Applicative ((,) a) where
  pure :: b -> (a, b)
  pure y = (mempty, y)

  (<*>) :: (a, b -> c) -> (a, b) -> (a, c)
  (x1, g) <*> (x2, y) = (x1 <> x2, g y)
```

### `(->)`

```haskell
instance Applicative ((->) a) where
  pure :: b -> a -> b
  pure y = \_ -> y

  (<*>) :: (a -> b -> c) -> (a -> b) -> a -> c
  f1 <*> f2 = \x -> f1 x (f2 x)
```

## References

TODO
