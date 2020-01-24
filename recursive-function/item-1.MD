Write a function called power which takes in a base and an exponent. If the exponent is 0, return 1.

### Sample
```javascript
  SAMPLE:
  power(2, 4) // 16
  power(2, 3) // 8
  power(2, 2) // 4 
  power(2, 1) // 2
  power(2, 0) // 1
```

### Answer
```javascript
function power(base, exp) {
  if (exp === 0) return 1;
  return base * power(base, --exp);
}
```