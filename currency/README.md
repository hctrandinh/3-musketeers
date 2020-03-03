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

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

