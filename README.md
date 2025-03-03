<div align="center">
<h1>user-event</h1>

<a href="https://www.emojione.com/emoji/1f415">
  <img
    height="80"
    width="80"
    alt="dog"
    src="https://raw.githubusercontent.com/testing-library/user-event/master/other/dog.png"
  />
</a>

<p>Simulate user events for <a href="https://github.com/testing-library/react-testing-library">react-testing-library</a>.</p>

<br />
</div>

<hr />

[![Build Status](https://travis-ci.org/testing-library/user-event.svg?branch=master)](https://travis-ci.org/testing-library/user-event)
[![Maintainability](https://api.codeclimate.com/v1/badges/75f1ff4397e994c6004e/maintainability)](https://codeclimate.com/github/testing-library/user-event/maintainability)
[![Test Coverage](https://api.codeclimate.com/v1/badges/75f1ff4397e994c6004e/test_coverage)](https://codeclimate.com/github/testing-library/user-event/test_coverage)
[![All Contributors](https://img.shields.io/badge/all_contributors-8-orange.svg?style=flat-square)](#contributors)

## The problem

From
[testing-library/dom-testing-library#107](https://github.com/testing-library/dom-testing-library/issues/107):

> [...] it is becoming apparent the need to express user actions on a web page
> using a higher-level abstraction than `fireEvent`

## The solution

`user-event` tries to simulate the real events that would happen in the browser
as the user interacts with it. For example `userEvent.click(checkbox)` would
change the state of the checkbox.

**The library is still a work in progress and any help is appreciated.**

## Installation

With NPM:

```sh
npm install @testing-library/user-event --save-dev
```

With Yarn:

```sh
yarn add @testing-library/user-event --dev
```

Now simply import it in your tests:

```js
import userEvent from "@testing-library/user-event";

// or

var userEvent = require("@testing-library/user-event");
```

## API

### `click(element)`

Clicks `element`, depending on what `element` is it can have different side
effects.

```jsx
import React from "react";
import { render } from "@testing-library/react";
import userEvent from "@testing-library/user-event";

const { getByText, getByTestId } = test("click", () => {
  render(
    <div>
      <label htmlFor="checkbox">Check</label>
      <input id="checkbox" data-testid="checkbox" type="checkbox" />
    </div>
  );
});

userEvent.click(getByText("Check"));
expect(getByTestId("checkbox")).toHaveAttribute("checked", true);
```

### `dblClick(element)`

Clicks `element` twice, depending on what `element` is it can have different
side effects.

```jsx
import React from "react";
import { render } from "@testing-library/react";
import userEvent from "@testing-library/user-event";

test("double click", () => {
  const onChange = jest.fn();
  const { getByTestId } = render(
    <input type="checkbox" id="checkbox" onChange={onChange} />
  );
  const checkbox = getByTestId("checkbox");
  userEvent.dblClick(checkbox);
  expect(onChange).toHaveBeenCalledTimes(2);
  expect(checkbox).toHaveProperty("checked", false);
});
```

### `type(element, text, [options])`

Writes `text` inside an `<input>` or a `<textarea>`.

```jsx
import React from "react";
import { render } from "@testing-library/react";
import userEvent from "@testing-library/user-event";

const { getByText } = test("click", () => {
  render(<textarea data-testid="email" />);
});

userEvent.type(getByTestId("email"), "Hello, World!");
expect(getByTestId("email")).toHaveAttribute("value", "Hello, World!");
```

If `options.allAtOnce` is `true`, `type` will write `text` at once rather than
one character at the time. `false` is the default value.

`options.delay` is the number of milliseconds that pass between two characters
are typed. By default it's 0. You can use this option if your component has a
different behavior for fast or slow users.

### `selectOptions(element, values)`

Selects the specified option(s) of a `<select>` or a `<select multiple>`
element.

```jsx
import React from "react";
import { render } from "@testing-library/react";
import userEvent from "@testing-library/user-event";

const { getByTestId } = render(
  <select multiple data-testid="select-multiple">
    <option data-testid="val1" value="1">
      1
    </option>
    <option data-testid="val2" value="2">
      2
    </option>
    <option data-testid="val3" value="3">
      3
    </option>
  </select>
);

userEvent.selectOptions(getByTestId("select-multiple"), ["1", "3"]);

expect(getByTestId("val1").selected).toBe(true);
expect(getByTestId("val2").selected).toBe(false);
expect(getByTestId("val3").selected).toBe(true);
```

The `values` parameter can be either an array of values or a singular scalar
value.

## Contributors

Thanks goes to these wonderful people
([emoji key](https://github.com/all-contributors/all-contributors#emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore -->
<table><tr><td align="center"><a href="https://twitter.com/Gpx"><img src="https://avatars0.githubusercontent.com/u/767959?v=4" width="100px;" alt="Giorgio Polvara"/><br /><sub><b>Giorgio Polvara</b></sub></a><br /><a href="https://github.com/testing-library/user-event/issues?q=author%3AGpx" title="Bug reports">🐛</a> <a href="https://github.com/testing-library/user-event/commits?author=Gpx" title="Code">💻</a> <a href="https://github.com/testing-library/user-event/commits?author=Gpx" title="Documentation">📖</a> <a href="#ideas-Gpx" title="Ideas, Planning, & Feedback">🤔</a> <a href="#infra-Gpx" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a> <a href="#review-Gpx" title="Reviewed Pull Requests">👀</a> <a href="https://github.com/testing-library/user-event/commits?author=Gpx" title="Tests">⚠️</a></td><td align="center"><a href="https://github.com/weyert"><img src="https://avatars3.githubusercontent.com/u/7049?v=4" width="100px;" alt="Weyert de Boer"/><br /><sub><b>Weyert de Boer</b></sub></a><br /><a href="https://github.com/testing-library/user-event/commits?author=weyert" title="Code">💻</a> <a href="https://github.com/testing-library/user-event/commits?author=weyert" title="Tests">⚠️</a></td><td align="center"><a href="https://github.com/twhitbeck"><img src="https://avatars2.githubusercontent.com/u/762471?v=4" width="100px;" alt="Tim Whitbeck"/><br /><sub><b>Tim Whitbeck</b></sub></a><br /><a href="https://github.com/testing-library/user-event/issues?q=author%3Atwhitbeck" title="Bug reports">🐛</a> <a href="https://github.com/testing-library/user-event/commits?author=twhitbeck" title="Code">💻</a></td><td align="center"><a href="https://michaeldeboey.be"><img src="https://avatars3.githubusercontent.com/u/6643991?v=4" width="100px;" alt="Michaël De Boey"/><br /><sub><b>Michaël De Boey</b></sub></a><br /><a href="https://github.com/testing-library/user-event/commits?author=MichaelDeBoey" title="Documentation">📖</a></td><td align="center"><a href="https://github.com/michaellasky"><img src="https://avatars2.githubusercontent.com/u/6646599?v=4" width="100px;" alt="Michael Lasky"/><br /><sub><b>Michael Lasky</b></sub></a><br /><a href="https://github.com/testing-library/user-event/commits?author=michaellasky" title="Code">💻</a> <a href="https://github.com/testing-library/user-event/commits?author=michaellasky" title="Documentation">📖</a> <a href="#ideas-michaellasky" title="Ideas, Planning, & Feedback">🤔</a></td><td align="center"><a href="https://github.com/shomalgan"><img src="https://avatars0.githubusercontent.com/u/2883620?v=4" width="100px;" alt="Ahmad Esmaeilzadeh"/><br /><sub><b>Ahmad Esmaeilzadeh</b></sub></a><br /><a href="https://github.com/testing-library/user-event/commits?author=shomalgan" title="Documentation">📖</a></td><td align="center"><a href="https://calebeby.ml"><img src="https://avatars1.githubusercontent.com/u/13206945?v=4" width="100px;" alt="Caleb Eby"/><br /><sub><b>Caleb Eby</b></sub></a><br /><a href="https://github.com/testing-library/user-event/commits?author=calebeby" title="Code">💻</a> <a href="https://github.com/testing-library/user-event/issues?q=author%3Acalebeby" title="Bug reports">🐛</a></td></tr><tr><td align="center"><a href="https://afontcu.dev"><img src="https://avatars0.githubusercontent.com/u/9197791?v=4" width="100px;" alt="Adrià Fontcuberta"/><br /><sub><b>Adrià Fontcuberta</b></sub></a><br /><a href="https://github.com/testing-library/user-event/issues?q=author%3Aafontcu" title="Bug reports">🐛</a> <a href="https://github.com/testing-library/user-event/commits?author=afontcu" title="Tests">⚠️</a></td></tr></table>

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the
[all-contributors](https://github.com/all-contributors/all-contributors)
specification. Contributions of any kind welcome!
