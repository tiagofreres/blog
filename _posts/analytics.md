#Analytics

##How to setup triggers

Every action/event on site can fire an analytics, in order to specify which ones should trigger it they will need to be set.

- Adding analytics handler into CTA's event listeners.
- Adding analytics handler on `document.body` for specific event types.
- Triggering specific event types over app logic.

```javascript
// Adding analytics handler into CTA's event listeners.
$('.analytics-trigger').on(EVENT.MOUSEDOWN, analyticsHandler);


// Adding analytics handler on document.body for specific event types.
$(document).on(Object.keys(ANALYTICS_EVENT).map(function(event){ 
  return ANALYTICS_EVENT[event];
}).join(' '), analyticsHandler);


// Triggering specific event types over app logic.
$('.play-button').trigger(EVENT.VIDEO_START, { 'video_name': videoTitle });
```

##How to identify TagID and its properties

Analytics handler should be able to identify which TagID belongs to the emmited event.

- Receiving an [`EventTarget`](https://developer.mozilla.org/en/docs/Web/API/EventTarget) that represents a CTA event.
- Setting up EventTarget Searchable Parameters.
- Setting TagIDs Rules based on Searchable Parameters.
- Creating logic to match Rules TagIDs Rules with Searchable Parameters.

```javascript
// Setting up EventTarget Searchable Parameters
function discoverMissingOptions(options) {
  if (options.$el) {
    return $.extend({
      template: discover.getTemplate(),
      module: discover.getModuleName(options.$el),
      submodule: discover.getSubModuleName(options.$el),
      props: {}
    }, options);
  }
  return options;
}

// Setting TagIDs Rules based on Searchable Parameters
forCtas = [
  {
    tagId: 'PURE_PROCESS_DROPDOWN_BUTTON_CLICK',
    propNames: ['panel_type', 'panel_title', 'state', 'cta'],
    atModules: arrayUtils.isIn(['pure-process']),
    atEvent: arrayUtils.isIn([EVENT.SELECTED_ITEM])
  },
  {
    tagId: 'PURE_PROCESS_DEALER_OVERLAY_LOAD',
    propNames: ['panel_type', 'panel_title'],
    atModules: arrayUtils.isIn(['pure-process-overlay']),
    atEvent: arrayUtils.isIn([EVENT.LOAD])
  },
  {
    tagId: 'PURE_PROCESS_DEALER_OVERLAY_SET_DEALER_CLICK',
    propNames: ['panel_type', 'panel_title', 'state', 'dealer_code'],
    atModules: arrayUtils.isIn(['pure-process-overlay']),
    atSubmodules: arrayUtils.isIn(['pure-process-dealers']),
    atEvent: arrayUtils.isIn([EVENT.MOUSEDOWN])
  },
  ...
];

// Creating logic to match Rules TagIDs Rules with Searchable Parameters
function defaultFindLogic(options) {
  return function(linkRule) {
    return (checkRule(linkRule.atTemplates, [options.template]) ||
      linkRule.atPath
        ? checkRule(linkRule.atPath, [PATHNAME, filterCta])
        : false) &&
      checkRule(linkRule.atModules, [options.module]) &&
      checkRule(linkRule.atSubmodules, [options.submodule]) &&
      checkRule(linkRule.atCtas, [options.$el && options.$el.attr('href'), filterCta]) &&
      checkRule(linkRule.atClass,
        [arrayUtils.toArray(options.$el && options.$el.get(0).classList || [])]) &&
      checkRule(linkRule.atEvent, [options.eventType] || []);
  };
}
```

##How to discover variable properties and dynamic values

Each TagID have different properties and dynamic values that change depending on content, that way the code should be able to identify those properties and discover those dynamic values.

- Receiving an [`EventTarget`](https://developer.mozilla.org/en/docs/Web/API/EventTarget) that represents a CTA event and a  property list, use it to discover those properties values.

```javascript
// Discover dynamic properties values
function ($eventTarget) {
  return {
    module: $eventTarget.closest('[data-module]').data('module'),
    type: $eventTarget.closest('[data-type]').data('type')
  };
}
```


##How to apply logic on analytics properties before dispatching it

Sometimes it is necessary to change properties values before sending it to analytics API, like filling up an empty field or adding globals properties.

- After filling all properties values, sometimes it is necessary to modify, add or remove some properties. So this would be that step.

**Set `<parameter>` with `<global_js_variable>` value**

`data-analytics-global-<parameter>="<global_js_variable>"`

**Set `<parameter>` with `<css_selector>` element text/value**

`data-analytics-css-<parameter>="<css_selector>"`

**Set `<parameter>` with `<scss_selector>` element text/value, `<scss_selector>` is limited on module `data-analytics-scope`**

`data-analytics-scss-<parameter>="<scss_selector>"`

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
