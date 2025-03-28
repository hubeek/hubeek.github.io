# Angular

_Status: Published_
_Created: 2020-01-10 08:51:44_
_Tags: javascript, angular_

##install angular cli
```
nom i angular-cli
```
##create new project
```
ng new <project-name>
```
##start proj
```
ng serve
ng s
```
##generate component
```
ng g c <optional-folder/component-name>
```
##component field - html prop
###two way binding
```
<my-cmp [(title)]="name">
```
###in component.ts  
selector decorator:
```
@Component({
  selector: '.app-servers',
...
})
```
in html:
```
<!--selector "app-servers"-->
<app-servers></app-servers>

<!--selector "[app-server]" as attribute-->
<div app-servers></div>

<!--selector ".app-server" as className-->
<div class="app-servers"></div>

```
varname: type, ex: name: string;  
or object (define class in folder models, like ObjectClass class { var a: number; }):  
objectclass: ObjectClass    
###in .html  
{{varname}} , ex: {{name}}  
{{objectclass.a}}  

##component input @input()
```
<input [value]="my_name">
```
in parent-component .html  
```
<component-name [name]="my_name" ....  
```
in component-name .ts
```
export component-name class {

@Input()
name: string;
...
}
```

##events
in component .html
```
<button (click)="functionname($event)">button title</button>
```
in .ts  
create function functionname($event)   
```
export class ComponentClass {  
  ...  
  constructor(){}  
  ...  
 functionname(event: any) {  
  //do something  
  }  
  ...  
}  
```
## Attribute Directives

```
<p appHighlight>Highlight me!</p>
```

ng g directive <directive-name>

to use it like [appClass] style of writing:
```
<li class="page-item"
        [appClass]="{'disabled':currentPage===images.length-1}">
</li>
```
```
import { Directive, ElementRef, Input } from '@angular/core';

@Directive({
  selector: '[appClass]'
})
export class ClassDirective {

  constructor(private element: ElementRef) { }

  @Input('appClass') set classNames(classObj: any) {
    for (const key in classObj) {
      if (classObj[key]) {
        this.element.nativeElement.classList.add(key);
      } else {
        this.element.nativeElement.classList.remove(key);

      }
    }
  }
}

```

##Structural Directives
###What are structural directives?  
  
Structural directives are responsible for HTML layout. They shape or reshape the DOM's structure, typically by adding, removing, or manipulating elements.  
As with other directives, you apply a structural directive to a host element. The directive then does whatever it's supposed to do with that host element and its descendants.  
Structural directives are easy to recognize. An asterisk (*) precedes the directive attribute name as in this example.  
```
<div *ngIf="hero" class="name">{{hero.name}}</div>
```
The three common structural directives are **ngIf ngFor ngSwitch**
    
## struct directive creation
```
ng g directive <directive-name>
```
to use like *appTimes

```
<ul *appTimes="5">
  <li>hi there!</li>
</ul>
```

```
import { Directive, TemplateRef, ViewContainerRef, Input } from '@angular/core';
// structural directive
@Directive({
  selector: '[appTimes]'
})
export class TimesDirective {

  constructor(
    private viewContainer: ViewContainerRef,
    private templateRef: TemplateRef<any>
  ) { }

  @Input('appTimes') set render(times: number) {
    this.viewContainer.clear();

    for (let i = 0 ; i < times; i++) {
      this.viewContainer.createEmbeddedView(this.templateRef, {
        index: i
      });
    }
  }
}

```

##ngFor
```
<ul>  
  <li *ngFor="let item of items; index as i">  
    {{i+1}} {{item}}  
  </li>  
</ul>  
  
```
The following exported values can be aliased to local variables:  
- $implicit: T: The value of the individual items in the iterable (ngForOf).  
- ngForOf: NgIterable<T>: The value of the iterable expression. Useful when the expression is more complex then a property access, for example when using the async pipe (userStreams | async).  
- **index**: number: The index of the current item in the iterable.  
- **first**: boolean: True when the item is the first item in the iterable.  
- **last**: boolean: True when the item is the last item in the iterable.  
- **even**: boolean: True when the item has an even index in the iterable.  
- **odd**: boolean: True when the item has an odd index in the iterable.  

##ngIf
shorthand
```
<div *ngIf="condition">Content to render when condition is true.</div>
```
extended
```
<ng-template [ngIf]="condition"><div>Content to render when condition is true.</div></ng-template>  
```
with else block
```
<div *ngIf="condition; else elseBlock">Content to render when condition is true.</div>  
<ng-template #elseBlock>Content to render when condition is false.</ng-template>  
```
if then else
```
<div *ngIf="condition; then thenBlock else elseBlock"></div>  
<ng-template #thenBlock>Content to render when condition is true.</ng-template>  
<ng-template #elseBlock>Content to render when condition is false.</ng-template>  
```
with value locally
```
<div *ngIf="condition as value; else elseBlock">{{value}}</div>  
<ng-template #elseBlock>Content to render when value is null.</ng-template>  
```
else in template, use #<templatename>
```
<div class="hero-list" *ngIf="heroes else loading">  
 ...   
</div>  
   
<ng-template #loading>  
 <div>Loading...</div>  
</ng-template>
```
##ngClass
Adds and removes CSS classes on an HTML element.  
  
The CSS classes are updated as follows, depending on the type of the expression evaluation:  
string - the CSS classes listed in the string (space delimited) are added,  
Array - the CSS classes declared as Array elements are added,  
Object - keys are CSS classes that get added when the expression given in the value evaluates to a truthy value, otherwise they are removed.  
```
<some-element [ngClass]="'first second'">...</some-element>  

<some-element [ngClass]="['first', 'second']">...</some-element>  

<some-element [ngClass]="{'first': true, 'second': true, 'third': false}">...</some-element>  

<some-element [ngClass]="stringExp|arrayExp|objExp">...</some-element>  

<some-element [ngClass]="{'class1 class2 class3' : true}">...</some-element>  
```
##ngSwitch
A structural directive that adds or removes templates (displaying or hiding views) when the next match expression matches the switch expression.  
```
<container-element [ngSwitch]="switch_expression">
  <!-- the same view can be shown in more than one case -->
  <some-element *ngSwitchCase="match_expression_1">...</some-element>
  <some-element *ngSwitchCase="match_expression_2">...</some-element>
  <some-other-element *ngSwitchCase="match_expression_3">...</some-other-element>
  <!--default case when there are no matches -->
  <some-element *ngSwitchDefault>...</some-element>
</container-element>
```
```
<container-element [ngSwitch]="switch_expression">
      <some-element *ngSwitchCase="match_expression_1">...</some-element>
      <some-element *ngSwitchCase="match_expression_2">...</some-element>
      <some-other-element *ngSwitchCase="match_expression_3">...</some-other-element>
      <ng-container *ngSwitchCase="match_expression_3">
        <!-- use a ng-container to group multiple root nodes -->
        <inner-element></inner-element>
        <inner-other-element></inner-other-element>
      </ng-container>
      <some-element *ngSwitchDefault>...</some-element>
    </container-element>
```
##ng-container
The Angular <ng-container> is a grouping element that doesn't interfere with styles or layout because Angular doesn't put it in the DOM.  
##ng-tempplate
renders only the hero-detail.
```
<template [ngIf]="currentHero">  
  <hero-detail [hero]="currentHero"></hero-detail>  
</template>  
```
##pipes for extending func
formatting strings, dates, numbers, upper, lower, etc  
###date  
```
{{ value_expression | date [ : format [ : timezone [ : locale ] ] ] }}
```
Examples are given in en-US locale.  
'short': equivalent to 'M/d/yy, h:mm a' (6/15/15, 9:03 AM).  
'medium': equivalent to 'MMM d, y, h:mm:ss a' (Jun 15, 2015, 9:03:01 AM).  
'long': equivalent to 'MMMM d, y, h:mm:ss a z' (June 15, 2015 at 9:03:01 AM GMT+1).  
'full': equivalent to 'EEEE, MMMM d, y, h:mm:ss a zzzz' (Monday, June 15, 2015 at 9:03:01 AM GMT+01:00).  
'shortDate': equivalent to 'M/d/yy' (6/15/15).  
'mediumDate': equivalent to 'MMM d, y' (Jun 15, 2015).  
'longDate': equivalent to 'MMMM d, y' (June 15, 2015).  
'fullDate': equivalent to 'EEEE, MMMM d, y' (Monday, June 15, 2015).  
'shortTime': equivalent to 'h:mm a' (9:03 AM).  
'mediumTime': equivalent to 'h:mm:ss a' (9:03:01 AM).  
'longTime': equivalent to 'h:mm:ss a z' (9:03:01 AM GMT+1).  
'fullTime': equivalent to 'h:mm:ss a zzzz' (9:03:01 AM GMT+01:00).  

```
{{ dateObj | date }}               // output is 'Jun 15, 2015'
{{ dateObj | date:'medium' }}      // output is 'Jun 15, 2015, 9:43:11 PM'
{{ dateObj | date:'shortTime' }}   // output is '9:43 PM'
{{ dateObj | date:'mm:ss' }}       // output is '43:11'
```
###LowerCasePipe
```
{{ value_expression | lowercase }}
```
simular as UpperCasePipe, TitleCasePipe

###PercentPipe
```
{{ value_expression | percent [ : digitsInfo [ : locale ] ] }}
  
<!--output '26%'-->  
    <p>A: {{a | percent}}</p>  
  
    <!--output '0,134.950%'-->  
    <p>B: {{b | percent:'4.3-5'}}</p>  
  
    <!--output '0 134,950 %'-->  
    <p>B: {{b | percent:'4.3-5':'fr'}}</p>  
  
```
###SlicePipe
```
<li *ngFor="let i of collection | slice:1:3">{{i}}</li>
...
    <p>{{str}}[0:4]: '{{str | slice:0:4}}' - output is expected to be 'abcd'</p>  
    <p>{{str}}[4:0]: '{{str | slice:4:0}}' - output is expected to be ''</p>  
    <p>{{str}}[-4]: '{{str | slice:-4}}' - output is expected to be 'ghij'</p>  
    <p>{{str}}[-4:-2]: '{{str | slice:-4:-2}}' - output is expected to be 'gh'</p>  
    <p>{{str}}[-100]: '{{str | slice:-100}}' - output is expected to be 'abcdefghij'</p>  
    <p>{{str}}[100]: '{{str | slice:100}}' - output is expected to be ''</p>  
```
###AsyncPipe
The async pipe subscribes to an Observable or Promise and returns the latest value it has emitted. When a new value is emitted, the async pipe marks the component to be checked for changes. When the component gets destroyed, the async pipe unsubscribes automatically to avoid potential memory leaks.

```
@Component({
  selector: 'async-promise-pipe',
  template: `<div>
    <code>promise|async</code>: 
    <button (click)="clicked()">{{ arrived ? 'Reset' : 'Resolve' }}</button>
    <span>Wait for it... {{ greeting | async }}</span>
  </div>`
})
export class AsyncPromisePipeComponent {
  greeting: Promise<string>|null = null;
  arrived: boolean = false;

  private resolve: Function|null = null;

  constructor() { this.reset(); }

  reset() {
    this.arrived = false;
    this.greeting = new Promise<string>((resolve, reject) => { this.resolve = resolve; });
  }

  clicked() {
    if (this.arrived) {
      this.reset();
    } else {
      this.resolve !('hi there!');
      this.arrived = true;
    }
  }
}
```
##ViewChild, ViewChildren
A template reference variable as a string (e.g. query <my-component #cmp></my-component> with @ViewChild('cmp'))   
Any provider defined in the child component tree of the current component (e.g. @ViewChild(SomeService) someService: SomeService)    
Any provider defined through a string token (e.g. @ViewChild('someToken') someTokenVal: any)    
A TemplateRef (e.g. query <ng-template></ng-template> with @ViewChild(TemplateRef) template;)    

##Directive, decorator
Decorator that marks a class as an Angular directive. You can define your own directives to attach custom behavior to elements in the DOM.  
like 'placeholder' in
```
<input value="abc" **placeholder**="firstname">  
```
reusable in whole project 


creation
```
ng g directive directives/HighlightedDirective
```
@HostBinding
@HostListener

or emit directive to other components:
```
@Input('highlighted')
  isHighlighted = false;

  @Output()
  toggleHighlight = new EventEmitter();

  constructor() {
    //console.log('highlighted created...');
  }

  @HostBinding('class.highlighted')
  get cssClasses() {
    return this.isHighlighted;
  }

  @HostBinding('attr.disabled')
  get disabled() {
    return "true";
  }

  @HostListener('mouseover', ['$event'])
  mouseover($event) {
    console.log($event);
    this.isHighlighted = true;
    this.toggleHighlight.emit(this.isHighlighted);
  }

toggle() {
    this.isHighlighted = !this.isHighlighted;
    this.toggleHighlight.emit(this.isHighlighted);
  }
```

##Structural Directives

ng g directive directive/ngx-name  

nix-name  

ngxNameDirective  
results to template  

```
import { Directive,  TamplateRef } from '@angular/core';

@Directive({
  selector: {'[ngxngxName]'}
})
export class NgxNameDirective {

  constructor(private templateRef: TemplateRef<any>, private viewContainer: ViewContainerRef) {
    
  }

  @Input()
  set ngxName(condition:booleam);
}
```
##Angular Injectable Services

## Modules

ng g m MODULE_NAME (--routing)   


