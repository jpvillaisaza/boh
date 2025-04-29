# Monoid

```haskell
module Boh.Monoid
  ( Monoid(..)
  ) where
```

```haskell
import Boh.Semigroup (Semigroup)
```

```haskell
class Semigroup a => Monoid a where
  mempty :: a
```

## References

TODO
