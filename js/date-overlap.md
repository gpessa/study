## Exercise

You have time-stamps (mentioned as integers), which represents phone call begin and end to booking.com call center. find the number of overlaps in calls that suggests to add more call center agents.

#### Answer

```js
let calls = [
  {
    start: new Date(
      "Mon Feb 03 2020 17:42:04 GMT+0100 (Central European Standard Time)"
    ),
    end: new Date(
      "Mon Feb 03 2020 18:42:04 GMT+0100 (Central European Standard Time)"
    )
  },
  {
    start: new Date(
      "Mon Feb 03 2020 17:45:04 GMT+0100 (Central European Standard Time)"
    ),
    end: new Date(
      "Mon Feb 03 2020 22:42:04 GMT+0100 (Central European Standard Time)"
    )
  },
  {
    start: new Date(
      "Mon Feb 03 2020 17:45:04 GMT+0100 (Central European Standard Time)"
    ),
    end: new Date(
      "Mon Feb 03 2020 19:42:04 GMT+0100 (Central European Standard Time)"
    )
  },
  {
    start: new Date(
      "Mon Feb 03 2020 21:45:04 GMT+0100 (Central European Standard Time)"
    ),
    end: new Date(
      "Mon Feb 03 2020 22:42:04 GMT+0100 (Central European Standard Time)"
    )
  },
  {
    start: new Date(
      "Mon Feb 03 2020 05:45:04 GMT+0100 (Central European Standard Time)"
    ),
    end: new Date(
      "Mon Feb 03 2020 07:42:04 GMT+0100 (Central European Standard Time)"
    )
  }
];

function dateRangeOverlaps(a_start, a_end, b_start, b_end) {
  if (a_start <= b_start && b_start <= a_end) return true; // b starts in a
  if (a_start <= b_end && b_end <= a_end) return true; // b ends in a
  if (b_start < a_start && a_end < b_end) return true; // a in b
  return false;
}

let overlap = calls => {
  const callsInt = calls.map(({ start, end, id }) => ({
    start: start.getTime(),
    end: end.getTime()
  }));

  return callsInt.map(({ start, end, id }) => {
    const overlaps =
      callsInt.filter(otherCall =>
        dateRangeOverlaps(start, end, otherCall.start, otherCall.end)
      ).length - 1;

    return {
      start: new Date(start),
      end: new Date(end),
      overlaps
    };
  });
};

console.log(overlap(calls));
```
