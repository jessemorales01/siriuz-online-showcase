# Engineering Decisions (Selected)

## 1) Why Rails?
- Fast delivery, strong conventions, reliable ecosystem, clean MVC boundaries

## 2) How we kept business logic maintainable
- Service objects + clear domain boundaries
- Thin controllers, predictable data contracts

## 3) Reliability strategy
- Background jobs for non-blocking work
- Retries + idempotency for external calls
- Monitoring/alerts around critical workflows

## 4) Performance strategy
- Indexing + query tuning
- Caching where it improves UX
- Avoiding N+1s and excessive payloads
