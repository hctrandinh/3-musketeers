# Currency 

Currency, through the use of cli.js provides an effective way for users to quickly get their currency device conversion.

## Installation

To start using Currency, multiple libraries must be first installed. Just below is given all necessary steps:

```bash
cd ./currency
npm install jest
npm install nock
npm install axios
npm install money
npm install ora
```

## Usage
Using this converter is easy, for example if you want the value of 20 EUR converted into BTC, just do the following:

```bash
$ node cli.js 20 EUR BTC
```
And here is the result you will get :

```console
20 BTC = 155467.6 EUR
```

Note: You can find all ISO 4217 currency code checking this [link](https://en.wikipedia.org/wiki/ISO_4217).

## Code explanation
In this section, we will explain to you how the javascript code works in details.
First things first, we require libraries we need and slice the two first arguments when calling our program.
```javascript
const currency = require('./');
const ora = require('ora');
const argv = process.argv.slice(2);
```
We slice it because usually when you give arguments, this is what is done:
```bash
$ node argv.js one two three four five
[ 'node',
  '/home/avian/argvdemo/argv.js',
  'one',
  'two',
  'three',
  'four',
  'five' ]
```
We don't use the first two arguments and the last three are use to config our request with the amount you want to convert, the money you start from and finally the one you it to be converted into:
```javascript
const opts = {
  'amount': argv[0] || 1,
  'from': (argv[1] || 'USD').toUpperCase(),
  'to': (argv[2] || 'BTC').toUpperCase()
};
```
The configuration is then used with the start function which will display the result:
```javascript
async function start (opts) {
  try {
    const {amount, from, to} = opts;
    const result = await currency(opts);

    spinner.stop();
    console.log(`${amount} ${from} = ${result} ${to}`);
  } catch (error) {
    spinner.stop();
    console.log(error);
    process.exit(1);
  }
}
```

Note: you can also get an usage exemple by using the following help function:
```javascript
function help () {
  console.log(
    [
      '',
      '  Example',
      '    ❯ currency 1650 dkk eur',
      '    1650 DKK = 220.79486154 EUR',
      '',
      '  See README.md for detailed usage.'
    ].join('\n')
  );
}
```

## Testing
In order to test your currency functions, you need to enter the following line:
```bash
$ npm test
```

If everything goes well you should get the following output:
```bash
> currency@ test /Users/huan/Documents/3-musketeers/currency
> jest

 PASS  ./index.test.js
  currency
    ✓ should convert 1 USD to EUR (32ms)
    ✓ should convert 1 USD to USD (6ms)
    ✓ should convert 1 EUR to USD (7ms)
    ✓ should convert 1 BTC to USD (15ms)
    ✓ should convert 1 BTC to EUR (7ms)
    ✓ should convert (with default values) without arguments (9ms)
    ✓ should convert with amount only as argument (7ms)
    ✓ should convert with amount and (from) currency only as arguments (7ms)
    ✓ should return errors message for unknown `from` or `to` currency value (4ms)

  console.log index.js:26
    https://api.exchangeratesapi.io/latest?base=USD

  console.log index.js:26
    https://api.exchangeratesapi.io/latest?base=USD

  console.log index.js:26
    https://api.exchangeratesapi.io/latest?base=EUR

  console.log index.js:18
    BTC

  console.log index.js:19
    BTC

  console.log index.js:21
    USD

  console.log index.js:22
    BTC

  console.log index.js:26
    https://api.exchangeratesapi.io/latest?base=USD

  console.log index.js:18
    BTC

  console.log index.js:19
    BTC

  console.log index.js:21
    EUR

  console.log index.js:22
    BTC

  console.log index.js:26
    https://api.exchangeratesapi.io/latest?base=EUR

  console.log index.js:18
    USD

  console.log index.js:19
    USD

  console.log index.js:21
    USD

  console.log index.js:22
    USD

  console.log index.js:26
    https://api.exchangeratesapi.io/latest?base=USD

  console.log index.js:18
    USD

  console.log index.js:19
    USD

  console.log index.js:21
    USD

  console.log index.js:22
    USD

  console.log index.js:26
    https://api.exchangeratesapi.io/latest?base=USD

  console.log index.js:18
    EUR

  console.log index.js:19
    EUR

  console.log index.js:21
    EUR

  console.log index.js:22
    EUR

  console.log index.js:26
    https://api.exchangeratesapi.io/latest?base=EUR

  console.log index.js:26
    https://api.exchangeratesapi.io/latest?base=AIB

Test Suites: 1 passed, 1 total
Tests:       9 passed, 9 total
Snapshots:   0 total
Time:        1.061s, estimated 2s
Ran all test suites.
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

