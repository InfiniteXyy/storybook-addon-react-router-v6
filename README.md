# Storybook Addon React Router v6
[![Storybook](https://raw.githubusercontent.com/storybookjs/brand/master/badge/badge-storybook.svg?sanitize=true)](https://storybook.js.org)
[![npm](https://img.shields.io/npm/v/storybook-addon-react-router-v6?color=blue)](https://www.npmjs.com/package/storybook-addon-react-router-v6)
[![Release](https://github.com/JesusTheHun/storybook-addon-react-router-v6/actions/workflows/release.yml/badge.svg)](https://github.com/JesusTheHun/storybook-addon-react-router-v6/actions/workflows/release.yml)

> Use React Router v6 in your stories.

## Getting Started
Install the package
 ```
 yarn add -D storybook-addon-react-router-v6
 ```
Add it to your storybook configuration:
```js
// .storybook/main.js
module.exports = {
    addons: ["storybook-addon-react-router-v6"],
};
```

## How to use it as a component decorator
To add the router to all the stories of a component, simply add it to the `decorators` array. 

Note that the `parameters.reactRouter` property is optional, by default the router will render the component at `/`.
```tsx
import { withRouter } from 'storybook-addon-react-router-v6';

export default {
  title: 'User Profile',
  component: UserProfile,
  decorators: [withRouter],
  parameters: {
    reactRouter: {
      routePath: '/users/:userId',
      routeParams: { userId: '42' },
    }
  }
};

export const Example = () => <UserProfile />;
```


## Usage at the story level
If you want to change the router config just for one story you can do the following :
```tsx
import { withRouter } from 'storybook-addon-react-router-v6';

export default {
  title: 'User Profile',
  component: UserProfile,
  decorators: [withRouter],
};

export const Example = () => <UserProfile />;
Example.story = {
  parameters: {
    reactRouter: {
      routePath: '/users/:userId',
      routeParams: { userId: '42' },
      searchParams: { tab: 'activityLog' }
    }
  }
};
```
## Define a global default
If you want you can wrap all your stories inside a router by adding the decorator in your `preview.js` file.
```ts
// preview.js

export const decorators = [withRouter];

// you can also define global defaults parameters
export const parameters = {
  reactRouter: {
    // ...
  }
}
```
