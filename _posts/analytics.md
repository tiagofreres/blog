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
