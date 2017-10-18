## Cycles

### Request format
To get the user cycles
* Send a `GET`
* with an `Authorization` header
* to `https://api.helloclue.com/cycles`

### Schema for the response body
```json
{
  "cycles": [
    {
      "start": "2017-10-16",
      "end": "2017-11-13",
      "length": 29,
      "phases":[
        {
          "type": "fertile_window",
          "start": "2017-10-27",
          "end": "2017-11-01",
          "length": 6,
          "body": {
            "ovulation_date": "2017-10-31"
          }
        },
        {
          "type": "period",
          "start": "2017-10-16",
          "end": "2017-10-19",
          "length": 4
        },
        {
          "type": "pms",
          "start": "2017-11-10",
          "end": "2017-11-12",
          "length": 2
        }
      ],
      "completed": false,
      "isValid": true,
      "predicted": false
    },
    {
      "start": "2017-11-14",
      "end": "2017-12-12",
      "length": 29,
      "phases":[
        {
          "type": "fertile_window",
          "start": "2017-11-25",
          "end": "2017-11-30",
          "length": 6,
          "body": {
            "ovulation_date": "2017-11-29"
          }
        },
        {
          "type": "period",
          "start": "2017-11-14",
          "end": "2017-11-17",
          "length": 4
        }
      ],
      "completed": false,
      "isValid": false,
      "predicted": true
    }
  ]
}
```

`cycles` is an array containing all of the cycles of a user in chronological order. For new users, this array can be empty. Otherwise, it will contain the completed cycles, the current cycle and 3 predicted cycles.

A cycle has the following flags:
* `"completed"` is `true` for cycles who ended already, `false` otherwise
* `"isValid"` is `false` for the very first cycle of the user in case it doesn't start with a period phase, `true` otherwise
* `"predicted"` is `true` for cycles starting in the future, `false` otherwise

A cycle also has an array of `phases`. This array can be empty, or contain phases of different types. The possible phase types are `"period"`, `"fertile_window"`, `"pms"` and `"unprotected"`.

All `fertile_window` phases expose an `ovulation_date` as part of their body.
