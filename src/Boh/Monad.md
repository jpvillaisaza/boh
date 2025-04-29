# Monad

```haskell
module Boh.Monad
  ( Monad(..)
  ) where
```

```haskell
import Boh.Applicative (Applicative)
import Boh.Monoid (Monoid)
import Boh.Prelude
import Boh.Semigroup (Semigroup(..))
```

```haskell
class Applicative m => Monad m where
  (>>=) :: m a -> (a -> m b) -> m b
```

## Instances

### `[]`

```haskell
instance Monad [] where
  (>>=) :: [a] -> (a -> [b]) -> [b]
  xs >>= f = [y | x <- xs, y <- f x]
```

### `Maybe`

```haskell
instance Monad Maybe where
  (>>=) :: Maybe a -> (a -> Maybe b) -> Maybe b
  Nothing >>= _ = Nothing
  Just x >>= k = k x
```

### `Either`

```haskell
instance Monad (Either a) where
  (>>=) :: Either a b -> (b -> Either a c) -> Either a c
  Left x >>= _ = Left x
  Right y >>= k = k y
```

### `(,)`

```haskell
instance Monoid a => Monad ((,) a) where
  (>>=) :: (a, b) -> (b -> (a, c)) -> (a, c)
  (x1, y) >>= k = let (x2, z) = k y in (x1 <> x2, z)
```

### `(->)`

```haskell
instance Monad ((->) a) where
  (>>=) :: (a -> b) -> (b -> a -> c) -> a -> c
  (>>=) f g x = g (f x) x
```

## References

TODO
