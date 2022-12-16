# Angular

Object Spread Operator Reducer Example: 
```ts
import { createReducer, on } from "@ngrx/store";
import { CounterCommands } from "../actions/count-actions";
export interface CountState {
    current: number;
    by: 1 | 3 | 5
}
const initialState:CountState = {
    current: 0,
    by: 1
}
export const reducer = createReducer(initialState,
    on(CounterCommands.countby, (s,a) => ({...s, by: a.by})),
    on(CounterCommands.reset, (s) => ({...s, current: 0})),
    on(CounterCommands.incremented, (currentState) => ({...currentState, current: currentState.current + currentState.by})),
    on(CounterCommands.decremented, (s) => ({...s, current: s.current - s.by}))
);
```
App Routing Module Typescript Routing Example: 
```ts
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { AboutUsComponent } from './features/about-us/about-us.component';
import { DashboardComponent } from './features/dashboard/dashboard.component';
import { GiftGivingComponent } from './features/gift-giving/gift-giving.component';

const routes: Routes = [
  {
    path: 'dashboard',
    component: DashboardComponent
  },
  {
    path: 'gifts',
    component: GiftGivingComponent
  },
  {
    path: 'about',
    component: AboutUsComponent
  },
  {
    path: 'counter',
    loadChildren: ()=> import('./features/counter/counter.module').then(m => m.CounterModule)
  },
  {
    path: '**',
    redirectTo: 'dashboard'
  }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }

```
Navigation Component Html Routing Example: 
```html
<ul class="nav nav-tabs">
    <li class="nav-item">
      <a class="nav-link" [routerLinkActive]="['active', 'pretty']" routerLink="dashboard">Dashboard</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" [routerLinkActive]="['active', 'pretty']" routerLink="gifts">Gift Giving</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" [routerLinkActive]="['active', 'pretty']" routerLink="about">About Us</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" [routerLinkActive]="['active', 'pretty']" routerLink="counter">Redux Counter</a>
    </li>
    
 </ul>

```