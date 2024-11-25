# nectar-sql

[![Clojars](https://img.shields.io/badge/clojars-net.clojars.plooney81/nectarsql_1.0.5-blue.svg?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAMAAABEpIrGAAAABGdBTUEAALGPC/xhBQAAACBjSFJNAAB6JgAAgIQAAPoAAACA6AAAdTAAAOpgAAA6mAAAF3CculE8AAABjFBMVEUAAAAdCh0qDikdChwAAAAnDSY0EjM2FjUnDiYnDSYnDSYpDigyEDEEAQRGNUb///////8mDSYAAAAAAAAAAAAFAgUqEyoAAAAAAAAAAAAFAgUAAABXU1c2FjVMx+dQx+f///////9Nx+b////4/f6y4vRPt+RQtOT///9Qt+P///8oDSey4vRQr9/////3/P5hzelNx+dNx+dNx+f///8AAAAuDy0zETIAAAAoDScAAAAAAAARBREAAAAvDy40ETMwEC9gSF+Ne42ilKKuoK6Rg5B5ZXlaP1o4Gzf///9nTWZ4YncyEDF/bn/8/Pz9/P339/c1FTUlDCRRM1AbCRtlS2QyEDEuDy1gRWAxEDAzETIwEC/g4OAvDy40EjOaiZorDiq9sbzNyM3UzdQyEDE0ETMzETKflZ/UzdQ5Fzmu4fNYyuhNx+dPt+RLu9xQyOhBbo81GTuW2vCo4PJNx+c4MFE5N1lHiLFEhKQyEDGDboMzETI5Fjh5bXje2d57aHrIw8jc2NyWhJUrDioxe9o4AAAAPnRSTlMAkf+IAQj9+e7n6e31RtqAD/QAAAED+A0ZEQ8DwvkLBsmcR4aG8+cdAD6C8/MC94eP+qoTrgH+/wj1HA8eEvpXOCUAAAABYktHRA8YugDZAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAB3RJTUUH3wcHFjou4Z/shwAAAUpJREFUOMul0/VTwzAUB/AAwyW4y3B3h8EDNuTh7u6UDHcd8I+TbHSjWdrjju/1h77kc+3Lu5aQvyakF/r6B5wu1+DQMEBomLRtG0EpozYDCEccA4iIjIqOiY0bB5iYxHgZ4FQCpYneKmmal0aQPMOXZnUAvJhLkbpInf8NFtKCTrGImK6DJcTlDGl/BXGV6oCsrSNIYAM3aQDwl2xJYBtBB5lZAuyYgWzY3YMcNcjN2wc4EGMEFTg8+hlyfgEenygAj71Q9FBExH0wKC4p1bRTJlJWXqEAVNM05ovbXfkPAHBmAUQPAGaAsXMBLiwA8z3h0gRcsWsObuAWLJu8Awb3ZoB5T8EvS/CgBo9Y5Z8TPwXBJwlUI9Ia/yRrEZ8lID71Olrf0MiamkkL4kurDEjba+C/e2sninR0wrsH8eMTvrqIWbodjh7jyjdtCY3Aniz4jwAAACV0RVh0ZGF0ZTpjcmVhdGUAMjAxNS0wNy0wN1QyMjo1ODo0NiswMjowMCgWtSoAAAAldEVYdGRhdGU6bW9kaWZ5ADIwMTUtMDctMDdUMjI6NTg6NDYrMDI6MDBZSw2WAAAAAElFTkSuQmCC)](https://clojars.org/net.clojars.plooney81/nectar-sql)

nectar: A sugary liquid secreted by plants, primarily in their flowers, to attract pollinators like bees, butterflies, and
hummingbirds. It serves as the raw material for honey.

`nectar-sql`: Converts raw sql strings into honey sql. nectar-sql takes a raw sql string, parses it (using [JSqlParser](JSqlParser)) and converts it into [honeysql](https://github.com/seancorfield/honeysql)

nectar-sql is currently a work in progress and, at present, can be expected to handle a wide variety of `SELECT` queries.

## Usage

```clojure
(require '[plooney81.nectar.sql :as nsql])

;; convert a query...
(nsql/ripen
  "SELECT *
     FROM people
    WHERE age > 25
 ORDER BY age DESC")

;; ...to HoneySQL!
{:select   [:*]
 :from     [:people]
 :where    [:> :age 25]
 :order-by [[:age :desc]]}
```

Run the project's tests:

    $ clj -T:build test

Run the project's CI pipeline and build a JAR (this will fail until you edit the tests to pass):

    $ clj -T:build ci

This will produce an updated `pom.xml` file with synchronized dependencies inside the `META-INF`
directory inside `target/classes` and the JAR in `target`. You can update the version (and SCM tag)
information in generated `pom.xml` by updating `build.clj`.

Install it locally (requires the `ci` task be run first):

    $ clj -T:build install

Deploy it to Clojars -- needs `CLOJARS_USERNAME` and `CLOJARS_PASSWORD` environment
variables (requires the `ci` task be run first):

    $ clj -T:build deploy

Your library will be deployed to net.clojars.plooney81/nectar-sql on clojars.org by default.

## Support

- Scope:
    - We currently only support `SELECT` functionality
    - We hope to support `INSERT`, `UPDATE`, `DELETE` in the future

- nectar-sql relies heavily on [JSQLParser](JSqlParser)
    - JSQLParser doesn't currently support a few pieces of functionality, like Implicit Casting in Postgres
        - Check out the other things that [JSQLParser doesn't support](jsql-doesnt-support)

----
[honeysql]: https://github.com/seancorfield/honeysql
[JSqlParser]: https://github.com/JSQLParser/JSqlParser
[jsql-doesnt-support]: https://jsqlparser.github.io/JSqlParser/unsupported.html


## License

Copyright © 2024 Plooney

Distributed under the Eclipse Public License version 1.0.