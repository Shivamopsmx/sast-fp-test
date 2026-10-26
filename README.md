# sast-fp-test

A tiny deliberately-insecure Python app used to exercise the SAST false-positive
pipeline. Each file under `app/` contains one pattern a SAST scanner
(Semgrep/Opengrep) will flag. Some are genuinely exploitable (true positives); a
couple are flagged-but-safe (false positives) so the FP agent has real decisions
to make.

**Do not deploy. For security-tooling testing only.**

| File | Pattern | Intent |
|------|---------|--------|
| app/sqli.py | SQL injection (string-formatted query) | true positive |
| app/cmdi.py | Command injection (shell + user input) | true positive |
| app/deserialize.py | Unsafe YAML/pickle load | true positive |
| app/ssrf.py | SSRF (user-controlled URL) | true positive |
| app/path_traversal.py | Path traversal (open user path) | true positive |
| app/secrets.py | Hardcoded password | true positive |
| app/weak_hash.py | MD5 used as a non-security cache key | likely false positive |
| app/eval_const.py | eval() of a hardcoded constant | likely false positive |
