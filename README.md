Decorators are a fundamental concept in TypeScript, and because Angular heavily relies on TypeScript, decorators have become an important element of Angular as well.

Decorators are methods or design patterns that are labeled with a prefixed @ symbol and preceded by a class, method, or property. They enable the modification of a service, directive, or filter before it is utilized. A decorator, in essence, provides configuration metadata that specifies how a component, class, or method should be processed, constructed, and used at runtime. Angular includes a number of decorators which attach various types of metadata to classes, allowing the system to understand what all these classes signify and how they should function.

Types of decorators:

Method Decorator: Method decorators, as the name implies, are used to add functionality to the methods defined within our class.
Class Decorator: Class Decorators are the highest-level decorators that determine the purpose of the classes. They indicate to Angular that a specific class is a component or module. And the decorator enables us to declare this effect without having to write any code within the class.
Parameter Decorator: The arguments of your class constructors are decorated using parameter decorators.
Property Decorator: These are the second most popular types of decorators. They enable us to enhance some of the properties in our classes.



Class Decorators
These are applied to classes, and they tell Angular what kind of object the class represents.

a) @Component
Defines a component.

ts

import { Component } from '@angular/core';

@Component({
  selector: 'app-hello',
  template: `<h1>Hello, {{ name }}</h1>`
})
export class HelloComponent {
  name = 'Angular';
}
b) @Directive
Defines a directive (custom behavior for elements).

ts

import { Directive, ElementRef } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  constructor(el: ElementRef) {
    el.nativeElement.style.backgroundColor = 'yellow';
  }
}
c) @Pipe
Creates a custom pipe for transforming data in templates.

ts

import { Pipe, PipeTransform } from '@angular/core';

@Pipe({ name: 'capitalize' })
export class CapitalizePipe implements PipeTransform {
  transform(value: string): string {
    return value.charAt(0).toUpperCase() + value.slice(1);
  }
}
d) @NgModule
Defines a module that can bundle components, pipes, and services.

ts

import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

@NgModule({
  declarations: [HelloComponent],
  imports: [BrowserModule],
  bootstrap: [HelloComponent]
})
export class AppModule {}

2. 🧩 Property Decorators
Used to decorate class properties (fields) — especially for inputs, outputs, or dependency injection.

a) @Input()
Marks a property as a component input.

ts

import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-user',
  template: `<p>User: {{ name }}</p>`
})
export class UserComponent {
  @Input() name: string;
}
b) @Output()
Marks a property as an event emitter to parent components.

ts

import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-button',
  template: `<button (click)="send()">Click</button>`
})
export class ButtonComponent {
  @Output() clicked = new EventEmitter<string>();

  send() {
    this.clicked.emit('Button clicked!');
  }
}
c) @ViewChild() / @ViewChildren()
Access child elements or components in the template.

ts

@ViewChild('inputRef') input;

ngAfterViewInit() {
  console.log(this.input.nativeElement.value);
}
d) @ContentChild() / @ContentChildren()
Access content projected inside <ng-content>.

3. ⚙️ Method & Parameter Decorators
Used on methods or constructor parameters, usually for dependency injection.

a) @Inject()
Manually specify a dependency to inject.

ts

import { Inject } from '@angular/core';

constructor(@Inject('API_URL') private apiUrl: string) {}
b) @HostListener()
Listens to DOM events on the host element.

ts

@HostListener('click')
onClick() {
  console.log('Element clicked');
}
c) @HostBinding()
Binds a host element property to a class property.

ts
Copy
Edit
@HostBinding('class.active') isActive = true;
