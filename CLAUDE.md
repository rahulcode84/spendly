# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Spendly — a Flask expense tracker ("Track every rupee"). It is a step-by-step teaching project: unfinished features are stubbed with placeholder responses like `"... — coming in Step N"`, and the step number tells you what is meant to be built there.

## Commands

```
pip install -r requirements.txt   # flask, werkzeug, pytest, pytest-flask
python app.py                     # dev server, debug mode, http://localhost:5001
pytest                            # run tests (no tests/ directory exists yet)
pytest tests/test_x.py::test_name # run a single test
```

There is no build or lint configuration.

## Architecture

- `app.py` is the single Flask app: all routes live here and render Jinja templates. Real routes: `/`, `/terms`, `/privacy`, `/register`, `/login` (the last two only render the form templates; no POST handling yet). The rest (`/logout`, `/profile`, `/expenses/add`, `/expenses/<id>/edit`, `/expenses/<id>/delete`) are placeholders returning plain strings.
- `database/db.py` is intentionally a stub (Step 1). Its header comment specifies the contract: `get_db()` returns a SQLite connection with `row_factory` set and foreign keys enabled; `init_db()` creates tables with `CREATE TABLE IF NOT EXISTS`; `seed_db()` inserts development sample data. `app.py` does not import it yet.
- Templates all extend `templates/base.html` (navbar, footer, Google Fonts, `css/style.css`, `js/main.js`). Pages add page-specific CSS through the `head` block (e.g. `landing.html` loads `css/landing.css`) and JS through the `scripts` block.
- Use `url_for(...)` for links in templates. The footer Terms/Privacy links in `base.html` are currently hardcoded paths.

## Notes

- Dependencies are pinned in `requirements.txt`; `werkzeug` is included for password hashing in the upcoming auth steps.
- `file.txt` and the screenshot in the repo root are scratch files, not part of the app.
- Commits follow a `landing: <summary>` style prefix for landing-page work.
