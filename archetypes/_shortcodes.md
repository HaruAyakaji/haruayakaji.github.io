+++
title = 'This page is not for generate.'
draft = true
+++

### Template for tab

{{< tabs >}}
{{% tab title="Tab title 1" %}}

```js
console.log('Tab title 1');
```

{{% /tab %}}
{{% tab title="Tab title 2" %}}

```js
console.log('Tab title 2');
```

{{% /tab %}}
{{< /tabs >}}

### Template for notice

{{% notice style="info" title="Notice title" %}}

{{% /notice %}}

{{% notice style="note" title="Notice title" %}}

{{% /notice %}}

{{% notice style="tip" title="Notice title" %}}

{{% /notice %}}

{{% notice style="warning" title="Notice title" icon="exclamation-circle" %}}

{{% /notice %}}
