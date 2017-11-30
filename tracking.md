## Tracking (read)

### Request format
To read tracking data
* Send a `GET`
* with an `Authorization` header
* and content-type as `application/json`
* to `https://api.helloclue.com/sync`

Optionally add `?sync_checkpoint=<datetime>`, where `<datetime>` is an ISO/JSON formatted timestamp, 
to only retrieve measurements stored after that point in time.

### Schema for the response body
```json
{
  "change_sets": {
    "measurements": [
      {"date":"2017-01-30", "type":"happy", "captured_at":"2017-01-30T09:49:00Z"}
    ]
  },
  "sync_checkpoint": "2017-01-30T09:59:00Z"
}
```

The `sync_checkpoint` refers to when the last returned measurement was inserted to the database.
By storing this checkpoint on the client and transmitting with following GET requests, this can 
be used to incrementally retrieve updated measurements.

See the Schemas section below for examples of how different measurements are formatted.


## Tracking (write)

### Request format
To send tracking data to clue
* Send a `POST`
* with an `Authorization` header
* and content-type as `application/json`
* with a JSON encoded body
* to `https://api.helloclue.com/sync`

### Schema for the request body
```json
{
  "change_sets": {
    "measurements": [
      {"date":"2017-01-30", "type":"happy", "captured_at":"2017-01-30T09:49:00Z"}
    ]
  }
}
```

PS: you can send multiple data-points in the `measurements` array

## Schema for various measurement types

Dates format is ISO 8601, always using hyphens to separate calendar dates and colons to separate time.
`date` in payload should be the calendar date for which the measurement is tracked (YYYY-MM-DD).
`captured_at` is when the measurement has been recorded by the user, in UTC time (YYYY-MM-DDThh:mm:ssZ).
`captured_at` field should be the UTC JSON datetime for _when_ the measurement was tracked.

* Bleeding
  * Heavy: `{"date":"2017-01-30", "type":"period", "body":"heavy", "captured_at":"2017-01-30T09:49:00Z"}`
  * Medium: `{"date":"2017-01-30", "type":"period", "body":"medium", "captured_at":"2017-01-30T09:49:00Z"}`
  * Light: `{"date":"2017-01-30", "type":"period", "body":"light", "captured_at":"2017-01-30T09:49:00Z"}`
  * Spotting: `{"date":"2017-01-30", "type":"period", "body":"spotting", "captured_at":"2017-01-30T09:49:00Z"}`
* Pain
  * Cramps: `{"date":"2017-01-30", "type":"cramps", "captured_at":"2017-01-30T09:49:00Z"}`
  * Headache: `{"date":"2017-01-30", "type":"headache", "captured_at":"2017-01-30T09:49:00Z"}`
  * Ovulation: `{"date":"2017-01-30", "type":"ovulation_pain", "captured_at":"2017-01-30T09:49:00Z"}`
  * Tender Breasts: `{"date":"2017-01-30", "type":"tender_breasts", "captured_at":"2017-01-30T09:49:00Z"}`
* Emotions
  * Happy: `{"date":"2017-01-30", "type":"happy", "captured_at":"2017-01-30T09:49:00Z"}`
  * Sensitive: `{"date":"2017-01-30", "type":"sensitive_emotion", "captured_at":"2017-01-30T09:49:00Z"}`
  * Sad: `{"date":"2017-01-30", "type":"sad", "captured_at":"2017-01-30T09:49:00Z"}`
  * PMS: `{"date":"2017-01-30", "type":"pms", "captured_at":"2017-01-30T09:49:00Z"}`
* Sex
  * Unprotected: `{"date":"2017-01-30", "type":"unprotected_sex", "captured_at":"2017-01-30T09:49:00Z"}`
  * Protected: `{"date":"2017-01-30", "type":"protected_sex", "captured_at":"2017-01-30T09:49:00Z"}`
  * High Sex Drive: `{"date":"2017-01-30", "type":"high_sex_drive", "captured_at":"2017-01-30T09:49:00Z"}`
  * Withdrawal: `{"date":"2017-01-30", "type":"withdrawal_sex", "captured_at":"2017-01-30T09:49:00Z"}`
* Energy
  * Energized: `{"date":"2017-01-30", "type":"energized", "captured_at":"2017-01-30T09:49:00Z"}`
  * High: `{"date":"2017-01-30", "type":"high_energy", "captured_at":"2017-01-30T09:49:00Z"}`
  * Low: `{"date":"2017-01-30", "type":"low_energy", "captured_at":"2017-01-30T09:49:00Z"}`
  * Exhausted: `{"date":"2017-01-30", "type":"exhausted", "captured_at":"2017-01-30T09:49:00Z"}`
