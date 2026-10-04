# TimeTree Sync Action

Personal TimeTree -> Google Calendar synchronization using GitHub Actions.

This repository uses the community project `timetree-exporter` to read TimeTree's web data and Google Calendar API to mirror events.

## Secrets

Configure these under Settings -> Secrets and variables -> Actions:

- `TIMETREE_EMAIL`
- `TIMETREE_PASSWORD`
- `TIMETREE_CALENDAR_CODE`
- `GOOGLE_SERVICE_ACCOUNT_JSON`
- `GOOGLE_CALENDAR_ID`

## Google setup

1. Create a Google Cloud project.
2. Enable Google Calendar API.
3. Create a service account and JSON key.
4. Create a dedicated Google Calendar named `TimeTree`.
5. Share that calendar with the service-account email with permission to modify events.
6. Put the calendar ID into `GOOGLE_CALENDAR_ID`.

## TimeTree calendar code

`TIMETREE_CALENDAR_CODE` is the TimeTree calendar alias code. It is visible in the TimeTree calendar URL and can also be obtained from TimeTree Exporter.

## Sync behavior

- TimeTree event created -> Google event created
- TimeTree event changed -> Google event updated
- TimeTree event deleted -> mirrored Google event deleted
- Native Google Calendar events are ignored
- Events are tagged with private Google extended properties to avoid duplicates

The workflow runs every 15 minutes and can also be run manually from Actions.

## Important

TimeTree no longer provides its former public Connect App API. `timetree-exporter` uses unofficial/reverse-engineered TimeTree web APIs, so this integration can break if TimeTree changes its web implementation. Keep request frequency reasonable.

## License

MIT. See LICENSE and NOTICE.
