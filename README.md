# purescript-query-params

This library provides a simple means of getting query parameters from the browser's url or from a specific url.  See the
[docs](./docs/QueryParams.md).

# Quick Start

```purescript

import Control.Monad.Eff (Eff)
import Control.Monad.Eff.Console (CONSOLE, log)
import Prelude (Unit, bind, (<>), show, ($))
import QueryParams (getParam, hasParam, runInBrowser, runInEnv)

main :: Eff (console :: CONSOLE) Unit
main = do

  let browserHasParam = runInBrowser $ hasParam "test"

  -- Get a query parameter from the browser's current url
  let browserValue = runInBrowser $ getParam "test"

  -- Get a query parameter from a specific url
  let envValue = (runInEnv "http://test.com?test=abc") $ getParam "test"

  log $ "Query Param ?test in browser: " <> (show browserValue)
  log $ "Query Param ?test in env: " <> (show envValue)

  case browserHasParam of
    true -> log $ "URL has ?test in it"
    false -> log $ "URL does not have ?test in it"

```
