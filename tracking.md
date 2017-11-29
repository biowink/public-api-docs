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
      {"date":"2017-1-1", "type":"happy", "captured_at":"2017-01-01T00:00:00Z"}
    ]
  }
}
```


PS: you can send multiple data-points in the `measurements` array

### Schema for various measurement types

The `date` in payload should be the date for which the measurement is tracked.
The `captured_at` field should be the UTC JSON datetime for _when_ the measurement was tracked.

* Bleeding
  * Heavy: `{"date":"2016-1-1", "type":"period", "body":"heavy"}`
  * Medium: `{"date":"2016-1-1", "type":"period", "body":"medium"}`
  * Light: `{"date":"2016-1-1", "type":"period", "body":"light"}`
  * Spotting: `{"date":"2016-1-1", "type":"period", "body":"spotting"}`
* Pain
  * Cramps: `{"date":"2016-1-1", "type":"cramps"}`
  * Headache: `{"date":"2016-1-1", "type":"headache"}`
  * Ovulation: `{"date":"2016-1-1", "type":"ovulation_pain"}`
  * Tender Breasts: `{"date":"2016-1-1", "type":"tender_breasts"}`
* Emotions
  * Happy: `{"date":"2016-1-1", "type":"happy"}`
  * Sensitive: `{"date":"2016-1-1", "type":"sensitive_emotion"}`
  * Sad: `{"date":"2016-1-1", "type":"sad"}`
  * PMS: `{"date":"2016-1-1", "type":"pms"}`
* Sex
  * Unprotected: `{"date":"2016-1-1", "type":"unprotected_sex"}`
  * Protected: `{"date":"2016-1-1", "type":"protected_sex"}`
  * High Sex Drive: `{"date":"2016-1-1", "type":"high_sex_drive"}`
  * Withdrawal: `{"date":"2016-1-1", "type":"withdrawal_sex"}`
* Energy
  * Energized: `{"date":"2016-1-1", "type":"energized"}`
  * High: `{"date":"2016-1-1", "type":"high_energy"}`
  * Low: `{"date":"2016-1-1", "type":"low_energy"}`
  * Exhausted: `{"date":"2016-1-1", "type":"exhausted"}`

