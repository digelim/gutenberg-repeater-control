### Import the module

```import { repeaterData, RepeaterControl } from './gutenberg-repeater-control/index.js';```

### Add an attribute

```attributes: {
  faq: {
    type: "string|array",
    source: "attribute",
    selector: "select",
    attribute: "faq",
    default: [],
  }
}
```

### Read the data

```
edit: (props) {
  const { attributes, setAttributes } = props;
  const faqData = repeaterData(props.attributes.faq, true);

...

}
```

```
<InspectorControls>
  <PanelBody title="Block settings">
    <PanelRow>
      <b>FAQs</b>
    </PanelRow>
    <PanelRow>
      <RepeaterControl
        max={20}
        value={props.attributes.faq}
        onChange={(val) => {
          props.setAttributes({ faq: val });
        }}
      >
        {(value, onChange) => {
          return [
            <TextControl
              label="Question"
              value={value.question}
              onChange={(v) => {
                value.question = v;
                onChange(value);
              }}
            />,
            <TextareaControl
              label="Answer"
              value={value.answer}
              onChange={(v) => {
                value.answer = v;
                onChange(value);
              }}
            />,
          ];
        }}
      </RepeaterControl>
    </PanelRow>
  </PanelBody>
</InspectorControls>

```

### Display the data
    
```    
{faq.map((v) => {
  return (
    <div>
        {v.question}
          {v.answer}
    </div>
  )
})}
```
