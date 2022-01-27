# Dialog

AgnosticUI's [Dialog](https://www.w3.org/TR/wai-aria-practices/#dialog_modal) component wraps Kitty Giraudel's [a11y-dialog](https://github.com/KittyGiraudel/a11y-dialog) — an accessible and inclusive dialog component that has been battle tested over several versions to date.

<div class="mbs24"></div>

## Examples

<div class="mbe24"></div>

<DialogExamples />

<script>
import DialogExamples from '../../components/DialogExamples.vue'
import { Alert } from "agnostic-vue";

export default {
  components: { Alert, DialogExamples }
}
</script>

<div class="mbe32"></div>

## Usage

<Alert type="warning">Documentation below for Angular, and Svelte are incomplete but coming soon!</Alert>

<div class="flex">
  <h3 id="react" tabindex="-1">
    <img src="/images/React-icon.svg" alt="react logo">React
  </h3>
</div>

```jsx
import { useRef } from 'react';
import "agnostic-react/dist/common.min.css";
import "agnostic-react/dist/esm/index.css";
import { Dialog } from "agnostic-react";

export const YourComponent = () => {
  const dialog = useRef();
  const dialog2 = useRef();
  const dialogPropsDefault = {
    id: 'ag-dialog-test',
    title: 'Dialog Test',
    classNames: {
      // Note we don't have to pass in ALL classNames props and those
      // not included will fallback to react-a11y-dialog's defaults
      // See https://github.com/KittyGiraudel/react-a11y-dialog#api
      title: 'h3 mbe18 h4 mbe18 flex justify-center',
    }
  };
  return {
    <>
      <div className="mbs16 mbe24">
        <Button onClick={() => dialog.current.show()} type="button" mode="primary" isBordered isRounded isBlock>Open the dialog</Button>
        <Dialog
          {...dialogPropsDefault}
          dialogRef={dialogInstance => (dialog.current = dialogInstance)}
          isAnimationSlideUp={true}
        >
          <p className="mbs16 mbe16" id="dialog-example-description">
            Fill in the form below to receive our newsletter!
          </p>
          <form className="dialog-form-demo">
            <Input isRounded label="Email (required)" type="email" name="EMAIL" id="email" placeholder="email@example.com" required />
            <div className="mbe16" />
            <Button type="submit" mode="primary" isRounded isBlock>Sign Up</Button>
          </form>
        </Dialog>
      </div>
      <div className="mbs16 mbe24">
        <Button onClick={() => dialog2.current.show()} type="button" mode="primary" isBordered isRounded isBlock>Open dialog 2</Button>
        <Dialog
          {...dialogPropsDefault}
          id="dialog-2"
          title="Dialog — Custom Close Button"
          dialogRef={instance => (dialog2.current = instance)}
          classNames={{ title: 'h4 mbe18', closeButton: 'close-button-demo' }}
          isAnimationFadeIn
          isAnimationSlideUp
          closeButtonPosition="last"
          closeButtonContent={<Button type="faux" isRounded isBordered isBlock>Cancel</Button>}
        >
          <p className="mbs16 mbe16" id="dialog-example-description">
            The <code>close-button-demo</code> class is in App.css (for the Cancel button at bottom).
            Otherwise, we use an AgnosticUI button of <code>type="faux</code> which generates a div that
            looks like a button. As <code>react-a11y-dialog</code> generates its own button
            around <code>closeButtonContent</code>, this prevents an unwanted nested buttons situation.
          </p>
          <p className="mbe16">You'll also notice that this dialog did not &ldquo;slide up&rdquo; as we have not
          passed in true to <code>isAnimationSlideUp</code> and this animation defaults to false. The other animation
          is <code>isAnimationFadeIn</code> which defaults to true. You can set it <code>false</code> if you wish to
          remove it.
          </p>
          <form className="dialog-form-demo">
            <Input isRounded label="Email (required)" type="email" name="EMAIL" id="email" placeholder="email@example.com" required />
            <div className="mbe16" />
            <Button type="submit" mode="primary" isRounded isBlock>Sign Up</Button>
          </form>
        </Dialog>
      </div>
    </>
  }
}
```

React: [component source](https://github.com/AgnosticUI/agnosticui/blob/master/agnostic-react/src/Dialog.tsx)

<div class="mbe32"></div>

<div class="flex">
  <h3 id="vue-3" tabindex="-1">
    <img src="/images/Vue-icon.svg" alt="Vue 3 logo">Vue 3
  </h3>
</div>

```vue
<script>
import "agnostic-vue/dist/common.min.css";
import "agnostic-vue/dist/index.css";
import { Button, Dialog, Input } from "agnostic-vue";

export default {
  name: "DialogExamples",
  components: {
    Button,
    Dialog,
    Input,
  },
  setup() {
    let dialog = null;
    const openDialog = () => {
      if (dialog) {
        dialog.show();
      }
    };

    const assignDialogRef = (instance) => {
      dialog = instance;
    };

    return {
      openDialog,
      assignDialogRef,
    };
  },
};
</script>
<template>
  <section>
    <h3>Dialog</h3>
    <p class="mbe24">
      The following opens because we've registered a dialog <code>instance</code> ref via <code>@instance="assignDialogRef"</code>. This is Vue syntax but the other framework implementations offer similar means:
    </p>
    <Button
      mode="primary"
      :is-bordered="true"
      :is-block="true"
      :is-rounded="true"
      type="button"
      @click="openDialog"
    >
      Open dialog via dialogRef
    </Button>
    <p class="mbs24 mbe16">
      The following also opens because a11y-dialog will bind to element with <code>data-a11y-dialog-show</code> attribute:
    </p>
    <button />
    <Button
      type="button"
      data-a11y-dialog-show="a11y-dialog"
      mode="primary"
      :is-bordered="true"
      :is-block="true"
      :is-rounded="true"
    >
      Open the dialog via data attribute
    </Button>
    <Dialog
      id="a11y-dialog"
      dialog-root="body"
      :is-animation-fade-in="true"
      :is-animation-slide-up="true"
      role="dialog"
      :class-names="{
        title: 'h4 mbe18 flex justify-center',
      }"
      @instance="assignDialogRef"
    >
      <template #title>
        My Dialog
      </template>
      <p class="mbs16 mbe16">
        Fill in the form below to receive our newsletter!
      </p>
      <form class="dialog-form-demo">
        <Input
          :is-rounded="true"
          label="Email (required)"
          type="email"
          name="EMAIL"
          id="email"
          placeholder="email@example.com"
          required
        />
        <div class="mbe16" />
        <Button
          type="submit"
          mode="primary"
          :is-rounded="true"
          :is-block="true"
        >
          Sign Up
        </Button>
      </form>
    </Dialog>
  </section>
</template>
```

Vue 3: [component source](https://github.com/AgnosticUI/agnosticui/blob/master/agnostic-vue/src/components/Dialog.vue)

<div class="mbe24"></div>

<Alert type="warning">Note: Vue 2 is not supported</Alert>

<div class="mbe32"></div>

<div class="flex">
  <h3 id="angular" tabindex="-1">
    <img src="/images/Angular-icon.svg" alt="Angular logo">Angular
  </h3>
</div>

In your Angular configuration (likely `angular.json`) ensure you're including
the common AgnosticUI styles:

<div class="mbe16"></div>

` "styles": ["agnostic/dist/common.min.css"],`

<div class="mbe24"></div>

Add AgnosticUI's `AgModule` module:

```js{3,9}
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AgModule } from 'agnostic-angular';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, AgModule],
  providers: [],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

Now you can use in your components:

```js
import { Component } from '@angular/core';

@Component({
  selector: 'your-component',
  template: `TBD`
})
export class YourComponent {}
```


Angular: [component source](https://github.com/AgnosticUI/agnosticui/blob/master/agnostic-angular/libs/ag/src/lib/dialog.component.ts)

<div class="mbe32"></div>

<div class="flex">
  <h3 id="svelte" tabindex="-1">
    <img src="/images/Svelte-icon.svg" alt="Svelte logo">Svelte
  </h3>
</div>

```html
<script>
  import 'agnostic-svelte/dist/common.min.css';
  import { Dialog } from "agnostic-svelte";
</script>
TBD
```

Svelte: [component source](https://github.com/AgnosticUI/agnosticui/blob/master/agnostic-svelte/src/lib/components/Dialog/Dialog.svelte)

## Storybook

You can run the framework Storybooks and see live examples for React, Vue 3, Angular, and Svelte. The following will set this up locally:

```shell
git clone git@github.com:AgnosticUI/agnosticui.git
cd agnosticui && yarn
# You can then run any of the top-level scripts:
yarn start:react # or
yarn start:vue # or
yarn start:angular # or
yarn start:svelte
```

See [Running monorepo](https://github.com/AgnosticUI/agnosticui/blob/master/CONTRIBUTING.md#running-monorepo).