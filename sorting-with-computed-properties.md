Another common usage of computed properties is sorting. Continuing to use our SuperRentals app as an example, let's say we want to display a city's rentals in order of cost.

We display our rentals on a `city-tile` template, within a `city` route:

<div class="filename">app/templates/components/city-tile.hbs</div>
```
<h4>Location: {{fullLocation}}</h4>

<h3>Rentals available in {{city.name}}:</h3>

<ul>
  {{#each city.rentals as |rental|}}
    {{rental-tile rental=rental}}
  {{/each}}
</ul>

<button {{action 'delete' city}}>Delete City</button>
```

However, by default, this will list rentals in order of creation. What if we want the _least expensive_ rentals displayed at the top? 

In order to sort the rentals by cost, we'll use a computed property on the `city-tile` component by adding the following code:

<div class="filename">app/components/city-tile.js</div>
```
import Ember from 'ember';

export default Ember.Component.extend({
  sortedRentals: Ember.computed.sort('city.rentals', 'cost:asc'),

  actions: {
   ...
```

Now, we can call `sortedRentals` in our `city-tile` template to view the newly-ordered rentals for our city:

<div class="filename">app/templates/components/city-tile.hbs</div>
```
<h4>Location: {{fullLocation}}</h4>

<h3>Rentals available in {{city.name}}:</h3>

<ul>
  {{#each sortedRentals as |rental|}}
    {{rental-tile rental=rental}}
  {{/each}}
</ul>

<button {{action 'delete' city}}>Delete City</button>
```

For more information on Computed Properties, check out the [Ember Guides](https://guides.emberjs.com/v2.3.0/object-model/computed-properties/).