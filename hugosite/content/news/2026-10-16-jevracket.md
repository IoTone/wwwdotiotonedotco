---
title: "jevracket — calibrated probabilities for Racket, now at full API parity"
date: 2026-10-16
draft: false
tags: ["release", "racket", "jev", "typesafe-ai", "api-client", "mit"]
summary: "jevracket is a Racket client for TypeSafe's System One API: ask typed questions about a blob of state, get calibrated probabilities back — no prose, no parsing. Opened in September, it now has full parity with the typesafe 0.7.5 API, built from the published spec with zero dependencies beyond Racket's base."
source_url: "https://github.com/IoTone/jevracket"
hero_image: "/images/news/jevracket.png"
repo_url: "https://github.com/IoTone/jevracket"
related_projects:
  - "telemachus"
---

[**jevracket**](https://github.com/IoTone/jevracket), our Racket client for the [TypeSafe](https://typesafe.ai) **System One** API, just landed **full parity with the typesafe 0.7.5 API**, a few weeks after its September debut.

Jev answers typed questions about a blob of state and returns **calibrated probabilities**. You don't get prose back and you don't parse anything: a yes/no question returns a number between 0 and 1, a multiple-choice question returns the winner plus the whole distribution, and a rating question returns a probability-weighted value plus a confidence. Several questions about the same state cost **one request** — jev reads the state once and evaluates every question against it.

```racket
(define r
  (ask c "Payouts have been failing for three days and I am losing sales."
       (hash "urgent" (noul "The message conveys time pressure.")
             "team"   (choice "Which team should handle this"
                              (hash "billing" "Payments, invoicing, refunds"
                                    "technical" "Bugs, outages, integrations")))))

(noul-answer-value   (response-ref r "urgent"))   ; 0.99
(choice-answer-value (response-ref r "team"))     ; "technical"
```

## Built from the spec, not ported

The client is written against the published HTTP reference at [docs.typesafe.ai/api](https://docs.typesafe.ai/api), not translated from the vendor's pre-1.0 Python SDK — the wire protocol is two endpoints and a handful of JSON shapes, and the SDK's bulk is ergonomics that wouldn't survive a move to Racket anyway. The tests pin the documented request and response examples **verbatim**, so a change on the vendor's side fails the suite rather than surfacing in production.

**No dependencies beyond `base`** — `net/http-client` and `json` ship with Racket. A client for one HTTP endpoint should not drag a dependency tree behind it.

MIT licensed. Source on [github.com/IoTone/jevracket](https://github.com/IoTone/jevracket).
