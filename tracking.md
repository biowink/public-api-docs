## Tracking

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

### Schema for various measurement types

Dates format is ISO 8601, always using hyphens to separate calendar dates and colons to separate time.
`date` in payload should be the calendar date for which the measurement is tracked (YYYY-MM-DD).
`captured_at` is when the measurement has been recorded by the user, in UTC time (YYYY-MM-DDThh:mm:ssZ).
`captured_at` field should be the UTC JSON datetime for _when_ the measurement was tracked.

* Bleeding
  * Heavy: `{"date":"2017-01-30", "type":"period", "body":"heavy"}`
  * Medium: `{"date":"2017-01-30", "type":"period", "body":"medium"}`
  * Light: `{"date":"2017-01-30", "type":"period", "body":"light"}`
  * Spotting: `{"date":"2017-01-30", "type":"period", "body":"spotting"}`
* Pain
  * Cramps: `{"date":"2017-01-30", "type":"cramps"}`
  * Headache: `{"date":"2017-01-30", "type":"headache"}`
  * Ovulation: `{"date":"2017-01-30", "type":"ovulation_pain"}`
  * Tender Breasts: `{"date":"2017-01-30", "type":"tender_breasts"}`
* Emotions
  * Happy: `{"date":"2017-01-30", "type":"happy"}`
  * Sensitive: `{"date":"2017-01-30", "type":"sensitive_emotion"}`
  * Sad: `{"date":"2017-01-30", "type":"sad"}`
  * PMS: `{"date":"2017-01-30", "type":"pms"}`
* Sex
  * Unprotected: `{"date":"2017-01-30", "type":"unprotected_sex"}`
  * Protected: `{"date":"2017-01-30", "type":"protected_sex"}`
  * High Sex Drive: `{"date":"2017-01-30", "type":"high_sex_drive"}`
  * Withdrawal: `{"date":"2017-01-30", "type":"withdrawal_sex"}`
* Energy
  * Energized: `{"date":"2017-01-30", "type":"energized"}`
  * High: `{"date":"2017-01-30", "type":"high_energy"}`
  * Low: `{"date":"2017-01-30", "type":"low_energy"}`
  * Exhausted: `{"date":"2017-01-30", "type":"exhausted"}`
