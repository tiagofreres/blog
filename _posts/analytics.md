#Analytics

##How to setup triggers

Every action/event on site can fire an analytics, in order to specify which ones should trigger it they will need to be set.

- Adding analytics handler into CTA's event listeners.
- Adding analytics handler on `document.body` for specific event types.
- Triggering specific event types over app logic.

```javascript
// Adding analytics handler into CTA's event listeners.
$('.analytics-trigger').on(ANALYTICS_EVENT.MOUSEDOWN, analyticsHandler);

// Adding analytics handler on document.body for specific event types.
$(document).on(Object.keys(ANALYTICS_EVENT).map(function(event){ 
  return ANALYTICS_EVENT[event];
}).join(' '), analyticsHandler);
```

##How to identify TagID and its properties

Analytics handler should be able to identify which TagID belongs to the emmited event.

- Receiving an [`EventTarget`](https://developer.mozilla.org/en/docs/Web/API/EventTarget) that represents a CTA event, use it to identify which TagID it belongs and which properties need to be filled.

##How to discover variable properties and dynamic values

Each TagID have different properties and dynamic values that change depending on content, that way the code should be able to identify those properties and discover those dynamic values.

- Receiving an [`EventTarget`](https://developer.mozilla.org/en/docs/Web/API/EventTarget) that represents a CTA event and a  property list, use it to discover those properties values.

##How to apply logic on analytics properties before dispatching it

Sometimes it is necessary to change properties values before sending it to analytics API, like filling up an empty field or adding globals properties.

- After filling all properties values, sometimes it is necessary to modify, add or remove some properties. So this would be that step.

**Used when need to perform a search and the value can change by content**

`data-analytics-selector-<parameter>`

**Used when no search need to be done and the value is be always the same and do not change by content**

`data-analytics-param-<parameter>`

**Used to connect with `data-analytics-selector-<parameter>`**

`data-analytics-<parameter>`

**Used to delimit analytics scope on HTML module structure**

`data-analytics-scope`

```HTML
<div data-analytics-scope data-analytics-param-panel-type="module-1">
  <div data-analytics-selector-cta>
    <div>
      <div>
        <div data-analytics-cta>Analytics CTA 1</div>
      </div>
    </div>
    <div>
      <p>Something</p>
    </div>
    <div>
      <a class="cta">CTA EXAMPLE 1</a>
    </div>
  </div>
  <div data-analytics-selector-cta>
    <div>
      <div>
        <div data-analytics-cta>Analytics CTA 2</div>
      </div>
    </div>
    <div>
      <p>Something</p>
    </div>
    <div>
      <a class="cta">CTA EXAMPLE 2</a>
    </div>
  </div>
</div>
```
