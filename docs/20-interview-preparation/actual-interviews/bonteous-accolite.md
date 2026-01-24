
# Bonteous-Accolite

## Interview Metadata
- on: 2026-01-17 Sat 16:00-17:15
- role: Angular Developer
- hr: Karthika & Lovely
- level: L2
- interviewer: Prem


## Questions
1. Self Intro

1. Ways to communicate Data among angular components
1. Types of directives
1. View Encaptulation
1. Pure vs Impure Pipes
1. Monorepo workspace
1. OnPush vs OnPull change detection
1. Rxjs vs Ngrx
1. effects in Ngrx
1. Component Inheritance
1. HostListner vs Viewchild
1. Dynamically inject a component
1. FormGroup vs FormArray
1. LinkedList vs Set
1. Bootstrap grid system
1. Css box model - the different layers
1. position relative vs absolute
1. margin collapsing
1. ES5 vs ES6
1. Object destructuring
1. Shallow copy vs Deep copy
1. Immediately invoked functions


## Problems
1. find the occurence count in an array
1. find 13 table using closure function
1. problem on shallow copy using Object.assign and deep copy using Json.stringify and Json.parse
1. analyse the code and predict the output - switchMap vs MergeMap

```ts

import { Component } from '@angular/core';
import { from, of } from 'rxjs';
import { delay, switchMap, mergeMap } from 'rxjs/operators';

@Component({
  selector: 'app-switch-merge',
  template: `Check console`,
})
export class SwitchMapMergeMap {
  // Simulated API call
  fakeApiCall(id: number) {
    return of(`Response from request ${id}`).pipe(delay(1000));
  } // Example input stream

  ngOnInit() {
    const requests = from([1, 2, 3]);

    requests
      .pipe(switchMap((id) => this.fakeApiCall(id)))
      .subscribe((result) => console.log('switchMap:', result));

    requests
      .pipe(mergeMap((id) => this.fakeApiCall(id)))
      .subscribe((result) => console.log('mergeMap:', result));
  }
}
```

