# AI Experts Assignment (Python)

This assignment demonstrates the ability to:

* run a Python project reliably (locally and in Docker),
* pin dependencies for reproducible environments,
* write tests that expose a real bug,
* apply a minimal and reviewable fix.

---

## Project Tasks

### 1. Dockerfile

A `Dockerfile` is provided so the test suite can run in a clean, non-interactive environment.

Requirements satisfied:

* Dependencies are installed from `requirements.txt`
* Dependencies are pinned
* Tests run automatically using pytest

---

### 2. requirements.txt

All dependencies are pinned using the format:

```
package==x.y.z
```

This ensures reproducible installations across environments.

---

### 3. Bug Identification and Fix

A bug was identified in the `Client.request()` method where OAuth tokens stored as dictionaries were not handled correctly.

The refresh logic only checked for missing tokens or expired `OAuth2Token` objects. When the token was stored as a dictionary, the expiration check was skipped and the authorization header was never set.

The fix ensures that dictionary tokens are treated as invalid tokens and refreshed properly.

---

## Running Tests Locally

1. Create a virtual environment

```
python -m venv venv
```

2. Activate the environment

Windows:

```
venv\Scripts\activate
```

3. Install dependencies

```
pip install -r requirements.txt
```

4. Run the tests

```
pytest -v
```

---

## Running Tests with Docker

### Build the Docker image

```
docker build -t ai-experts-assignment .
```

### Run the tests

```
docker run ai-experts-assignment
```

---

## Repository Structure

```
app/
    http_client.py
    tokens.py

tests/
    test_http_client.py

Dockerfile
requirements.txt
README.md
EXPLANATION.md
```

---

## Notes

* The fix was implemented with the smallest possible code change.
* No unrelated refactoring was introduced.
* All existing tests pass successfully.
