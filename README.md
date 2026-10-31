# NetMap notices

NetMap installs read `notices.json` from this repository every 6 hours and show any notice that matches their version. Nothing about the install is sent; it is a plain HTTPS GET of the raw file.

## Format

```json
{
  "notices": [
    {
      "id": "v2-postgres",
      "severity": "breaking",
      "title": "NetMap 2.0 moves to PostgreSQL",
      "message": "Back up your database before upgrading to 2.0.",
      "link": "https://github.com/xoriin/netmap/releases",
      "show_from": "1.8.0",
      "show_below": "2.0.0",
      "starts": "2026-11-01",
      "ends": "2027-06-30"
    }
  ]
}
```

| Field | Required | Notes |
|---|---|---|
| `id` | yes | Lowercase letters, numbers and dashes, up to 64. Never reuse one: dismissals and acknowledgements are stored by id. |
| `severity` | no | `info` (default), `warning` or `breaking`. |
| `title` | yes | Up to 120 characters. |
| `message` | yes | Up to 1000 characters, plain text. |
| `link` | no | `https://` only. |
| `show_from` | no | Show to versions at or above this, e.g. `1.8.0`. |
| `show_below` | no | Show to versions below this, e.g. `2.0.0`. |
| `starts` / `ends` | no | Dates, `YYYY-MM-DD`, inclusive. |

- `info` and `warning` show to every user until they dismiss them.
- `breaking` shows only to SuperAdmins, until one of them acknowledges it.
- An invalid entry is skipped; the rest of the file still loads. At most 20 notices and 64 KB.
- An empty list (`"notices": []`) shows nothing.
