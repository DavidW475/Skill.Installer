---
name: run-tests
description: "Run tests for the skill-installer Go project. Use when: running unit tests, checking test results, verifying build after code changes, running go vet, testing a specific package like internal/skill."
argument-hint: "Package to test, e.g. 'all' or 'internal/skill' or 'just build'"
metadata:
   version: "1.0.1"
---

# Run Tests — skill-installer

## What This Skill Does

Runs the Go test suite for the skill-installer project and reports results.

## Procedure

### 1. Build check
Always verify the project compiles before running tests:
```
go build ./...
```
If this fails, fix compile errors first.

### 2. Run all tests
```
go test ./...
```

### 3. Run a specific package
```
go test ./internal/skill/...
go test ./internal/config/...
go test ./internal/git/...
go test ./internal/tui/...
```

### 4. Run with verbose output
```
go test -v ./...
```

### 5. Run vet (static analysis)
```
go vet ./...
```

### 6. All in one
```
go build ./... && go vet ./... && go test ./... && echo "ALL OK"
```

## Test File Locations

| Package | Test file |
|---|---|
| `internal/skill` | `internal/skill/metadata_test.go`, `registry_test.go`, etc. |
| `internal/config` | `internal/config/config_test.go` |
| `internal/git` | `internal/git/generic_test.go` |

## After Adding New Code

1. Run `go build ./...` — must compile cleanly
2. Run `go test ./...` — all tests must pass
3. Run `go vet ./...` — no static analysis warnings
