# Welcome to PowerDale

PowerDale is a small town with around 100 residents. Most houses have a smart meter installed that can save and send information about how much power a house is drawing/using.

There are three major providers of energy in town that charge different amounts for the power they supply.

- _Dr Evil's Dark Energy_
- _The Green Eco_
- _Power for Everyone_

# Introducing JOI Energy

JOI Energy is a new start-up in the energy industry. Rather than selling energy they want to differentiate themselves from the market by recording their customers' energy usage from their smart meters and recommending the best supplier to meet their needs.

You have been placed into their development team, whose current goal is to produce an API which their customers and smart meters will interact with.

## Users

To trial the new JOI software 5 people from the JOI accounts team have agreed to test the service and share their energy
data.

| User    | Smart Meter ID  | Power Supplier        |
| ------- | --------------- | --------------------- |
| Sarah   | `smart-meter-0` | Dr Evil's Dark Energy |
| Peter   | `smart-meter-1` | The Green Eco         |
| Charlie | `smart-meter-2` | Dr Evil's Dark Energy |
| Andrea  | `smart-meter-3` | Power for Everyone    |
| Alex    | `smart-meter-4` | The Green Eco         |

These values are used in the code and in the following examples too.

## Requirements

The project requires [Node v14](https://nodejs.org/).

## Useful Node commands

The project makes use of node and its package manager to help you out carrying some common tasks such as building the
project or running it.

### Install dependencies

```console
$ npm install
```

### Run the tests

There are two options to run the tests

- Run the tests once

  ```console
  $ npm test
  ```

- Keep running the tests with every change

  ```console
  $ npm run test-watch
  ```

### Run the application

Run the application which will be listening on port `8080`. There are two ways to run the application.

- Run the application with the current code

  ```console
  $ npm start
  ```

- Run the application with reload on save

  ```console
  $ npm run dev
  ```

## More information 

* [API documentation](docs/api-documentation.md)