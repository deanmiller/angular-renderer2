# Renderer2

[docs](https://angular.io/api/core/Renderer2)

## Renderer2, what is it?
As you may know, Angular2+ was designed to be decoupled from the dom. This leads to a lot of wins like easier testing and server-sider rendering.

`Renderer2` (The `Renderer` class is deprecated, so we're using the latest and greatest with Renderer2) is a built-in Angular service that gives you some pretty nice abstractions for UI rendering and manipulation.

## Why use it instead of ViewChild?
You might be familiar with the `ViewChild` decorator, and how to use it to interact with native elements like a button or input.

example
```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
  selector: 'dope-app',
  template: '<input type="text" #input>'
})
export class AppComponent {
  @ViewChild('input') input;

  ngAfterContentInit() {
    this.input.nativeElement.focus();
  }
}
```

The above code will work perfectly when you run your application in a browser, but what if you want to run the same code in an environment that doesn't have a DOM? If you're doing any server-side rendering (Angular Universal), testing, or even mobile and desktop work, you'll run into issues. So what do we do?

You guessed it, we use `Renderer2`!

Here's a naive example of listening to changes on an element.
```
ngAfterViewInit() {
  this.touchmoveListener = this.renderer.listen('body', 'touchmove', (event) => {
    // do stuff
  })

  this.touchendListener = this.renderer.listen('body', 'touchend', (event) => {
    // do other stuff
  })
}
```
