# NRSuite Docs

Official documentation and resources for the NRSuite Android app and ESP32
firmware.

## Local preview

```bash
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install -r requirements.txt
mkdocs serve
```

Open <http://127.0.0.1:8000/>.

## Build

```bash
mkdocs build --strict
```

The generated site is written to `site/`.

## GitHub Pages

The workflow in `.github/workflows/pages.yml` builds and deploys the site when
`main` is updated.

> Authorized testing only. Use NRSuite only on devices and networks you own or
> have explicit written permission to test.
