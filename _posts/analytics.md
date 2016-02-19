#Analytics

##How to setup triggers

Every action/event on site can fire an analytics, in order to specify which ones should trigger it they will need to be set.

- Adding analytics handler into CTA's event listeners
- Adding analytics handler on `document.body` for specific event types
- Triggering specific event types over app logic

##How to identify TagID and its properties

Analytics handler should be able to identify which TagID belongs to the emmited event.

- Using [`EventTarget`](https://developer.mozilla.org/en/docs/Web/API/EventTarget), received by analytics handler, identify which TagID it belongs.

##How to discover variable properties and dynamic values

Each TagID have different properties and dynamic values that change depending on content, that way the code should be able to identify those properties and discover those dynamic values.

##How to apply logic on analytics properties before dispatching it

Sometimes it is necessary to change properties values before sending it to analytics API, like filling up an empty field or adding globals properties.

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
