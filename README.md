# Ember Page Objects

Represent the screens of your web app as a series of objects.

## References

* [Page Objects](https://code.google.com/p/selenium/wiki/PageObjects) - Selenium wiki
* [PageObject](http://martinfowler.com/bliki/PageObject.html) - Martin Fowler

## Usage

First add the npm package to your ember-cli project

```sh
npm install san650/ember-cli-page-object
npm install
```

Now you can reference `page-object` from your Acceptance tests

```js
import Ember from 'ember';
import { module, test } from 'qunit';
import startApp from '../helpers/start-app';
import PO from 'page-object';

var application;

module('An Integration test', {
  beforeEach: function() {
    application = startApp();
  },
  afterEach: function() {
    Ember.run(application, 'destroy');
  }
});

var login = PO.build({
  visit: PO.visitable('/login'),
  userName: PO.fillable('#username'),
  password: PO.fillable('#password'),
  submit: PO.clickable('#login'),
  errorMessage: PO.text('.message')
});

test('Invalid log in', function(assert) {
  login
    .visit()
    .userName('user@example.com')
    .password('secret')
    .submit();

  andThen(function() {
    assert.equal(login.errorMessage(), 'Invalid credentials!');
  });
});
```

## Development

### Installation

* `git clone` this repository
* `npm install`
* `bower install`

### Running

* `ember server`
* Visit your app at http://localhost:4200.

### Running Tests

* `ember test`
* `ember test --server`

### Building

* `ember build`

## License

ember-cli-page-object is licensed under the MIT license.

See LICENSE for the full license text.